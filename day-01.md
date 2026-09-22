# Day 1: Why infrastructure as code

Started with the why before the how.

Clicking around the console works until you need the same setup twice, or need to know who changed what. IaC fixes that:
- Infra lives in files, so it's versioned, reviewed in PRs, and repeatable.
- Same config can build dev, staging and prod.
- Less drift between what you think exists and what actually exists.

Terraform specifically:
- **Declarative**: you describe the end state, Terraform figures out the steps.
- Works with basically any platform through **providers** (AWS, Azure, GCP, Kubernetes, GitHub, Datadog...).
- Keeps a **state** file that maps your config to real resources.
- Written in **HCL**.

Editions:
- **Terraform Community** (the CLI, free).
- **HCP Terraform** (hosted, used to be Terraform Cloud): remote runs, state, policies, team access.
- **Terraform Enterprise**: self-hosted version of HCP Terraform.

Compared to CloudFormation: Terraform is multi-cloud and has a huge provider ecosystem, CloudFormation is AWS only but has no state file to manage.
