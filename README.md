# Unofficial EGM Implement

An unofficial Claude Code skill for implementing approved [Elephant-Goldfish Model (EGM)](https://github.com/google/elephant-goldfish-model) design docs. Not affiliated with the EGM project.

| Skill | What it does |
|---|---|
| [egm-implement](egm-implement/SKILL.md) | Implements an approved [Elephant-Goldfish Model](https://github.com/google/elephant-goldfish-model) design doc in a fresh session: plans work packages, delegates them to subagents, runs the Verification Plan, and finishes with a zero-context review against the spec. |

## Install

Copy a skill folder into `~/.claude/skills/` (user-wide) or `<project>/.claude/skills/` (one project), then start a new session:

```text
/egm-implement docs/designs/<FEATURE>.md
```
