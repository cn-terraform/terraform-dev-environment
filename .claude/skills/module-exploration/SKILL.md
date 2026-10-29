---
name: module-exploration
description: Explore one Terraform module in this umbrella repository before making a change or answering questions about its interface, implementation, examples, dependencies, or validation.
---

# Explore a module

1. Identify the module path from `.gitmodules` and `MODULES_OVERVIEW.md`; confirm the directory is initialized.
2. Read the module README, `versions.tf`, `main.tf` and any split Terraform files, `variables.tf`, `outputs.tf`, and example directories. Inspect `.pre-commit-config.yaml` and `.github/workflows/` for validation expectations.
3. Check `git status --short --branch` at both umbrella root and module root. Record the module HEAD and branch; do not change them during exploration.
4. Summarize purpose from implementation and README, inputs and defaults from variable declarations, outputs from output declarations, AWS resources, internal/external module sources, examples, supported Terraform/provider constraints, and validation commands.
5. Compare generated README tables with variables/outputs and flag discrepancies or placeholder text. Mark missing evidence as unknown instead of inferring behavior.

Use paths and relevant block names in findings so another developer can verify them. This skill is read-only unless the user also requested an edit. Do not initialize absent submodules, fetch updates, plan against an AWS account, or modify files as part of exploration alone.
