# Reference architecture

```
 chat channels / web UI
          │
      ┌───▼────┐   routing rules (binding: channel/room → agent)
      │ Gateway│──────────────────────────────┐
      └───┬────┘                              │
          │ sessions, queueing, approvals     │
   ┌──────▼──────┐  ┌───────────┐  ┌──────────▼───┐
   │ Agent: ops  │  │ Agent: …  │  │ Agent: helper │   one role each
   └──────┬──────┘  └─────┬─────┘  └──────┬───────┘
          │ tool allowlist per agent      │
   ┌──────▼───────────────────────────────▼──────┐
   │ Tools / MCP servers (mail, files, home, …)  │
   └──────┬───────────────────────────────────────┘
          │
   Private network services (reverse proxy + auth in front of anything exposed)
```

## Components
- **Gateway**: single entry point; owns auth, channel adapters, session lifecycle, queueing/debounce, and approval prompts.
- **Agents**: each has a workspace directory (brief, skills, scratch state) and a model cascade.
- **Skills**: markdown playbooks an agent loads on demand; versioned in git.
- **Tools/MCP**: external capabilities exposed through an allowlist.
- **Scheduler**: cron-style jobs for periodic agent runs, with a concurrency cap and session retention.
- **Storage**: workspace files (git), session store (private), secrets (secret manager).

## Deployment boundaries
- Expose only the reverse proxy. Put SSO/2FA in front of every non-public app; default-deny.
- Keep the gateway bound to loopback or an internal network; reach it through the proxy or a VPN.
- Separate networks/VLANs for IoT, VPN-egress workloads and the management plane where possible.
