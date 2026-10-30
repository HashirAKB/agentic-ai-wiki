# Block writes outside working directories

Source: [Claude Code changelog 2.1.314](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md) · Type: setting

## What it is for
`permissions.blockWritesOutsideWorkingDirectories: true` in `~/.claude/settings.json` makes Claude Code's Write, Edit and NotebookEdit tools refuse any path outside the folders the session works in, in every permission mode. A runaway or misdirected session cannot change files elsewhere on the machine.

## When to reach for it
Always on. It matters most when you let Claude work with fewer prompts (auto-accept edits, auto mode).

## Commands that matter
- Start Claude Code **inside the project folder** (`cd <project>` then `claude`). The folder you start in is the working directory.
- `/add-dir <path>` adds another folder for this session when a task genuinely needs it.
- `/status` shows which settings files loaded.

## First exercise (about 5 minutes)
In a project folder, start `claude` and ask it to create a file one level above the project (for example `../test.txt`). It should refuse. Then run `/add-dir ..` and ask again; now it may proceed (delete the test file afterwards).

## How you know it worked
The write outside the project is refused with a message about working directories.

## Common mistake
Starting Claude Code from your home folder. Then the whole home folder is the working directory and the block protects almost nothing. Shell commands are not covered by this setting; Claude Code's normal permission prompts still govern those.
