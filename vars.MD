```
variable "bl" {
  default = ["foo", "bar", "next"]
}

variable "disks" {
  default = ["live", "staging", "quarantine"]
}



locals {
  mr_s3_buckets = [
  for pair in setproduct(var.bl, var.disks) : {
    full_name = format("%s-mbr-%s-s3-%s", var.env_name, pair[0], pair[1])
    account_type = "reporting"
    disk_type = pair[1]
    bl = pair[0]
    dated = jsondecode(file("lookup.json"))[var.env_name][pair[0]].dated
    nondated = jsondecode(file("lookup.json"))[var.env_name][pair[0]].nondated
  }
]

 mr_s3_buckets_map = { for idx, item in local.mr_s3_buckets:  item["full_name"] => {account_type = item["account_type"], bl = item["bl"], disk_type = item["disk_type"], dated = item["dated"], nondated = item["nondated"]} }
 uuid = {for k, v in random_id.s3_id_bl: k =>v.hex}

 all_buckets = merge(local.mr_s3_buckets_map, var.s3_bucket_names)


```
