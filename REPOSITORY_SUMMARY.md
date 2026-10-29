# Repository summary

This project is an umbrella Git repository whose `modules/*` entries are independent Terraform module repositories recorded as submodules. The root commit pins one commit per module; Terraform work belongs inside the selected module repository, which owns its code, examples, CI, version constraints, tags, and releases.

There is no root Terraform configuration. Module composition occurs through Terraform module `source` references in each module's code. These references should not be confused with Git submodules in the umbrella checkout.

The actual inventory, observed internal module source references, and documentation gaps are maintained in [MODULES_OVERVIEW.md](MODULES_OVERVIEW.md). Operational boundaries for agents are maintained in [AGENTS.md](AGENTS.md).
