# MCP Integration

Claude Code supports the Model Context Protocol (MCP) for integrating external tools and resources. Through the SDK's `mcpServers` option, clients can register servers of different transport types:

- `stdio` – spawn a local process and communicate over standard I/O
- `sse` – connect to a remote server using Server‑Sent Events
- `http` – issue HTTP requests to a tool endpoint

Each server configuration may include environment variables or headers to satisfy authentication requirements. Once connected, the CLI exposes server-provided tools alongside built-in ones, prefixed with `mcp__` in their names.

The schema file defines helper tools for MCP interaction:

- `ListMcpResources` – enumerates available resources on a server
- `ReadMcpResource` – fetches the content of a specific resource
- Generic `Mcp` requests – send arbitrary payloads to a server-defined procedure

Strict configuration mode (`strictMcpConfig`) enforces that only explicitly declared servers may be used. Hook callbacks and the permission system still apply, letting integrators control which MCP operations are permitted at runtime.

