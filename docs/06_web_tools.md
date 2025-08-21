# Web and Research Tools

Claude Code can reach beyond the local repository using two web-oriented utilities.

## WebFetch
Fetches a URL, converts HTML to markdown and applies a small model to answer a prompt about the page. Inputs:

- `url` – fully formed HTTP(S) address, automatically upgraded to HTTPS when possible
- `prompt` – instructions describing what information to extract from the fetched content

Responses may be summarized when content is large. The tool maintains a 15‑minute cache and informs the user if the request redirects to a different host. The CLI warns that MCP-provided fetch tools should be preferred when available.

## WebSearch
Performs web searches to provide up‑to‑date information. Options include `allowed_domains` and `blocked_domains` for domain filtering. Results come back as structured search blocks and may be constrained to US availability. When building queries, the agent accounts for the current date to ensure timely results.

These tools enrich the agent's capabilities by providing access to external knowledge and content analysis while respecting domain restrictions and user oversight.

