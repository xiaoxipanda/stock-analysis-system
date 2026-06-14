# AGENTS.md

本文件用于约束本仓库的默认开发流程，目标是减少重复沟通、减少返工，并让改动和当前 AI 交易系统结构保持一致。

如果本文件与仓库中的脚本、工作流、代码现状不一致，以实际可执行内容为准，并在相关改动中同步修正规范文档。

## 1. 硬规则

- 遵循现有目录边界：
  - 后端 API 层放在 `api/`
  - 后端领域与应用核心放在 `src/`
  - Web 前端放在 `apps/web/`
  - 原始数据采集和爬虫放在 `spider/`
  - 配置模板放在 `config/`
  - 部署资产放在 `docker/`
  - 运维与开发脚本放在 `scripts/`
  - 文档放在 `docs/`
  - 测试放在 `tests/`
- 未经明确确认，不执行 `git commit`、`git tag`、`git push` 或创建 PR。
- commit message 使用英文，不添加 `Co-Authored-By`。
- 不写死密钥、账号、绝对路径、模型名、端口或环境差异逻辑。
- 优先复用现有模块、配置入口、脚本和测试，不新增平行实现。
- 默认稳定性优先于顺手优化；非当前任务直接需要的重构、抽象和基础设施迁移一律克制。
- 新增配置项时，必须同步更新配置模板和相关文档。
- 涉及用户可见能力、CLI/API 行为、部署方式、通知方式、报告结构变化时，必须同步更新相关文档。
- 修改报告格式、报告渲染效果或 Web UI 界面时，PR 描述应附受影响报告或页面截图；无法截图时说明原因与替代验证证据。
- 一次性验收截图、审查截图和临时可视证据不应作为仓库文件合入；应放在 PR 描述、评论、Actions artifact 或外部证据链接中。
- `README.md` 只用于项目定位、核心能力总览、快速开始、主要入口等首页级信息；更细的模块行为、页面交互、配置、排障和字段契约放入 `docs/*.md`。
- 注释、docstring、日志文案以清晰准确为准，不强制要求英文，但应与文件语境保持一致。

## 1.1 PR 标题规范

- 推荐使用 `<type>: <change summary>` 作为 PR 标题，例如 `docs: add AI trading system structure`。
- 类型优先为 `fix`、`feat`、`refactor`、`docs`、`chore`、`test`、`ci`。
- 标题应描述实际变更内容，建议不添加 `[codex]`、`codex`、`autocode`、`copilot` 或其他工具/agent 来源前缀。
- 该规范用于协作一致性，不应单独作为 review 阻断项。

## 1.2 贡献质量底线

- 不接受以堆叠代码量、扩大 diff 面、补丁式响应 review 来替代真实设计收敛的 PR。
- 贡献质量以是否解决明确问题、是否最小化影响面、是否保持现有契约一致、是否覆盖真实风险路径为准。
- 使用 AI 辅助开发本身不是问题；问题是提交未经人工语义审查、未验证、未收敛的 AI 生成内容。
- review 反馈后，不接受只在被指出的位置追加局部 patch。应重新检查同一业务语义涉及的入口、配置、测试、文档、workflow 和用户可见路径。

## 2. AI 协作资产治理

- `AGENTS.md` 是仓库内 AI 协作规则的唯一真源。
- `CLAUDE.md` 用于兼容 Claude 生态，必须明确指向 `AGENTS.md`。
- `.github/copilot-instructions.md` 与 `.github/instructions/*.instructions.md` 是 GitHub Copilot / Coding Agent 的镜像或分层补充；若与本文件冲突，以 `AGENTS.md` 为准。
- 仓库协作 skill 存放在 `.claude/skills/`，分析产物存放在 `.claude/reviews/`；前者可以入库，后者默认视为本地产物。
- 修改 AI 协作治理资产时，执行：

```bash
python scripts/check_ai_assets.py
```

## 3. 仓库速览

- 项目定位：基于 AI Agent 的股票分析与交易系统。
- 当前基础：`spider/AKShare/consultationInformation` 提供 AKShare 采集能力。
- 目标主流程：采集数据 -> 数据标准化 -> 特征工程 -> 策略/回测/风控 -> LLM 分析 -> 交易决策 -> 通知与前端展示。
- 关键目录：
  - `api/`：后端 API 层
  - `apps/web/`：Web 前端
  - `src/agents/`：AI agent 编排
  - `src/data/`：数据接入与标准化
  - `src/features/`：特征工程
  - `src/strategies/`：策略规则
  - `src/backtest/`：回测
  - `src/risk/`：风险控制
  - `src/trading/`：交易执行抽象
  - `src/portfolio/`：组合与持仓
  - `src/llm/`：LLM 适配与 prompt
  - `spider/`：原始数据采集

