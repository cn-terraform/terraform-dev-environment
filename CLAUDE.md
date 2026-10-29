# Claude Code project instructions

Read and follow [AGENTS.md](AGENTS.md) for repository structure, module boundaries, Git/submodule handling, Terraform documentation, and validation. Use [MODULES_OVERVIEW.md](MODULES_OVERVIEW.md) as an orientation map, then verify all module-specific details in that module's current source and README.

This is an umbrella repository with independently versioned module Git submodules. Do not treat the root as a Terraform root module or update unrelated submodules. Make module changes inside the target module repository and inspect Git status at both levels before and after work.

Project workflows are available as skills under `.claude/skills/`. Their Codex-compatible counterparts live under `.agents/skills/`; keep both copies in sync when editing a skill.
