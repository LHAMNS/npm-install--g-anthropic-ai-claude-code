# Shell and Process Tools

The CLI integrates tightly with the local shell, allowing the agent to run commands, capture output and manage long-running processes.

## Bash
Executes a command string using the system shell. Inputs allow:

- `command` – the literal shell command
- `timeout` – optional milliseconds before termination (max 600000)
- `description` – a concise explanation for the user
- `run_in_background` – run without blocking and retrieve output later
- `sandbox` – restrict writes and network access for safer inspection
- `shellExecutable` – override the default shell (primarily for tests)

The command description is used to present context to the user when permission is requested.

## BashOutput
Retrieves buffered stdout from a background shell created with `run_in_background`. It requires the `bash_id` of the process and can optionally filter lines with a regular expression. Non-matching lines are discarded once read, preventing indefinite accumulation.

## KillShell
Terminates a background shell by its `shell_id`. This is necessary to clean up stray processes that were started but no longer needed.

## NotebookEdit
Provides structured editing of Jupyter notebook files. It accepts a `notebook_path`, optional `cell_id`, new `source` code, cell type (`code` or `markdown`), and an `edit_mode` of `replace`, `insert`, or `delete`. The tool ensures notebook JSON is updated correctly without manual manipulation.

These process-oriented tools give Claude Code the ability to explore a codebase, execute tests or linters, and incorporate results back into the conversation while keeping user approval and safety at the forefront.

