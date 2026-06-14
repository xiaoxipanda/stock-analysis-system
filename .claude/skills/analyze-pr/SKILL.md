# Analyze PR

分析 GitHub Pull Request，评估必要性、描述完整性、验证证据、主要风险与是否可直接合入。

**Repository**: https://github.com/xiaoxipanda/stock-analysis-system/pulls

## Usage

```text
/analyze-pr <pr_number>
```

## Instructions

分析时使用简洁中文，优先遵循仓库根目录 `AGENTS.md`。

### Step 1: 拉取 PR 基本信息

```bash
gh pr view <pr_number> --repo xiaoxipanda/stock-analysis-system
gh pr view <pr_number> --repo xiaoxipanda/stock-analysis-system --comments
gh pr checks <pr_number> --repo xiaoxipanda/stock-analysis-system
gh pr diff <pr_number> --repo xiaoxipanda/stock-analysis-system
```

如有失败的 CI，优先查看失败日志，而不是立刻在本地重跑全部检查。

### Step 2: 检查标题与描述完整性

- PR title 建议符合 `<type>: <change summary>`
- 类型优先为 `fix`、`feat`、`refactor`、`docs`、`chore`、`test`、`ci`
- 不建议包含 `[codex]`、`codex`、`autocode`、`copilot` 或其他工具/agent 来源前缀
- 标题格式不应单独作为 review blocker

### Step 3: 优先使用 CI / Diff 证据

- 先根据 `gh pr checks`、PR diff、现有测试与工作流日志判断问题
- 仅当 CI 未覆盖改动面、CI 结果不足以定性问题、或需要验证关键回归风险时，再补充本地最小验证
- 不要默认切换当前分支或执行 `gh pr checkout`

### Step 4: 评估正确性与风险

重点检查：

- 是否解决了明确问题，且没有夹带无关改动
- 是否破坏 API / Schema / Web 兼容性
- 是否破坏 fallback、降级路径、通知链路、交易风控或发布流程
- 是否存在明显逻辑错误、异常吞没、安全问题、配置语义变化未同步文档

### Step 5: 生成评审文档

保存到 `.claude/reviews/prs/pr-<number>.md`。

## Output Document Format

```markdown
# PR #<number> Analysis

**Date**: YYYY-MM-DD
**Status**: Pending Review

## Findings

- [严重级别] file:line - 问题描述

## Summary

- 必要性：
- 是否有对应 issue：
- PR 类型：
- PR title：
- description 完整性：
- 验证情况：
- 主要风险：
- 是否可直接合入：

## Validation Evidence

- CI 结论：
- 本地补充验证：

## Compatibility And Risk

- API / Web：
- 配置 / Docker / GitHub Actions：
- fallback / 通知 / 报告结构：
- 交易 / 风控：

## Draft Review Comment

<建议评论内容>
```

## Allowed Auto-Actions

- 拉取 PR 元数据、diff、评论和 CI 状态
- 阅读相关代码、模板、工作流与文档
- 在必要时执行最小化本地验证
- 生成评审文档

## Actions Requiring Confirmation

- 发布评论
- Approve PR
- Request changes
- Merge PR
- 关闭 PR
