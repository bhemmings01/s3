```
resource "aws_s3_bucket_lifecycle_configuration" "sftp_livedisk_staging" {
  for_each = {
    for name, default in var.s3_bucket_names : name => default
    if default.disk_type == "staging"
  }
  depends_on = [aws_s3_bucket.sftp_livedisk]
  bucket = each.key
  rule {
    id = "housekeep-staged-reports"

    expiration {
      days = 7
    }

    filter {
      prefix = "staging"
    }

    status = "Enabled"
  }
  rule {
    id = "delete-expired-markers"

    expiration {
      expired_object_delete_marker = true
    }

    abort_incomplete_multipart_upload {
      days_after_initiation = 2
    }

    status = "Enabled"
  }
}

```
