# Day 6: Resources and references

Resources can refer to each other using `<type>.<name>.<attribute>`:

```hcl
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
}
```

Because the subnet references `aws_vpc.main.id`, Terraform knows to create the VPC first. That's an implicit dependency, and it's how almost all ordering works.

Arguments vs attributes:
- **Arguments** are what you set (`cidr_block`).
- **Attributes** are what the provider gives back after creation (`id`, `arn`). Some aren't known until apply, which is why the plan shows `(known after apply)`.

Changing some arguments updates in place. Changing others (like a subnet's `cidr_block`) forces replacement. The plan tells you with `# forces replacement`.
