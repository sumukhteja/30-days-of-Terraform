# Terraform Commands & Essentials

Terraform = declarative language. Official workflow: **Write -> Plan -> Apply**.

## Basics
```bash
type nul > main.tf            # create empty file (Windows; use `touch main.tf` on Linux/Mac)

terraform fmt                 # format all .tf files in current dir
terraform fmt -recursive      # include subdirectories

terraform init                # initialize working directory
terraform init -upgrade       # re-init and upgrade providers/modules

terraform plan
terraform apply
terraform apply -auto-approve

terraform destroy
terraform destroy -target=<resource_address>   # destroy a single resource
```

## Plan files
```bash
terraform plan -out=plan.tfplan

terraform show plan.tfplan
terraform show -json plan.tfplan
terraform show -json plan.tfplan > plan.json
terraform show -json plan.tfplan | jq
terraform show -json plan.tfplan | jq > plan.json

terraform apply plan.tfplan
```

## State
```bash
terraform state list
```

## Help
```bash
terraform -help
terraform apply -help
terraform -install-autocomplete
```

## Environment variables
```bash
export TF_LOG=DEBUG
export TF_VAR_svr_name=prod-db-01        # sets input variable `svr_name`
export AWS_ACCESS_KEY_ID=<your-access-key>
```

## Syntax (block types)
provider, resource, data, variable, output, terraform, module, import

## Working directory
`.terraform/`
- `providers/` - e.g. aws, random
- `modules/` - downloaded child modules

## Organising code (separate .tf files)
variables.tf, network.tf, firewall.tf, kubernetes.tf, dns.tf, outputs.tf