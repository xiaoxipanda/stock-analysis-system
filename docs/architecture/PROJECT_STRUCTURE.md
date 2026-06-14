# AI Trading System Structure

This project is evolving from a stock information collector into a full AI
trading system. The directory layout is designed around clear boundaries:

- `api/` exposes backend capabilities to the web app and external clients.
- `apps/web/` hosts the frontend experience.
- `src/` contains backend domain logic and application services.
- `spider/` keeps data collection modules, including the current AKShare work.
- `config/`, `docker/`, `scripts/`, `docs/`, and `tests/` support operation,
  deployment, documentation, and verification.

## Backend Domains

- `agents/`: AI agent orchestration, tool routing, memory, and task planning.
- `backtest/`: historical simulation and strategy evaluation.
- `core/`: shared runtime primitives, application settings, and scheduling.
- `data/`: providers, normalization, market data loading, and cache boundaries.
- `features/`: technical, fundamental, sentiment, and event feature inputs.
- `llm/`: provider adapters, prompt templates, and model configuration.
- `notifications/`: alert routing for email, IM, webhook, and app channels.
- `portfolio/`: holdings, positions, performance, and account aggregation.
- `repositories/`: persistence interfaces and storage adapters.
- `risk/`: exposure, drawdown, stop loss, and pre-trade checks.
- `schemas/`: internal contracts shared across services.
- `services/`: application use cases that coordinate domain modules.
- `strategies/`: strategy definitions, signal generation, and rules.
- `trading/`: order lifecycle, broker adapters, execution, and fills.
- `utils/`: cross-cutting backend helpers.

## Frontend Domains

- `api/`: typed clients for backend endpoints.
- `components/`: reusable UI building blocks.
- `hooks/`: reusable frontend behavior.
- `layouts/`: shells, navigation, and route frames.
- `pages/`: dashboard, analysis, portfolio, backtest, risk, and trading pages.
- `stores/`: state management for user workflows.
- `types/`: frontend domain types.
- `utils/`: formatting, validation, and UI helpers.

## Implementation Notes

This commit intentionally adds structure only. Future changes should introduce
code module by module, with tests added alongside behavior.
