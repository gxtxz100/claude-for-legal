# 案件文件夹

每个案件在此目录下有独立子文件夹，由 `/china-litigation-legal:matter-intake` 自动创建。

```
matters/
  _log.yaml                 # 案件台账（结构化数据，自动维护）
  _README.md                # 本文件
  <案件标识>/
    matter.md               # 案件主文件（受理时写入，持续更新）
    history.md              # 事件日志（追加式，最新在上）
    evidence/               # 证据目录（可选）
    documents/              # 文书草稿（可选）
```

**案件标识规则：** 小写汉语拼音缩写或关键词、连字符、年份。例：
- `zhang-san-hetong-2026` （张三合同纠纷2026）
- `abc-laodong-2026`（ABC公司劳动争议2026）
- `cietac-mouyin-2026`（贸仲某引进案2026）

**不要手动创建子文件夹。** 运行 `/china-litigation-legal:matter-intake` 完成规范化受理。
