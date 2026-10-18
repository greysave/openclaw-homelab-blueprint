# Security

## Threat model (short)
Prompt injection via tool output/web content; credential leakage via config, logs or chat; over-privileged tools;
exposed admin surfaces; supply-chain drift of images and packages.

## Rules for this repository
- Placeholders only: `example.invalid`, `*-placeholder`, `secret:NAME` references. Never real hostnames, IPs, IDs, emails or tokens.
- Never commit: live configs and their backups, `.env` files, session/memory stores, agent private prompts, logs,
  database exports, user data, vendor/customer information.
- Run a secret scanner (e.g. gitleaks/trufflehog) on every commit and in CI; rotate anything that is ever exposed.

## Hardening checklist for adopters
- Gateway on loopback/internal network; auth mode never `none` outside a lab.
- Default-deny tool allowlists; approval for outward-facing and destructive actions.
- Digest-pinned images, non-root, read-only filesystems, dropped capabilities.
- SSO/2FA at the reverse proxy; MCP servers never publicly exposed.
- Tested backups and a written rollback for every change.

## Reporting
Report vulnerabilities privately through the hosting platform's private security advisory feature; do not open public issues for them.
