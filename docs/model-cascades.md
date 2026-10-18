# Model cascades

Define per-agent ordered model lists: `primary` (cheap/fast) → `escalation` (stronger) → `fallback` (different provider).

- Escalate on **evidence**: failed validation, tool error loops, low-confidence flags, or explicit task class (e.g. "legal review").
- Cap escalation per task and log the reason; review monthly for agents that always escalate (their primary is wrong).
- Keep provider credentials in auth profiles/secret stores; the cascade config only references profile names.
- Prefer providers/plans whose terms allow your usage pattern. Routing a consumer subscription through a local
  shim can violate terms of service — read them first, and prefer official API access for automation.
