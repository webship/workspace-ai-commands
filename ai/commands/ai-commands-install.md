---
description: Install a command of the ai-commands/ folder of the Webship Workspace into the AI CLI, or into one project, with cmd-tools-ai-items.sh — read it first, install it, and check that what is installed is what the folder has.
argument-hint: '<command> [<workspace>/<project>]'
---

# /ai-commands-install

Install the command of `~/workspace/ai-commands` named in: `$ARGUMENTS`

The arguments are the text typed after the command: the first word is the command (its name in
`ai-commands/`), and a second word, as `<workspace>/<project>`, is one project to install it into
instead of the whole machine. With no command, stop and list the ones there are. The workspace is
container-based (DDEV by default); an install copies a file, and starts nothing.

## 1. Find it, and read it

```bash
cd ~/workspace/ai-commands
bash cmd-tools-ai-items.sh
```

Read the command before installing it: it tells an AI assistant what to do on this machine. If it
asks for something that should not be done unasked (deleting, pushing, spending), say so and
stop.

## 2. Install

```bash
bash cmd-tools-ai-items.sh <command> --install
bash cmd-tools-ai-items.sh <command> --install --to <workspace>/<project>
```

Use the second form when a project was named. Without `--to` it goes into the AI CLI of this
machine (Claude Code by default: `~/.claude/commands`).

## 3. Check

```bash
bash cmd-tools-ai-items.sh <command> --check
```

It compares what is installed against the folder and changes nothing.

## 4. Report

Where the command was installed, and that a new session is needed to pick it up. For commands from
another repository, or an update of everything that is installed, hand over to the `ai-commands-keeper` agent;
the `ai-commands-workflow` skill has every flag.
