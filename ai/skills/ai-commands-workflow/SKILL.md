---
name: ai-commands-workflow
description: How work is done in the `ai-commands/` folder of the Webship Workspace — what a command is there and the shape it has, how the commands of the folder are listed, pulled from the shared repository, added from any GitHub repository, installed into the AI CLI or into one project, checked and updated, copied to adapt and proposed back with `cmd-tools-ai-items.sh`, with every flag of the command and the settings keys of the folder. Use when asked to "write a command", "install a command", "update the installed commands", "pull the shared commands", or when a file of `ai-commands/` is about to be written.
argument-hint: '[what you are about to do in ai-commands]'
---

# ai-commands-workflow

`~/workspace/ai-commands` is the AI Commands folder of a Webship Workspace (container-based, DDEV by default).
AI Commands holds the commands of the workspace as items a person edits in place: one command is one file, `~/workspace/ai-commands/<name>.md`, run as `/<name>` once it is installed. It comes with the AI Commands plugin (`@webship.co/workspace-ai-commands`), which places the commands below in the folder. Every command finds the workspace from its own path; run it from the folder, and read `bash <command> --help` before quoting a flag.

## The order of work

1. **See what is where**: `bash cmd-tools-ai-items.sh`.
2. **Start from one that exists**: `bash cmd-tools-ai-items.sh my-command --clone-to my-command-2`, or write
   `~/workspace/ai-commands/my-command.md` in the shape below.
3. **Read it as its reader would**: an AI assistant that knows nothing else about the work.
4. **Install**: `bash cmd-tools-ai-items.sh my-command --install` (add `--to dev/mysite` for one project).
5. **Keep it in step**: `bash cmd-tools-ai-items.sh --check`, then `bash cmd-tools-ai-items.sh --update`.

## Commands

| Command | What it does | Flags |
| --- | --- | --- |
| `cmd-tool-backup-command.sh` | One command as an archive, into `backups/ai-commands/`: `<name>` | none |
| `cmd-tools-ai-items.sh` | The commands of this folder against the AI CLI and the shared repository: `[name]`. With no flag it shows what each place has | `--add` `--check` `--clone-to` `--confirm` `--fetch` `--filter` `--install` `--list-remote` `--propose` `--pull` `--purpose` `--source` `--status` `--summary` `--to` `--update` |

## The shape of a command

A command is a markdown file with a frontmatter, then what to do with what was typed:

| Part | What it holds |
| --- | --- |
| `description` | What the command does: shown in the list of commands |
| `argument-hint` | What to type after it |
| No `name` | The file names the command: `<name>.md` is `/<name>` |
| The body | Plain Markdown any AI CLI can follow. It reads what was typed from `$ARGUMENTS`, and says in words what the arguments are |

Names are short, lowercase, with hyphens, and start with what the command belongs to. A command and a prompt never share a name.

## Settings

| Key | File | What it says |
| --- | --- | --- |
| `doc.name` | `core/config/workspace.ai-commands.settings.yml` | The folder under the workspace root: `ai-commands` |
| `type` | `core/config/workspace.ai-commands.settings.yml` | `ai-items`: the page lists AI items, with its own install, fetch and propose actions |
| `assistant.name`, `assistant.placeholder` | `core/config/workspace.ai-commands.settings.yml` | What the assistant is called on this page; `default` takes the workspace's |
| `workspaces` | `core/config/settings.yml` | The active folders; `ai-commands` is on it once the plugin is activated |
| `sources.ai_items.repo`, `sources.ai_items.ref` | `core/config/settings.yml` | The shared repository `--list-remote`, `--pull` and `--propose` talk to, and its branch |

## Rules

- **The folder is the draft, the AI CLI is the copy.** Change a command here, then install it again; never edit the installed copy.
- **`--pull` and `--add` bring in what somebody else wrote.** Read a command before it is installed: it tells an AI assistant what to do on this machine.
- **`--propose` prints its plan and stops**; `--confirm` files an issue and opens a request on the shared repository: only when asked.
- **Nothing private in a command**: no password, no token, no personal path; addresses are example addresses.
- **The body is plain Markdown any AI CLI can follow.** Claude Code is the default shape (the frontmatter, the launch line of a prompt), never a requirement.
- **Back up before a rewrite**: `bash cmd-tool-backup-command.sh <name>`.
- The workspace is container-based (DDEV by default): a command that describes it says so.

The AI Commands plugin places these beside this one, each in the workspace folder of its kind: the agent `ai-commands-keeper` (`ai-agents/`), the command `/ai-commands-install` (`ai-commands/`) and the prompt `ai-commands-write-a-new-command` (`ai-prompts/`).
