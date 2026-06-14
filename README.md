# stock-analysis-system

Ai Agent Stock Analysis System

## Project Direction

This repository is being expanded into a full AI trading system. The current
`feature_dev_20260517` branch already contains AKShare-based stock information
collection under `spider/AKShare/consultationInformation`. The new structure
keeps that collector in place and adds room for a complete frontend and backend
architecture.

No application code has been added in this step. The new files are structure
markers and module notes for later implementation.

## Planned Directory Structure

```text
api/                         Backend HTTP API layer
  v1/
    endpoints/               Route modules for analysis, trading, portfolio, etc.
    schemas/                 Request and response schemas
apps/
  web/                       Frontend web application
    public/                  Static frontend assets
    src/
      api/                   API clients
      assets/                UI images, icons, and static imports
      components/            Reusable UI components
      hooks/                 Frontend hooks
      layouts/               Page shells and navigation layouts
      pages/                 Route-level pages
      stores/                Client-side state stores
      types/                 Frontend TypeScript/domain types
      utils/                 Frontend helpers
config/                      Environment and runtime configuration templates
data/                        Local runtime data, caches, and generated datasets
docker/                      Container and compose deployment assets
docs/
  architecture/              Architecture notes and module boundaries
scripts/                     Developer, operations, and data utility scripts
spider/                      Existing data collection modules
src/                         Backend domain and application core
  agents/                    AI agent orchestration and tool routing
  backtest/                  Backtesting engine and evaluation workflows
  core/                      Shared application primitives
  data/                      Data access and normalization
  features/                  Feature engineering and signal inputs
  llm/                       LLM provider adapters and prompts
  notifications/             Alert delivery integrations
  portfolio/                 Holdings, positions, and account views
  repositories/              Persistence abstractions
  risk/                      Risk controls and exposure checks
  schemas/                   Internal domain schemas
  services/                  Business services
  strategies/                Strategy definitions and execution rules
  trading/                   Order, broker, and execution abstractions
  utils/                     Shared backend helpers
tests/                       Backend, frontend, and integration tests
```

## Reference

The expanded layout is inspired by
[`ZhuLinsen/daily_stock_analysis`](https://github.com/ZhuLinsen/daily_stock_analysis),
especially its separation of API, frontend apps, backend domain modules,
deployment assets, documentation, scripts, and tests.
