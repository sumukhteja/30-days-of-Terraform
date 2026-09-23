# Day 3: Providers

Providers are plugins that talk to APIs. Terraform core does the planning, providers do the actual calls.

- Found on the **Terraform Registry**. Source address format is `namespace/type`, like `hashicorp/aws`. Full form is `registry.terraform.io/hashicorp/aws`.
- Tiers: official (HashiCorp), partner, community.
- Downloaded into `.terraform/` during `terraform init`.

Multiple configurations of the same provider using `alias`:

```hcl
provider "aws" {
  region = "us-east-1"
}

provider "aws" {
  alias  = "west"
  region = "us-west-2"
}

resource "aws_s3_bucket" "backup" {
  provider = aws.west
  bucket   = "backup-bucket-example"
}
```

Without an alias you get the default provider config.

Credentials should never go in the config. Use env vars (`AWS_PROFILE`, `AWS_ACCESS_KEY_ID`), a shared credentials file, or better, a role.
