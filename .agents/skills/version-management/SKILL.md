---
name: version-management
description: Inspect or plan Terraform module versions, submodule commit pins, tags, and release compatibility without conflating their independent versioning systems.
---

# Manage module versions

Distinguish these version records:

- Umbrella repository gitlink: the commit currently checked out for each Git submodule.
- Module repository history: branch, `HEAD`, and tags/releases in that module's own Git repository.
- Terraform Registry module constraints: `version` on a registry module source.
- Git module refs: `?ref=` or equivalent ref in a Git source.
- Terraform/provider constraints: `required_version` and `required_providers` in module code.

Workflow:

1. Read root and module Git status before inspecting or changing anything. Capture the current gitlink SHA, module HEAD/branch, and available local tags with `git -C modules/<name> describe --tags --always` and `git -C modules/<name> tag --sort=-version:refname`.
2. Inspect version constraints and source references in Terraform code and the target module's workflow/release configuration. Treat local tags as evidence only; they may not represent the latest remote release.
3. For an upgrade request, identify the requested target precisely. Explain semantic-version compatibility only where the published release notes or interface evidence support it. Never assume latest or silently choose a release.
4. Change a module source constraint in the caller only when requested. Change the umbrella gitlink only when the task intends to pin a different submodule commit. Keep those edits separate and describe each.
5. Do not create or switch branches, stage or commit, create/move tags, publish releases or module versions, or advance unrelated submodules. These Git and release operations are user-owned. Do not fetch/pull unless needed for an explicitly requested, read-only current-version lookup; use official registry/provider sources for current release facts where possible.

Report current and proposed versions/SHAs, exact files or gitlinks affected, compatibility evidence, and remaining uncertainty. This workflow does not publish releases.
