---
applyTo: "README.md,docs/**,AGENTS.md,CLAUDE.md,.github/**,.claude/skills/**,scripts/**,docker/**"
---

# Governance Instructions

- Keep commands, file paths, workflow names, config keys, release paths, and directory references aligned with the executable repository state.
- `AGENTS.md` is the canonical AI collaboration document; if its meaning changes, sync `CLAUDE.md`, `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`, and repository skills as needed.
- Explain which pipeline, release path, deployment path, review automation, or governance asset is affected and what the rollback path is.
- Keep `README.md` limited to homepage-level content; put detailed behavior, configuration, troubleshooting, field contracts, and edge cases in `docs/*.md`.
- Avoid widening permissions, secret exposure, or destructive automation without a clearly documented need.
- When creating, reviewing, or suggesting PRs, prefer PR titles in `<type>: <change summary>` form and omit tool/agent source prefixes.
