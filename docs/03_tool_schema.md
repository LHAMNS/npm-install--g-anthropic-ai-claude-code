# Tool Input Schemas

Claude Code defines its tool interface through a comprehensive TypeScript declaration file `sdk-tools.d.ts`. This schema enumerates every tool that the agent may invoke along with the expected input fields and validation rules. The tools include:

- **Agent** – delegate tasks to specialized subagents with a short description and prompt.
- **Bash** and **BashOutput** – execute shell commands and read output from background processes, with optional sandbox mode, timeouts and regex filtering.
- **FileEdit** and **FileMultiEdit** – modify existing files via precise string replacement operations, supporting atomic multi-edit batches.
- **FileRead** and **FileWrite** – read or overwrite files using absolute paths. Reads support paging with offsets and limits.
- **Glob**, **Grep**, and **Ls** – search the filesystem using patterns, regular expressions, and directory listing primitives.
- **NotebookEdit** – manipulate Jupyter notebooks by editing or inserting cells.
- **WebFetch** and **WebSearch** – retrieve web content or execute internet searches with domain filtering and post-processing prompts.
- **TodoWrite** – maintain a structured todo list.
- **KillShell**, **ListMcpResources**, **ReadMcpResource**, and generic **Mcp** requests for interacting with Model Context Protocol servers.

Every schema documents required types, optional fields, and special usage notes such as sandboxing rules, maximum lengths, or error conditions. These definitions are auto-generated from JSON Schema sources, ensuring strict validation before tools execute.

