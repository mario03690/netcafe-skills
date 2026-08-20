# netcafe skills

An [Agent Skill](https://agentskills.io/) that teaches your agent when to reach for
deterministic tools instead of estimating over a table.

One skill, one source of truth, four ways to install it.

**Claude Code**

```
/plugin marketplace add mario03690/netcafe-skills
/plugin install netcafe@netcafe
```

**Codex** — the repo ships `.codex-plugin/plugin.json` pointing at `./skills/`.

**Gemini CLI** — `.gemini/commands/netcafe.toml` adds a `/netcafe` command.

**OpenCode** — `.opencode/skills` is a symlink to `./skills`, so the skill-driven
execution model picks it up directly.

**Anything else** — copy `skills/netcafe/SKILL.md` to `~/.claude/skills/netcafe/SKILL.md`
(or your tool's skills directory). The file follows the open
[Agent Skills](https://agentskills.io/) standard, which around 40 products now read.

`.opencode/skills` is a symlink rather than a copy on purpose: a stale copy of a skill is
worse than no skill, because the agent trusts it.

## The part that is not another API wrapper

When the same data job comes back for the third or fourth time, the skill stops hand-running
it and freezes the sequence into a **production line** that runs on the server on a schedule —
including when your machine is off. Every run leaves a work order with each step's arithmetic
proof; runs whose checks fail are not billed.

Live examples, no signup, real run history:
[reachability](https://ainetcafe.com/line/pl_8dc2f234f9d7) ·
[dirty-data reconciliation](https://ainetcafe.com/line/pl_2f4982aead1f) ·
[HS classification](https://ainetcafe.com/line/pl_aa842f5afab5)

The division of labour is the point: **your agent designs the flow** — only it has seen your
data and knows its quirks. **The server keeps running it** — on time, with a receipt.

## What it covers

| Job | Why not do it inline |
| --- | --- |
| Reconcile a bank statement against a ledger with **no shared reference number** | Amount + date-window + fuzzy-reference matching, 1:N instalments and N:1 combined payments, and it refuses to guess when evidence is thin |
| Compare two tables on a key | Surfaces `case_drift` and `duplicate_keys` — the usual reason two "identical" exports disagree |
| Reconcile two ledgers on a shared key | Integer cents, so `0.1 + 0.2` never invents a phantom difference; `(100.00)` reads as negative |
| Find duplicate companies | Tax-ID checksums cross-checked against name similarity; never auto-merges, and flags look-alikes that are provably different |
| Read/write `.xlsx` | Dates come back `YYYY-MM-DD`, not `45123`; `007` stays `007`; merged cells reported, not silently filled |
| US HS/HTS codes | Official USITC schedule; returns candidate chapters with reasons rather than guessing a code |
| Mainland-China reachability | Measured from a real mainland network, not inferred from an IP range |

Every result involving counts or money carries an arithmetic self-check computed in code.
No model call inside, so the same input always produces the same output.

No API key needed — anonymous calls draw on a free quota.

Full tool list: <https://ainetcafe.com/mcp.html>

## License

MIT
