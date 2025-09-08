# git-add-new

A Git plugin that stages new files as pure additions, making them appear as all
green lines (additions) in VS Code and other diff viewers instead of showing as
modified files.

## What it does

When you add a new file to Git normally, diff viewers often show it as
"modified" or may not highlight every line as an addition. This plugin uses the
"empty file trick" to ensure new files appear as pure additions:

1. Temporarily moves your file to a backup
2. Creates an empty file with the same name
3. Stages the empty file (`git add`)
4. Restores your real file content (now showing as unstaged modifications)

The result: The staged version is empty, and your real content shows as unstaged
additions (all green lines).

Important: This utility only operates on untracked files. It will never stage
already-tracked files to preserve the "pure addition" behavior. Use regular
`git add` for tracked files.

## Installation

The plugin is already installed globally. You can use it from any Git
repository:

```bash
git add-new <file1> [file2] [file3] ...
```

## Usage Examples

```bash
# Stage a single new file
git add-new src/NewComponent.js

# Stage multiple new files
git add-new src/NewComponent.js src/NewStyle.css docs/API.md

# After running git-add-new, use VS Code or git add -p to selectively stage
git add -p  # Interactive staging
```

## Workflow

1. Create your new file(s)
2. Run `git add-new <files>` instead of `git add <files>`
3. Open VS Code or run `git add -p` to see pure additions (all green lines)
4. Selectively stage the parts you want
5. Commit as usual

## Behavior and Notes

- Only untracked files are processed. Tracked files are skipped with a warning.
- Non-existent paths are reported and skipped.
- This tool does not replace `git add` for normal staging; it is specifically
  for preparing new files to show as pure additions in diff viewers.

## Safety Features

- Checks if you're in a Git repository
- Skips files that don't exist
- Handles already-tracked files gracefully
- Uses process-specific backup names to avoid conflicts
- Provides colored status output

## Why Use This?

- **Better code review**: All lines show as additions (green) in diff viewers
- **Easier partial staging**: In VS Code, you can easily see what you're adding
- **Cleaner diffs**: Avoid confusing "modified" status for brand new files
- **Team consistency**: Everyone sees the same clean addition diffs
