# openclaw-homelab-blueprint

A vendor-neutral blueprint for running a **multi-agent assistant stack at home**: one gateway, many
narrowly-scoped agents, per-agent model cascades, least-privilege tool access, containerized deployment,
and an operations discipline (backups, dry-run-first changes, secret hygiene).

> **Status: private staging, not published. License: Apache-2.0 (see `LICENSE`).** Everything here is generic and synthetic. It contains no
> live configuration, prompts, memory, credentials, hostnames, IPs, IDs or logs from any real deployment.
> It is a design pattern plus examples, not a copy of anyone's system.

## What's inside

| Path | Purpose |
|---|---|
| `docs/architecture.md` | Reference architecture: gateway, agents, channels, tools, storage |
| `docs/agent-roster-pattern.md` | How to carve a roster into roles and write scoped agent briefs |
| `docs/model-cascades.md` | Cheap-first, escalate-on-failure model routing pattern |
| `docs/tool-allowlist-pattern.md` | Least-privilege tool/MCP access per agent |
| `docs/operations-playbook.md` | Change safety: inspect, back up, dry-run, verify, roll back |
| `examples/config/gateway.example.json` | Sanitized example configuration (placeholders only) |
| `schema/gateway-config.schema.json` | JSON Schema for the example config shape |
| `examples/deploy/compose.example.yaml` | Generic container deployment example |
| `SECURITY.md` | Threat model and publication hygiene |
| `LICENSE`, `NOTICE` | Apache License 2.0 and attribution notice |

## Design principles

1. **Small agents, narrow jobs.** One role per agent; escalate by handoff, not by widening scope.
2. **Least privilege.** Each agent gets an explicit tool allowlist; destructive tools need approval.
3. **Secrets never in config.** Config references secret *names*; values come from a secret manager or runtime env.
4. **Dry-run first, back up before writes, verify after.**
5. **Cheap model first, escalate on evidence.**
6. **Everything reproducible from files**: config, compose, and docs live in git; state and secrets do not.

## Quick start (conceptual)

1. Copy `examples/config/gateway.example.json` to a private location and fill in placeholders.
2. Validate: `python3 -c "import json,sys;json.load(open('gateway.json'))"` (or any JSON Schema validator against `schema/`).
3. Adapt `examples/deploy/compose.example.yaml`; supply secrets via your secret manager, not the file.

This repo does not ship the gateway software; point to your chosen runtime's own documentation.

## License

Apache License 2.0 — see [`LICENSE`](LICENSE) and [`NOTICE`](NOTICE). Chosen for its explicit patent grant,
which suits infrastructure patterns and example configuration. Docs may optionally be dual-licensed CC BY 4.0 later.
Copyright holder of record: "Greysave contributors" (see `NOTICE`).
