# Claude Code 插件 — 技能集合

[English](README_EN.md)

提供多个 Claude Code skill，覆盖并行子代理派遣与诚实执行规范。

## 概览

本插件包含两个 skill：

### dispatching-parallel-subagents（并行派遣子代理）

定义主代理拆分任务后，并行派遣子代理的执行规范：
- 准入条件：上下文独立性
- 子代理类型：判定型与实现型
- 不可违背原则：子代理之间不得交换中间结果，不得继承主会话历史
- 结果聚合策略
- 失败处理

触发关键词："并行派遣子代理"、"dispatch parallel subagents"、"拆分任务"等。

### honest-execution（诚实执行）

全局行为准则，覆盖所有任务的诚实执行规范：
- 毋意 — 不凭空臆测
- 毋必 — 不武断绝对
- 毋固 — 不固执己见
- 毋我 — 不自以为是
- 敬事 — 不回避责任

触发关键词："诚实执行"、"不要偷工减料"、"实事求是"、"验证不要偷懒"等。

## 安装

```bash
claude --plugin-dir /path/to/this/repo
```

或添加到 Claude Code 插件目录以自动加载。

## 让 honest-execution 日常生效

honest-execution 默认仅在用户显式提及相关关键词时触发。如需在日常编码任务中自动生效，将以下内容追加到你项目的 `CLAUDE.md`（或全局 `~/.claude/CLAUDE.md`）：

```markdown
## 行为锚点

- 毋意 — 不凭空臆测。未验证的事实不做声称；编译、测试等动作，做了才说。
- 毋必 — 不武断绝对。说明验证边界，避免"肯定""一定"等表述。
- 毋固 — 不固执己见。判断与实际不符时立即修正并坦白。
- 毋我 — 不自以为是。执行路径重大偏离时先告知用户并获得同意。
- 敬事 — 不回避责任。不因困难将验证责任推给用户。
```

这段轻量级锚点会在每个会话中自动加载，不占用显著上下文。

## 文件结构

```
.claude-plugin/
└── plugin.json
skills/
├── dispatching-parallel-subagents/
│   ├── SKILL.md
│   ├── DESIGN_NOTES.md
│   ├── references/
│   │   ├── prompt-templates.md
│   │   ├── quick-reference.md
│   │   └── failure-handling.md
│   └── examples/
│       └── real-example.md
└── honest-execution/
    ├── SKILL.md
    ├── DESIGN_NOTES.md
    ├── references/
    │   ├── common-pitfalls.md
    │   └── quick-reference.md
    └── examples/
        └── real-example.md
```

## 许可证

MIT
