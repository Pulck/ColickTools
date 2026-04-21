# Dispatching Parallel Subagents

Claude Code plugin providing execution standards and safety framework for dispatching parallel subagents.

## Overview

This plugin contains a single skill — `dispatching-parallel-subagents` — that serves as a reference standard for the main agent after it has decided a task can be split into parallel subtasks. It defines:

- **Admission criteria** for parallel dispatch (context independence is the only gate)
- **Two subagent types**: judgment-type (boolean/enum results) and implementation-type (module coding with locked interfaces)
- **Non-negotiable principles**: subagents must not exchange intermediate results or inherit main session history
- **Aggregation strategies** for merging results back into the main session
- **Failure handling** (retry once with fresh subagent, then fall back to serial execution)

## Installation

```bash
claude --plugin-dir /path/to/this/repo
```

Or add to your Claude Code plugins directory for automatic loading.

## Usage

Once loaded, the skill is automatically triggered when your request contains phrases like:

- "并行派遣子代理"
- "dispatch parallel subagents"
- "拆分任务给多个子代理"
- "让多个子代理同时工作"

## File Structure

```
.claude-plugin/
└── plugin.json                          # Plugin manifest
skills/dispatching-parallel-subagents/
├── SKILL.md                             # Core specification (concise)
├── DESIGN_NOTES.md                      # Design decisions for cross-session continuity
├── references/
│   ├── prompt-templates.md              # Ready-to-use prompt templates
│   ├── quick-reference.md               # Comparison table and checklists
│   └── failure-handling.md              # Common mistakes and anti-patterns
└── examples/
    └── real-example.md                  # End-to-end worked example
```

## License

MIT
