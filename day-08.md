# Day 8: Dependencies

Terraform builds a dependency graph and creates things in parallel where it can (10 at a time by default, `-parallelism` changes that).

- **Implicit**: one resource references another. Preferred.
- **Explicit**: `depends_on`, for when there's a hidden dependency Terraform can't see.

```hcl
resource "aws_instance" "app" {
  ami           = var.ami
  instance_type = "t3.micro"

  depends_on = [aws_iam_role_policy.app_s3]
}
```

Example of a hidden dependency: the app on the instance needs an IAM policy to exist at boot, but nothing in the instance config references that policy.

`depends_on` is a last resort. It makes plans more conservative since Terraform treats more values as unknown.

`terraform graph` outputs the graph in DOT format if you want to visualize it.

Destroy goes in reverse order of creation, which is why the graph matters there too.
