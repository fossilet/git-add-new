# AGENTS.md

This file provides guidance to AI coding agents when working with code in this
repository.

## Project Overview

`git-add-new` is a Git plugin that stages new (untracked) files as pure
additions using the "empty file trick":

1. Move file to backup
2. Create empty file and stage it (`git add`)
3. Restore the original file content (now shows as unstaged additions)

This makes new files appear as all-green additions in diff viewers instead of
"modified" files.

## Commands

```bash
# Run the plugin directly
./git-add-new [-A] <file1> [file2] ...

# Install globally (copies to a directory in PATH)
cp git-add-new ~/.local/bin/  # or wherever PATH looks

# Test in a git repository
git add-new <untracked-file>
```

No build, test, or lint commands — it's a standalone Bash script.

## Architecture

Single Bash script (`git-add-new`) with no dependencies beyond standard Git and
Bash built-ins.

Key logic:

- Validates git repository context
- Parses `-A` flag for "add all untracked" mode
- Uses `git ls-files --others --exclude-standard -z` to find untracked files
  (respects `.gitignore`)
- Skips already-tracked files to preserve pure-addition behavior
- Processes files one-by-one with the backup/empty/restore cycle

## File Structure

```
git-add-new        # Main script (executable)
README.md          # User-facing documentation
var/todo.md        # Personal notes (not part of project)
```
