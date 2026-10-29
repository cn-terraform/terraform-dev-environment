---
name: module-comparison
description: Compare two or more Terraform modules in this umbrella repository by purpose, interfaces, implementation, dependencies, examples, constraints, and checks.
---

# Compare modules

1. Confirm the selected module directories from `.gitmodules`, then inspect each using the `module-exploration` workflow.
2. Compare the same evidence categories for every module: purpose, Terraform/provider constraints, required inputs and defaults, outputs, major resources, Terraform module sources, examples, and validation workflow.
3. Separate verified implementation differences from README claims. Do not infer that similarly named modules are interchangeable or that one is a drop-in replacement.
4. If comparing compatibility, trace how the caller supplies inputs and consumes outputs. Check constraints and source references on both sides; explain any unknowns.
5. Present results in a concise table followed by practical selection guidance and any documentation gaps.

Comparison is read-only unless a change is explicitly requested. Do not edit module pins or repositories while comparing.
