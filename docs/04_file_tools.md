# File Manipulation Tools

Claude Code offers several tools for inspecting and mutating files in a repository. These tools operate on absolute paths and expect the caller to read files before attempting writes.

## FileRead
Reads a file from the local filesystem. It requires a `file_path` and optionally supports `offset` and `limit` for paginated access when files are too large to load at once.

## FileWrite
Writes content to an absolute `file_path`. If the file exists it will be overwritten. The CLI emphasizes that existing files should be edited rather than replaced and warns against creating documentation unless explicitly requested by the user.

## FileEdit
Replaces a single string within a file. Inputs include `file_path`, `old_string`, `new_string`, and optional `replace_all` to change every occurrence. The operation fails if `old_string` does not match the file's current contents exactly or if `old_string` and `new_string` are identical.

## FileMultiEdit
Applies a sequence of edits to one file atomically. Each edit specifies `old_string`, `new_string`, and optional `replace_all`. All edits must succeed or none are applied. The bundled instructions stress reading the file first and ensuring earlier edits do not interfere with later ones.

## Glob and Grep
`Glob` searches for files matching a pattern optionally rooted at a `path`. `Grep` leverages ripgrep-style options including `--glob` filters, context lines (`-A`, `-B`, `-C`), line numbers (`-n`), case insensitivity (`-i`), file type constraints, and output modes (`content`, `files_with_matches`, `count`). Both tools support `head_limit` to cap results.

## Ls
Lists the contents of a directory at an absolute `path`, with optional glob patterns to ignore. This is used to understand project structure before editing.

Together, these tools enable the agent to analyze and modify codebases while maintaining strict validation to prevent accidental corruption or unauthorized writes.

