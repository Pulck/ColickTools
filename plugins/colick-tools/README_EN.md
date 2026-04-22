# Claude Code Plugin — Skill Collection

Provides multiple Claude Code skills covering parallel subagent dispatching and honest execution standards.

## Overview

This plugin contains two skills:

### dispatching-parallel-subagents

Defines execution standards for dispatching parallel subagents after the main agent decides a task can be split:
- Admission criteria: context independence
- Subagent types: judgment-type and implementation-type
- Non-negotiable principles: subagents must not exchange intermediate results or inherit main session history
- Result aggregation strategies
- Failure handling

Trigger phrases: "dispatch parallel subagents", "拆分任务", "并行派遣子代理", etc.

### honest-execution

Global behavioral standard for honest execution across all tasks:
- Wu Yi (毋意) — No unfounded speculation
- Wu Bi (毋必) — No dogmatic absolutism
- Wu Gu (毋固) — No stubborn self-righteousness
- Wu Wo (毋我) — No presumptuous substitution of judgment
- Jing Shi (敬事) — No shirking of verification responsibility

Trigger phrases: "诚实执行", "不要偷工减料", "实事求是", "verification", "transparency", etc.

## Installation

```bash
claude --plugin-dir /path/to/this/repo
```

Or add to your Claude Code plugins directory for automatic loading.

## Commands

### /fill-survey

Fill out the AI self-assessment survey, reviewing the session execution and outputting to a specified folder.

```bash
/fill-survey ./my-surveys
```

- Honest self-assessment based on the survey template
- Automatic desensitization of sensitive information
- Output file: `ai-self-assessment-{date}.md`

## Making honest-execution Always-On

By default, honest-execution only triggers when the user explicitly mentions related keywords. To make it effective during everyday coding tasks, append the following to your project's `CLAUDE.md` (or global `~/.claude/CLAUDE.md`):

```markdown
## Behavioral Anchor

- Wu Yi — No unfounded speculation. Do not claim unverified facts; compilation, testing, etc. are only reported after execution.
- Wu Bi — No dogmatic absolutism. State verification boundaries; avoid absolute phrasing like "definitely" or "certainly".
- Wu Gu — No stubborn self-righteousness. Correct and confess immediately when judgment contradicts reality.
- Wu Wo — No presumptuous substitution of judgment. Inform the user and obtain consent before major execution deviations.
- Jing Shi — No shirking of responsibility. Do not push verification duties onto the user due to difficulty.
```

This lightweight anchor loads automatically in every session without consuming significant context.

## File Structure

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

## License

MIT
