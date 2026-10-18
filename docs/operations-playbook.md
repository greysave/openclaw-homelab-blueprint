# Operations playbook

1. **Inspect** the current state read-only. Record what you saw.
2. **Back up** the specific file/DB you will touch (timestamped copy outside the repo).
3. **Dry-run** or diff. Prefer additive changes; avoid whole-file replacement of shared configs.
4. **Apply** the smallest change; one concern per change.
5. **Verify** with an independent check (health endpoint, query, test), not just "command exited 0".
6. **Roll back** path written down before you start.
7. **Document**: runbook entry with date, reason, rollback. No secrets in the entry.

Recurring checks: backup restore test, dependency update notifications, uptime monitors with alerting,
exposure review of the reverse proxy (who can reach what).
