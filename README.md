# netcafe skills

An [Agent Skill](https://agentskills.io/) that teaches your agent when to reach for
deterministic tools instead of estimating over a table.

```
/plugin marketplace add mario03690/netcafe-skills
/plugin install netcafe@netcafe
```

Or drop `plugins/netcafe/skills/netcafe/SKILL.md` into `~/.claude/skills/netcafe/SKILL.md`.
The file follows the open Agent Skills standard, so it also works in other tools that read
`SKILL.md`.

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
