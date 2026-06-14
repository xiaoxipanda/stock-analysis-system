---
applyTo: "apps/web/**"
---

# Client Instructions

- Preserve the planned `apps/web` frontend boundary; reuse current API/state patterns once implementation exists instead of adding parallel client abstractions.
- If a change affects API fields, auth state, route behavior, Markdown/chart rendering, local backend startup, or report payloads, assess backend compatibility.
- Validate Web changes with `cd apps/web && npm ci && npm run lint && npm run build` when feasible.
- Keep user-facing trading, portfolio, risk, and backtest screens explicit about pending/loading/error states once implemented.
