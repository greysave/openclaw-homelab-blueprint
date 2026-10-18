# Tool / MCP allowlist pattern

- Default **deny**. Each agent lists exactly the tools it may call.
- Split read vs. write tools; require human approval for write/delete/send and for anything outward-facing.
- Run MCP servers on an internal network with their own auth; never expose them through the public proxy.
- Pin server images by digest; review tool descriptions as untrusted input (prompt-injection surface).
- Log tool calls to a private audit log (see SECURITY.md: logs are never committed).
