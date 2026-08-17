# Adding Trello MCP to a New Project

## Quick Setup

From any project directory, run:

```bash
claude mcp add-json -s user trello '{"command":"node","args":["/home/io/trello-mcp/dist/index.js"],"env":{"TRELLO_API_KEY":"YOUR_API_KEY","TRELLO_TOKEN":"YOUR_TOKEN"}}'
```

## Scope Options

| Scope | Flag | Effect |
|-------|------|--------|
| **user** | `-s user` | Available in all projects for your user account |
| **project** | `-s project` | Only available in the current project (saves to `.mcp.json` in project root) |
| **local** | `-s local` (default) | Per-project, stored in Claude's internal config directory |

**Recommended:** Use `-s user` so you only need to do this once.

## Useful Commands

```bash
# List configured MCP servers
claude mcp list

# Remove the server (match the scope it was added with)
claude mcp remove trello -s user

# Re-add with updated credentials
claude mcp remove trello -s user
claude mcp add-json -s user trello '{"command":"node","args":["/home/io/trello-mcp/dist/index.js"],"env":{"TRELLO_API_KEY":"...","TRELLO_TOKEN":"..."}}'
```

## Updating Credentials

If your Trello token expires, run `~/update-trello-mcp.sh` or re-run the `add-json` command above with the new token.

## Troubleshooting

- **Server not appearing:** Make sure you're checking the right scope. `claude mcp list` shows servers available in the current project context.
- **Connection errors:** Verify the server is built — run `ls /home/io/trello-mcp/dist/index.js` to confirm the entry point exists.
- **Token issues:** Generate a new token at https://trello.com/power-ups/admin and update via the add-json command.
