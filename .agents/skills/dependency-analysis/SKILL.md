---
name: dependency-analysis
description: Trace Terraform module dependencies and compatibility impacts across the independent module repositories in this umbrella checkout.
---

# Analyze dependencies

1. Inspect actual Terraform `module` blocks and `source` attributes recursively in the requested module(s). Use `rg -n 'module|source|provider|version' --glob '*.tf'` as a starting point, then read each matching block.
2. Classify each dependency correctly: Terraform module source (registry, Git, local path), provider requirement, or Git submodule relationship. They are different dependency systems.
3. For an internal `cn-terraform` source, resolve its corresponding directory in `modules/` when available. Record source version/ref constraints and note when the source is unpinned or the referenced module is absent/uninitialized.
4. Follow relevant transitive internal module sources only as far as the requested impact analysis requires. Confirm assumptions in source rather than relying on `MODULES_OVERVIEW.md` alone.
5. For a proposed change, identify callers and likely interface impact by finding where the affected module is referenced and comparing consumed outputs with inputs. Do not claim full downstream compatibility without examining the relevant constraints and interfaces.
6. Report a compact dependency graph or table, the source evidence, version/ref constraints, and unresolved risks.

Do not run `git submodule update --remote`, change provider/module versions, fetch remote state, or apply infrastructure unless separately requested. Keep analysis read-only by default.
