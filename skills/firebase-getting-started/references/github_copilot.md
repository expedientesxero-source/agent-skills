# GitHub Copilot Setup

To get the most out of Firebase with GitHub Copilot in VS Code, follow these steps to install the agent skills and the MCP server.

## 1. Install/Update Agent Skills

Agent skills provide the interactive instructions for working with Firebase.

**Installation:**
```bash
npx skills add firebase/agent-skills --agent github-copilot --all
```

## 2. Install Firebase MCP Server

The MCP server allows GitHub Copilot to interact directly with your Firebase projects.

1. Edit your workspace `.vscode/mcp.json` or your global User Settings.
2. Add the following configuration:
```json
{
  "mcp": {
    "servers": {
      "firebase": {
        "type": "stdio",
        "command": "npx",
        "args": ["-y", "firebase-tools@latest", "mcp"]
      }
    }
  }
}
```
