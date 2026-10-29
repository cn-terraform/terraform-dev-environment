# Repository guidance for coding agents

## Purpose and structure

This is an umbrella repository for the `cn-terraform` Terraform modules. The root repository tracks module repositories as Git submodules under `modules/`; it does not contain a single Terraform root configuration. Each submodule has its own repository, development branch, tags/releases, CI, and module-specific conventions. Read [MODULES_OVERVIEW.md](MODULES_OVERVIEW.md) for a checked-out inventory.

## Find the work boundary first

1. Read the root `README.md` and this file, then inspect `.gitmodules` and `git status --short --branch`.
2. Identify the requested module under `modules/` and inspect that module's `README.md`, Terraform files, examples, `.pre-commit-config.yaml`, and `.github/workflows/` before editing.
3. Check both repository levels with `git -C <module-path> status --short --branch` and `git status --short --branch`. Preserve existing user changes.
4. Keep module implementation, tests, docs, and releases within that module repository. The umbrella repository should normally record only a submodule gitlink change when its pinned commit changes.

## Submodule and Git rules

- Do not run `git submodule update --remote`, `git submodule foreach git pull`, or otherwise advance unrelated modules. The root gitlink is an intentional pin.
- Never assume the submodule's checked-out branch, HEAD, or latest tag is the desired target. Inspect it first. A detached HEAD is normal for consumers of submodules.
- Do not edit a nested module's `.git` file, its remote, branch, tags, or release configuration unless the task specifically requires it.
- When asked to change module code, make the change in the module repository. Report the module commit and whether the umbrella gitlink also changed.
- Avoid root-level Terraform commands: the umbrella repository has no Terraform root module. Run validation from the module root or its examples as configured by that module.

## Terraform and documentation conventions

- Treat the module's current code, README, examples, tests, and workflow as the source of truth. Do not repeat dependency or architecture assumptions from the umbrella docs without checking actual `module` blocks and their `source` values.
- Preserve the module's supported Terraform/provider constraints and established style. Do not opportunistically modernize provider constraints, dependencies, security behavior, or naming while implementing an unrelated request.
- Keep input/output docs aligned with `variables.tf` and `outputs.tf`; check README-generated sections and hooks before changing them. Existing modules do not all use identical conventions.
- Examples are executable documentation. Reuse the nearest example, and update/add examples when a user-visible interface change needs one.
- For dependency analysis, distinguish Terraform module sources from provider requirements and from Git submodules. A registry source such as `cn-terraform/networking/aws` is not the same thing as a nested Git submodule.

## Validation

There is no umbrella-level Terraform validation command. Use the target module's own checks, normally its configured pre-commit hooks and CI workflow. Inspect the actual hook/workflow before choosing commands; versions and checks vary across modules. Validate examples from their own directories if their workflow does so. Do not run an AWS apply or any command that creates/changes cloud resources unless the user explicitly requested it.

When validation is not requested or cannot be run, make that clear in the handoff. Do not claim that a Terraform module was validated if only formatting, static inspection, or documentation checks were performed.

## Task-specific workflows

Reusable workflows are available in `.agents/skills/` for Codex and `.claude/skills/` for Claude Code:

- `module-exploration`: map one module's interface, implementation, examples, and checks.
- `module-comparison`: compare modules using evidence from their code and docs.
- `dependency-analysis`: trace module-to-module and provider dependencies.
- `version-management`: inspect independent submodule pins, tags, constraints, and compatibility implications.

Keep both skill copies in sync when changing their instructions. These skills are task guides, not authority to update module pins or publish releases.

## Handoff

Summarize the changed repository/module paths, explain the effect on the module interface or root gitlink, and list the checks actually run with their results. Call out relevant documentation or validation gaps without silently expanding the requested scope.
