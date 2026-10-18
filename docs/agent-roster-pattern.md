# Agent roster pattern

Group agents by function, not by person:

| Role family | Examples (generic) | Typical tools |
|---|---|---|
| Coordinator | `main` | session spawn, messaging |
| Infra / ops | `ops`, `net`, `storage` | container API, dns, backups (approval-gated) |
| Domain helpers | `finance`, `fitness`, `travel`, `career` | domain APIs, files |
| Specialist reviewers | `legal-reader`, `security` | read-only file access |

## Writing a brief (AGENTS.md-style)
1. **Role** in one sentence.
2. **Inputs/outputs**: where it reads handoffs, where it writes artifacts.
3. **State files** it owns (and that nobody else edits).
4. **Hard limits**: what it must never do (publish, delete, spend, message third parties).
5. **Escalation**: who to hand off to, and the handoff file format.

Keep briefs short; put procedures in skills. Never put credentials, personal data or real hostnames in a brief.
Use a handoff convention (a shared folder with frontmatter-tagged files: `status: new|processed`) so agents
coordinate through auditable files rather than hidden chat context.
