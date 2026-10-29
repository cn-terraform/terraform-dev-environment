# cn-terraform development environment

This repository is an umbrella checkout for the organisation's Terraform modules. Each directory under `modules/` is an independently versioned Git repository tracked here as a submodule. The root commit pins the exact module commit; changes to a module are developed and released in that module's repository.

## Getting started

Clone with the modules initialized:

```sh
git clone --recurse-submodules https://github.com/cn-terraform/terraform-dev-environment.git
```

If you already cloned the umbrella repository without submodules:

```sh
git submodule update --init --recursive
```

See [MODULES_OVERVIEW.md](MODULES_OVERVIEW.md) for the module inventory and [MODULE_DEPENDENCY_ORDER.md](MODULE_DEPENDENCY_ORDER.md) for the dependency graph and task order. See [AGENTS.md](AGENTS.md) for repository boundaries and agent workflows. Claude Code also reads [CLAUDE.md](CLAUDE.md); reusable Codex and Claude Code skills are in `.agents/skills/` and `.claude/skills/`.

## Working on a module

1. Choose `modules/<module-name>` and read its README, Terraform source, examples, and validation workflow.
2. Check the root and module Git status before editing. Work and commit in the module repository.
3. Run checks from the module's own repository, following its pre-commit configuration and CI workflow. There is no root Terraform configuration.
4. If the umbrella checkout should point at the new module commit, stage the changed submodule path in the root repository separately. This records a gitlink update; it does not create or publish a module release.

Module commits, tags, release cadence, provider constraints, and validation steps are managed independently. Do not update every submodule to its remote tip as a routine setup step.
