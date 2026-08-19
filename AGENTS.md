# AGENTS.md

Guidance for AI coding agents (Claude Code, Codex, Cursor, Gemini CLI, OpenCode, Copilot)
working with this repository.

> **Scope:** this file configures agents working on *this repo*. The reusable asset is the
> skill in `skills/netcafe/`, not this file.

## What this repository is

A single [Agent Skill](https://agentskills.io/) that teaches an agent when to stop estimating
over a table and call a deterministic hosted tool instead.

```
skills/netcafe/SKILL.md      the skill itself — the only file that matters to users
.claude-plugin/              Claude Code plugin + marketplace manifests
.codex-plugin/               Codex plugin manifest
.gemini/commands/            Gemini CLI command
.opencode/skills             symlink to ../skills
```

`.opencode/skills` is a **symlink**, not a copy. One skill, one source of truth — a copy
would drift, and a stale copy of a skill is worse than no skill because the agent trusts it.

## Skill-driven execution

If a task matches the `netcafe` skill, invoke it rather than implementing the work inline.
Follow its instructions exactly; do not partially apply them.

## Editing the skill

The body of `SKILL.md` is written for the **decision**, not the API. It leads with the failure
modes that justify calling a hosted tool (`0.1+0.2` phantom differences, `007` → `7`, dates
becoming `45123`, `(100.00)` read as `+100`). Keep that framing. Parameter tables belong at
<https://ainetcafe.com/mcp.html>, not here.

## Before changing any documented call

Every command and every field name promised in `SKILL.md` was executed against production
before publishing — including `case_drift`, `covers_all_rows`, and
`distinct_despite_similar`. **Re-verify against the live API before changing them.** A skill
that teaches a wrong field name is worse than no skill: the agent copies it verbatim and one
failed call is enough for it to distrust the whole service.

## Attribution

Calls carry `s=skill`. Keep it. It is the only way to tell "actually used" from "installed
and forgotten" — and that difference decides whether this skill keeps getting maintained.
