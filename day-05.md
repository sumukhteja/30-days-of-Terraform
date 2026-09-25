# Day 5: The core workflow

Write, plan, apply. That's the loop.

- `terraform init`: downloads providers and modules, sets up the backend. Safe to run again anytime.
- `terraform plan`: compares config, state and real infra, shows what will change. `+` create, `-` destroy, `~` update in place, `-/+` replace.
- `terraform apply`: runs a plan and asks for confirmation. `-auto-approve` skips the prompt (CI only).
- `terraform destroy`: removes everything in the state. Same as `apply -destroy`.

Saved plans:

```bash
terraform plan -out=tfplan
terraform apply tfplan
```

Applying a saved plan doesn't ask for confirmation, because you already reviewed it. This is how pipelines should work: plan in one step, review, apply exactly that plan.

`terraform show tfplan` prints a saved plan, and `terraform show -json tfplan` gives JSON you can feed into policy checks.

`-refresh-only` just updates state to match reality without changing infra. The old `terraform refresh` command does the same thing but is deprecated.
