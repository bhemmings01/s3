# s3
scratch pad for s3

```
variable "s3_bucket_names" {
  description = "map of s3 bucket names"
  type        = map
  default = {
    dev-member-s3-live-disk = {
      account_type = "member",
      disk_type = "",
      bl = "",
      dated = "",
      nondated = ""
    },
    dev-client-s3-live-disk = {
      account_type = "client",
      disk_type = "",
      bl = "",
      dated = "",
      nondated = ""
    },
    dev-portal-scp-billing-s3-live-disk = {
      account_type = "scp-billing",
      disk_type = "",
      bl = "",
      dated = "",
      nondated = ""
    }
  }
}

```
