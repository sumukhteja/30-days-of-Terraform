# Day 7: Data sources

Data sources read info about things that already exist, without managing them.

```hcl
data "aws_ami" "al2023" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["al2023-ami-*-x86_64"]
  }
}

resource "aws_instance" "web" {
  ami           = data.aws_ami.al2023.id
  instance_type = "t3.micro"
}
```

Referenced as `data.<type>.<name>.<attribute>`.

Handy ones:
- `aws_caller_identity` to get the current account ID
- `aws_region`
- `aws_availability_zones`
- `aws_iam_policy_document` to write IAM policies in HCL instead of raw JSON (nicer than heredocs)
- `terraform_remote_state` to read outputs from another config's state

Data sources are read during plan, unless they depend on something not known yet, then they wait until apply.

Rule I'm following: if something is created in this config, reference the resource. If it exists outside, use a data source. Don't hardcode IDs.
