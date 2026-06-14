# Analyze Issue

分析 GitHub Issue，判断其真实性、优先级、仓库责任边界与建议动作。

**Repository**: https://github.com/xiaoxipanda/stock-analysis-system/issues

## Usage

```text
/analyze-issue <issue_number>
```

## Instructions

分析时使用简洁中文，优先遵循仓库根目录 `AGENTS.md`。

### Step 1: 拉取 Issue 信息

```bash
gh issue view <issue_number> --repo xiaoxipanda/stock-analysis-system
gh issue view <issue_number> --repo xiaoxipanda/stock-analysis-system --comments
```

如为 bug，优先核对 issue 模板中是否提供了版本基线、运行环境、复现步骤、日志或报错信息。

### Step 2: 回答核心问题

- 版本是否明确
- 问题是否真实且可验证
- 是否属于仓库责任边界
- 是否值得立即处理

### Step 3: 结合仓库现状做证据检查

- 阅读相关代码、配置、测试、脚本、工作流与文档
- 如果问题涉及 API、数据源 fallback、报告生成、通知、认证、交易、风控或发布流程，明确写出影响面
- 判断是实际 bug、环境配置问题、使用方式问题，还是外部依赖问题

### Step 4: 生成分析文档

保存到 `.claude/reviews/issues/issue-<number>.md`。

## Output Document Format

```markdown
# Issue #<number> Analysis

**Date**: YYYY-MM-DD
**Status**: Pending Review

## Summary

- 版本基线：
- 是否合理：
- 是否是 issue：
- 是否好解决：
- 结论：
- 分类：
- 优先级：
- 难度：
- 建议动作：

## Evidence

- 关键 issue 信息：
- 关键代码/脚本/工作流证据：

## Impact Scope

- 受影响模块：
- 受影响运行路径：

## Root Cause / Main Reasoning

<根因或主要判断依据>

## Proposed Handling

<建议修复、澄清或关闭方式>

## Risks And Rollback

- 风险点：
- 若修复，回滚方式：

## Draft Reply

<建议回复内容>
```

## Allowed Auto-Actions

- 拉取 issue 详情与评论
- 阅读相关代码、配置、脚本、工作流和文档
- 生成分析文档

## Actions Requiring Confirmation

- 添加或修改标签
- 在 issue 下评论
- 关闭 issue
- 开始修复 issue
