---
applyTo: "api/**/*.py,src/**/*.py,spider/**/*.py,tests/**/*.py"
---

# Backend Instructions

- Preserve current module boundaries and reuse existing services, schemas, data collectors, and fallback logic instead of creating parallel paths.
- Changes touching config, CLI flags, schedule semantics, API behavior, auth, trading execution, risk checks, or report payloads must sync relevant templates/docs and assess Web compatibility.
- Changes in `spider/` or `src/data/` must preserve provider priority, normalization behavior, timeout/retry expectations, and graceful degradation.
- Prefer deterministic validation; at minimum run `python -m py_compile` on changed Python files plus the closest tests.
- Do not let a single provider, notification channel, or optional integration failure break the main analysis flow unless the requirement explicitly demands fail-fast behavior.
- Trading and risk code must default to fail-safe behavior. Never silently place orders when inputs, account state, or risk checks are uncertain.
