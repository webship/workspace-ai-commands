Write a new command in the ai-commands folder, in the shape the folder lists, and install it.

The launch line is for Claude Code, the default; the text between the triple quotes can be given to another AI CLI as it is.

```
claude --permission-mode bypassPermissions """
Write a new command named <name> in the ai-commands folder, for: <what-for>
# ~/workspace/ai-commands/<name>.md · an item edited in place · container-based (DDEV by default)
# the body is plain Markdown any AI CLI can follow; no password, no token, no personal path

1. bash cmd-tools-ai-items.sh
   tell me whether a command for this exists already; if one does, propose to adapt it instead
2. read one command of the folder that is close to this, for its shape
3. ask me what the command must do and must never do, and which commands it may run
4. write the file: the frontmatter (description, argument-hint, no name), then what to do with what was typed
   every command, flag and path in it is one you ran or opened
5. bash cmd-tools-ai-items.sh <name> --install
   bash cmd-tools-ai-items.sh <name> --check

Show me the file before you install it, and install only when I say so.
Report where it was installed, and that a new session is needed to pick it up.
"""
```
