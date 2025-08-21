# SDK and Transport Layer

The SDK entry point `sdk.mjs` exports a `query` function that orchestrates an interactive session with the Claude Code CLI. The function accepts a prompt (string or streaming iterable) and an options object. Internally it spawns `cli.js` as a child process using the `ProcessTransport` abstraction, piping JSON messages between processes.

Key utilities in the SDK include:

* **Stream** – an async iterator implementation that queues messages and supports `done` and `error` signals.
* **createAbortController** – constructs abort controllers with raised listener limits to support many concurrent hooks.
* **ProcessTransport** – wraps `child_process.spawn`, forwarding stdin/stdout and encoding messages as newline-delimited JSON.

The `query` function sets up environment variables and determines the executable (`node` or `bun`). It also configures permission mode, allowed/disallowed tools, model selection, and optional custom system prompts before spawning the transport. If the prompt is an async iterator, the SDK operates in streaming mode and feeds user messages to the transport incrementally.

Returned from `query` is a `Query` object that implements `AsyncGenerator<SDKMessage, void>`. It yields structured messages representing system, user, assistant, or result events. The object exposes helper methods:

* `interrupt()` – cancel a streaming query
* `setPermissionMode()` – adjust permission enforcement while streaming

The `Query` class also handles control requests from the CLI, such as asking whether a tool may be executed or invoking hook callbacks supplied in the options. Messages are processed through an internal `Stream` instance and surfaced to consumers via async iteration.

