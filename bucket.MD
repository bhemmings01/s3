```
resource "aws_s3_bucket" "sftp_livedisk" {
  for_each = var.s3_bucket_names
  bucket   = each.key
  lifecycle {
    prevent_destroy = true
  }

  tags = merge(
    var.s3_tags,
    local.tags,
    {
      "Name" = format("%s-%s-%s-s3%s-live-disk", var.env_name, var.app_name, each.value.account_type, var.region_mem)
    },
    {
      "DataClassification" = "${var.dataclassification}"
    },
  )
}

```
