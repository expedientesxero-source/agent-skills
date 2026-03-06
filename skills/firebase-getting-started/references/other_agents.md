# Other Agents Setup

If you use another agent (like Windsurf, Cline, or Claude Desktop), follow these steps to install the agent skills and the MCP server.

## 1. Install/Update Agent Skills

Agent skills provide the interactive instructions for working with Firebase.

**Installation:**
```bash
npx skills add firebase/agent-skills --all
```

## 2. Install Firebase MCP Server

The MCP server allows your agent to interact directly with your Firebase projects. Use the following settings in their respective MCP configuration files (e.g., `~/.codeium/windsurf/mcp_config.json`, `cline_mcp_settings.json`, or `claude_desktop_config.json`):

**Configuration:**
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
