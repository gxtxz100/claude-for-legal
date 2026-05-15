# china-litigation-legal

**中国诉讼与争议解决实务助手** — 为中国律师事务所律师（诉讼/非诉）和企业法务设计的 Claude Code 插件。

覆盖中国法律框架下的全流程诉讼和争议解决工作：民事/商事诉讼、行政复议/诉讼、国内外仲裁（CIETAC/BAC/SHIAC等）、诉讼时效管理和法律文书起草。

> **重要提示：** 本插件的所有输出均为供律师审阅的初稿——不是法律意见，不是最终法律结论，不能替代执业律师。插件提供研究、组织和结构化支持，最终法律判断和专业责任由使用本插件的律师承担。

---

## 快速开始

```bash
# 安装插件
/plugin install china-litigation-legal

# 重启 Claude Code 后，运行冷启动访谈（必须首先完成）
/china-litigation-legal:cold-start-interview
```

**必须先运行冷启动访谈。** 访谈写入实践档案，插件中的每条命令都从该档案读取。跳过设置是获得通用输出而非定制输出的最常见原因。访谈大约需要10-15分钟（或2分钟快速模式）。

---

## 技能与命令参考

| 命令 | 技能 | 功能描述 |
|---|---|---|
| `/china-litigation-legal:cold-start-interview` | cold-start-interview | 冷启动访谈——按角色（律所/法务/个人执业）建立实践档案 |
| `/china-litigation-legal:matter-intake` | matter-intake | 受理新案件——写入matter.md和history.md，追加至台账 |
| `/china-litigation-legal:matter-briefing` | matter-briefing | 案件深度简报——适合合伙人例会或客户更新前准备 |
| `/china-litigation-legal:matter-update` | matter-update | 追加案件进展至历史记录并刷新台账 |
| `/china-litigation-legal:matter-close` | matter-close | 结案归档——记录结果、最终损失和经验教训 |
| `/china-litigation-legal:matter-workspace` | matter-workspace | 管理案件工作空间（多委托人律所执业） |
| `/china-litigation-legal:portfolio-status` | portfolio-status | 案件组合状态汇总——风险分布、期限预警、停滞案件 |
| `/china-litigation-legal:legal-doc-drafter` | legal-doc-drafter | 起草法律文书——起诉状/答辩状/代理词/律师函等 |
| `/china-litigation-legal:arbitration-management` | arbitration-management | 仲裁管理——条款分析、机构选择、程序跟踪 |
| `/china-litigation-legal:statute-of-limitations` | statute-of-limitations | 诉讼时效管理——计算、中断/中止追踪、到期预警 |
| `/china-litigation-legal:chronology` | chronology | 事实时间轴——从材料中提取有日期的事件，标注重要性 |
| `/china-litigation-legal:claim-analysis` | claim-analysis | 诉请/抗辩分析——分析来函主张或评估我方诉请可行性 |
| `/china-litigation-legal:evidence-management` | evidence-management | 证据管理——证据目录、质量评级、缺口分析 |
| `/china-litigation-legal:administrative-litigation` | administrative-litigation | 行政复议/行政诉讼——期限管理、申请书/起诉状起草 |
| `/china-litigation-legal:customize` | customize | 自定义修改实践档案中的单项设置 |
| 定期 | case-deadline-watcher（代理人）| 每周监控期限和诉讼时效，推送警报 |

---

## 与美国版本的核心区别

本插件针对中国法律体系从头设计，不是美国版插件的翻译。主要区别：

| 美国诉讼概念 | 中国对应 | 本插件处理方式 |
|---|---|---|
| Attorney Work Product | 律师职业秘密（保密标注适用，但无程序豁免）| 使用中国法律下的保密标注，明确说明局限性 |
| Discovery/eDiscovery | 无强制证据开示 | `/evidence-management` 技能覆盖中国举证规则 |
| Deposition | 无庭前证人证词程序 | 替换为庭审前证人安排 |
| Privilege Log | 无直接对应 | 替换为律师工作文件目录 |
| Subpoena | 法院调查令（机制不同）| `/evidence-management` 覆盖证据保全申请 |
| CourtListener | 中国裁判文书网、北大法宝 | `.mcp.json` 说明中国数据库接入方式 |
| Bar Exam (MBE) | 法考（国家统一法律职业资格考试）| `cold-start-interview` 询问法考状态 |
| IRAC格式 | 中国法律文书规范（无IRAC）| `legal-doc-drafter` 使用中国文书格式 |
| Statute of Limitations | 诉讼时效（《民法典》第188条）| 专门技能 `statute-of-limitations` |
| Federal Court System | 基层/中级/高级/最高人民法院 | `matter-intake` 和 `chronology` 使用中国法院体系 |
| Arbitration (AAA/JAMS) | CIETAC/BAC/SHIAC 等 | `arbitration-management` 覆盖中国仲裁机构 |

---

## 中国法律数据库说明

目前尚无中国主流法律数据库的官方 MCP 连接器。建议通过以下途径访问：

| 数据库 | 网址 | 内容 |
|---|---|---|
| 中国裁判文书网 | wenshu.court.gov.cn | 全国法院判决书（官方）|
| 国家法律法规数据库 | flk.npc.gov.cn | 现行法律法规（官方）|
| 北大法宝 | pkulaw.com | 法律法规、案例、期刊（付费）|
| 威科先行 | wklawchina.com | 法律法规、案例（付费）|

若上述数据库无法通过 MCP 连接，插件会在每次引用法律条文时注明 `[训练知识 — 请核实]`，提示律师对照权威来源核实。

---

## 实践档案配置路径

用户实践档案：`~/.claude/plugins/config/claude-for-legal/china-litigation-legal/CLAUDE.md`

案件台账：`~/.claude/plugins/config/claude-for-legal/china-litigation-legal/matters/_log.yaml`

以上文件是纯文本，可直接编辑。小改动直接编辑文件；大改动运行 `/china-litigation-legal:cold-start-interview --redo`。

---

## 贡献

所有内容均为 Markdown 和 JSON。Fork、编辑、PR 均欢迎。

新技能：在 `skills/` 下添加技能文件夹，按现有技能的 frontmatter 格式填写。

---

## 许可证

Apache License, Version 2.0。
