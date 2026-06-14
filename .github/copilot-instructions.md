# Repository Instructions

Canonical source: [`AGENTS.md`](../AGENTS.md).

If any instruction in this file conflicts with `AGENTS.md`, follow `AGENTS.md`.

## Core Rules

- Respect directory boundaries:
  - Backend API: `api/`
  - Backend core: `src/`
  - Web frontend: `apps/web/`
  - Data collection: `spider/`
  - Deployment/workflows: `scripts/`, `.github/workflows/`, `docker/`
- Do not run `git commit`, `git tag`, `git push`, or create PRs without explicit user confirmation.
- PR titles should use `<type>: <change summary>` where possible, and avoid `[codex]`, `codex`, `autocode`, `copilot`, or other tool/agent source prefixes.
- Do not hardcode secrets, accounts, ports, model names, absolute environment-specific paths, or environment-specific branches.
- Reuse existing modules, configuration entrypoints, scripts, and tests instead of adding parallel implementations.
- Keep `README.md` focused on homepage-level content; put detailed behavior, configuration, troubleshooting, field contracts, and edge cases in `docs/*.md`.
- When config semantics change, sync configuration templates and assess impact on local runs, Docker, GitHub Actions, API, and Web.

## Validation

- Backend changes: run `python -m py_compile` on changed Python files and the closest deterministic tests.
- Web changes: run `cd apps/web && npm ci && npm run lint && npm run build` when feasible.
- AI governance changes: run `python scripts/check_ai_assets.py`.

## AI Asset Governance

- `AGENTS.md` is the single source of truth for repository AI collaboration rules.
- `CLAUDE.md` must clearly point to `AGENTS.md`.
- Use `.github/instructions/*.instructions.md` for path-specific guidance.
- Current repository collaboration skills live in `.claude/skills/`; keep them aligned with `AGENTS.md`.