## 4. 常用命令

### 后端验证

```bash
python -m py_compile <changed_python_files>
python -m pytest
```

### Web 验证

```bash
cd apps/web
npm ci
npm run lint
npm run build
```

### AI 协作资产验证

```bash
python scripts/check_ai_assets.py
```

## 5. 默认工作流

1. 判断任务类型：`fix / feat / refactor / docs / chore / test / review`。
2. 先读现有实现、配置、测试、脚本、工作流和文档，再动手修改。
3. 识别改动边界：后端 / API / Web / Spider / Workflow / Docs / AI 协作资产。
4. 判断是否命中高风险区域：配置语义、API / Schema、数据源 fallback、报告结构、认证、调度、发布流程、交易执行链路。
5. 只做和当前任务直接相关的最小改动，不夹带无关重构。
6. 改完后按改动面执行最接近的验证。
7. 最终交付默认说明：改了什么、为什么这么改、验证情况、未验证项、风险点、回滚方式。

## 6. 验证矩阵

- Python 后端改动：
  - 适用范围：`api/**`、`src/**`、`spider/**`、`tests/**`
  - 最低要求：`python -m py_compile <changed_python_files>`
  - 若影响 API、任务编排、报告生成、通知、数据源 fallback、交易执行或风控，交付说明中写明是否覆盖对应路径。
- Web 前端改动：
  - 适用范围：`apps/web/**`
  - 默认执行：`cd apps/web && npm ci && npm run lint && npm run build`
  - 若涉及 API 联调、路由、状态管理、图表渲染或认证状态，交付说明中说明联动面和未覆盖风险。
- 文档与治理文件改动：
  - 适用范围：`README.md`、`docs/**`、`AGENTS.md`、`.github/**`、`.claude/skills/**`
  - 不强制代码测试。
  - 改动 AI 协作治理资产时，执行 `python scripts/check_ai_assets.py`。
- 工作流 / 脚本 / Docker 改动：
  - 适用范围：`.github/**`、`scripts/**`、`docker/**`
  - 运行最接近改动面的本地验证，交付时说明影响了哪条流水线、发布路径或部署路径。

## 7. 稳定性护栏

- 配置与运行入口：修改环境变量、默认值、CLI 参数、服务启动方式、调度语义时，要评估本地运行、Docker、GitHub Actions、API 和 Web 的影响。
- 数据源与 fallback：修改 `spider/` 或 `src/data/` 时，要关注数据源优先级、失败降级、字段标准化、缓存与超时策略。
- API / Web 兼容：改 API / Schema / 认证 / 报告载荷时，要同时检查后端和 Web 的兼容性。
- 报告 / Prompt / 通知：修改报告结构、Prompt、提取器、通知模板时，要检查上游输入与下游消费方是否仍兼容。
- 交易 / 风控：修改 `src/trading/` 或 `src/risk/` 时，默认保持 fail-safe，不应在错误或不确定状态下静默下单。

## 8. Issue / PR / Skill 工作流

- 仓库协作 skill：
  - `.claude/skills/analyze-issue/SKILL.md`
  - `.claude/skills/analyze-pr/SKILL.md`
  - `.claude/skills/fix-issue/SKILL.md`
- 如果任务明确是 issue 分析、PR 审查、issue 修复，优先按对应 skill 执行，并将产物保存到 `.claude/reviews/`。
- skill 中的命令、模板、验证顺序和交付结构必须与 `AGENTS.md` 保持一致。
- skill 不得默认执行 `git pull`、`git push`、`git tag`、`gh pr create` 等会改变远端或当前分支状态的操作；这些操作必须要求用户确认。

## 9. 交付与发布

- 默认交付结构：
  - 改了什么
  - 为什么这么改
  - 验证情况
  - 未验证项
  - 风险点
  - 回滚方式
- 如果是 docs-only 任务，可写 `Docs only, tests not run`，但仍需说明是否核对了命令和文件名。
