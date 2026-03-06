# Claude Code Setup

To get the most out of Firebase in Claude Code, follow these steps to install the agent skills and the MCP server.

## Recommended Method: Using Plugins

We recommend using the plugin marketplace to install both the agent skills and the MCP functionality.

### 1. Add Marketplaces
```bash
claude plugin marketplace add firebase/agent-skills
claude plugin marketplace add firebase/firebase-tools
```

### 2. Install Plugins
```bash
claude plugin install firebase@firebase
```

## Alternative: Manual MCP Configuration
If you prefer to add the MCP server manually:
```bash
claude mcp add firebase npx -- -y firebase-tools@latest mcp
```
