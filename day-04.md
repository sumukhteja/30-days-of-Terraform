# Day 4: Versions and the lock file

Version constraints:
- `= 1.2.0` exact
- `>= 1.2.0` at least
- `~> 1.2.0` allows 1.2.x only (rightmost part can increase)
- `~> 1.2` allows 1.x from 1.2 up, but not 2.0

`required_version` in the `terraform` block pins the CLI version. `required_providers` pins providers.

**`.terraform.lock.hcl`**
- Created by `terraform init`. Records the exact provider versions and hashes that were selected.
- Commit it to git so everyone and CI use the same versions.
- It only covers providers, not modules.
- `terraform init -upgrade` picks newer versions allowed by your constraints and updates the lock file.

The `.terraform/` folder itself should be gitignored. It's just the downloaded plugins and modules.

Something that surprised me: if the lock file says 5.40 and your constraint is `~> 5.0`, Terraform keeps using 5.40 even if 5.80 is out, until you run `init -upgrade`.
