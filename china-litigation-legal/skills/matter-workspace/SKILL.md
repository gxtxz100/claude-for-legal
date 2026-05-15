---
name: matter-workspace
description: 管理案件工作空间 — 创建、列表、切换、关闭或分离活跃案件工作空间，适用于多委托人执业（律所律师）。企业法务一般无需此功能。
argument-hint: "new [案件标识] | list | switch [案件标识] | close [案件标识] | none"
---

# /matter-workspace

管理多委托人执业环境中的案件工作空间。

## 命令

- `new [标识]` — 创建新案件工作空间并切换至该案件
- `list` — 列出所有案件工作空间及当前活跃案件
- `switch [标识]` — 切换活跃案件
- `close [标识]` — 关闭案件（归档，不删除）
- `none` — 清除活跃案件，返回执业层面背景

## 工作空间路径

案件工作空间位于：
`~/.claude/plugins/config/claude-for-legal/china-litigation-legal/matters/[标识]/`

每个工作空间包含：
- `matter.md` — 案件主文件
- `history.md` — 事件日志
- `evidence/` — 证据目录（可选）
- `documents/` — 文书草稿（可选）

## 保密隔离

跨案件背景关闭时（默认），处理案件A的技能不会读取案件B的文件。在律所执业中，委托人A和委托人B的案件材料必须完全隔离。

若需要跨案件比较（例如，汇总报告），使用 `/portfolio-status` — 它仅读取 `_log.yaml` 中的结构化行，不读取案件详情。

## 激活案件工作空间后

所有技能将使用当前活跃案件的背景运行：
- 读取 `matter.md` 获取案件事实
- 输出写入案件文件夹
- 引用该案件的诉讼时效和期限数据

## 本技能不做的事

- **合并不同委托人的案件数据。** 每个工作空间严格隔离。
- **删除案件记录。** 使用 `close` 标注为结案；使用 `/matter-close` 正式结案。
