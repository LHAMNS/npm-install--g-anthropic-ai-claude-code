# Claude Code Overview

@anthropic-ai/claude-code is a terminal-based coding assistant published as an npm package. After a global install, the `claude` command launches an interactive agent that understands a repository, edits files and executes commands through natural language.

The package is distributed with a small set of top-level assets:

- `cli.js` – entry point for the CLI interface
- `sdk.mjs` and TypeScript definition files for programmatic access
- `vendor/` and `node_modules/` directories containing bundled dependencies
- `yoga.wasm` for layout rendering

Running `npm install -g @anthropic-ai/claude-code` adds the command to the global path and exposes the exported APIs for Node.js applications.

The project exposes a CLI and an SDK. The CLI renders a terminal UI, displays messages, and invokes tools to fulfill user requests. The SDK provides a `query` function that streams messages from a spawned CLI process and enables external programs to integrate Claude Code behavior.

Agent sessions begin with a concise system prompt identifying the tool: "You are Claude Code, Anthropic's official CLI for Claude." The agent can read and modify files, run shell commands, fetch web content, search documentation, and interact with Model Context Protocol (MCP) servers.

Each tool invocation and major event flows through a permission and hook system that allows customization or auditing. The package defaults to Node 18+, includes zero direct dependencies, and relies on optional `sharp` builds per platform for image manipulation tasks.

