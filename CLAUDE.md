# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目定位

这是一个 Claude Code 的 **plugin 项目**，核心是 `dispatching-parallel-subagents` skill（并行派遣子代理的规范框架）。项目以 Markdown 文档为主要产出，没有构建工具、测试框架或 lint 流程。Plugin 通过 `.claude-plugin/plugin.json` 声明，可被 Claude Code 通过 `--plugin-dir` 加载。

## 文件结构约定

采用**渐进式披露（Progressive Disclosure）**结构：

```
skills/<skill-name>/
├── SKILL.md              # 精简版核心规范，包含定位、职责、准入条件、原则
├── DESIGN_NOTES.md       # 设计结论备忘，供跨会话衔接
├── references/
│   ├── prompt-templates.md   # 可直接复制使用的 Prompt 模板
│   ├── quick-reference.md    # 快速参考表与验收清单
│   └── failure-handling.md   # 失败处理与常见错误详解
└── examples/
    └── real-example.md       # 完整实战示例
```

新增 skill 时应遵循此结构。`SKILL.md` 必须保持精简，不重复展开细节。

## 核心设计决策（必须理解）

### 1. Skill 是执行标准，不是拆分决策器

主代理负责判断任务是否可拆（接口锁定、模块独立、上下文可隔离）。本 skill 只负责拆分**之后**的执行规范（prompt 结构、返回格式、聚合策略）。

### 2. 唯一准入条件：上下文独立性

并行拆分的唯一准入条件是子任务之间**不需要交换中间结果**且**不需要继承主会话历史**。不满足时保留在主会话串行执行。

### 3. 两种子代理类型

| 类型 | 任务 | 输入 | 返回 |
|------|------|------|------|
| **判定型** | 独立查询验证（存在性检查、匹配提取） | 关键词 + 判定标准 | 是/否、行号、无匹配（一句话，无解释） |
| **实现型** | 接口已锁定的独立模块编码 | 接口契约 + 验收标准 + 约束清单 | DONE/ERROR/BLOCKED + 产物 + 自测结果 |

### 4. 不可违背的核心原则

1. **子代理之间不得交换中间结果** — 破坏上下文隔离，token 损失超过并行收益
2. **子代理不得继承主会话历史** — 失去并行拆分的意义

### 5. 规范 ≠ 限制

- 核心原则使用强硬措辞（"不得"）
- 推荐性规范使用柔性措辞（"建议""可以调整"），当与判断冲突时，判断优先
- 用户说"先讨论""你觉得呢"是邀请讨论，不是授权执行

### 6. 失败处理策略

子代理失败 → 结束并派遣全新子代理（最小上下文，不继承纠缠历史）→ 仍失败则**停止并行，在主会话串行处理**。强行继续派遣只会增加 overhead。

## 编辑规范时的注意事项

- **避免"机械式软化/硬化"**：调整措辞时应结合内容本质判断，不是把"不得"全改成"建议"
- **用词一致性**：核心原则用"不得"，推荐性规范用"建议"
- **不重复**：`SKILL.md` 只放核心内容，详细参考放在 `references/` 目录
- 修改前先完整阅读 `DESIGN_NOTES.md`，了解设计背景和跨会话结论

## 版本控制

Git 远程地址：`git@github.com:Pulck/ColickTools.git`

常用命令（已配置自动权限）：
- `git add -A && git commit -m "..."` — 提交变更
- `git push origin main` — 推送到远程
