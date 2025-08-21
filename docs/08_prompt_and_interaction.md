# System Prompts and Interaction Flow

Upon startup, the CLI constructs a system prompt identifying its role: *"You are Claude Code, Anthropic's official CLI for Claude."* This instruction anchors the agent's behavior and is supplied to the underlying model with each request.

Consumers of the SDK may customize prompting through two options:

- `customSystemPrompt` – replaces the default instructions entirely
- `appendSystemPrompt` – appends additional guidance while preserving the baseline rules

For streaming interactions, user messages can be supplied as an `AsyncIterable`. The `Query` object exposes `interrupt()` to cancel and `setPermissionMode()` to adjust safety levels mid-conversation. When plain strings are used, the entire prompt is sent in one batch.

The CLI maintains conversational context, rendering a terminal UI with real-time updates. It can detect whether new messages start a different topic and update the terminal title accordingly. User input is parsed into tool requests, which are executed only after permissions are granted or policy hooks approve them.

Session transcripts are written to disk, enabling resume capability via the `resume` option. Additional directories may be supplied to expand the agent's view beyond the current working directory.

