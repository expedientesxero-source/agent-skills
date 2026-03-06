# Cursor Setup

To get the most out of Firebase in Cursor, follow these steps to install the agent skills and the MCP server.

## 1. Install/Update Agent Skills

Agent skills provide the interactive instructions for working with Firebase.

**Installation:**
```bash
npx skills add firebase/agent-skills
```

## 2. Install Firebase MCP Server

The MCP server allows Cursor to interact directly with your Firebase projects.

Add the following to your `~/.cursor/mcp.json` (global) or `.cursor/mcp.json` (project):
```json
{
  "mcpServers": {
    "firebase": {
      "command": "npx",
      "args": ["-y", "firebase-tools@latest", "mcp"]
    }
  }
}
```
