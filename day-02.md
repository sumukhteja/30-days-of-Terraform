# Day 2: Installing and the first config

Got Terraform installed and wrote a first config.

A config is just `.tf` files in a folder. Terraform reads all of them together, file names don't matter to it. The usual split:
- `main.tf` for resources
- `variables.tf` for inputs
- `outputs.tf` for outputs
- `versions.tf` or `providers.tf` for the terraform and provider blocks

First real config:

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "notes" {
  bucket = "my-terraform-notes-bucket-12345"
}
```

A resource block is `resource "<type>" "<local name>"`. The address you refer to it by is `aws_s3_bucket.notes`.

`terraform fmt` fixes formatting and `terraform validate` checks the syntax and references. Running both before every plan is a good habit.
