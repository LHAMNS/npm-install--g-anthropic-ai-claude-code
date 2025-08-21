# Permissions and Hooks

Claude Code enforces a permission system around tool usage. The SDK's options allow specifying a `permissionMode`:

- `default` – request approval for actions that may modify the system
- `acceptEdits` – automatically apply file edits after preview
- `bypassPermissions` – execute without interactive confirmation
- `plan` – produce a plan for review without executing actions

A `canUseTool` callback may be provided to programmatically allow, deny, or ask for approval before executing a tool. The callback returns a `PermissionResult` that can update the tool input or deny the request with a message.

Beyond permissions, the SDK defines a rich hook system. The constant `HOOK_EVENTS` enumerates trigger points such as `PreToolUse`, `PostToolUse`, `Notification`, `UserPromptSubmit`, `SessionStart`, `SessionEnd`, `Stop`, `SubagentStop`, and `PreCompact`. Each hook receives structured input describing the current session and tool invocation.

Hooks are registered by event name with optional pattern matchers. When a matching event occurs, the CLI sends a `hook_callback` control request and waits for the provided function's asynchronous response. Hook outputs can influence the session by adding context, suppressing output, or stopping execution.

These mechanisms let integrators audit actions, enforce policy, or extend Claude Code with custom behaviors while maintaining a tight approval loop around potentially destructive operations.

