# Antigravity Setup

To get the most out of Firebase in Antigravity, follow these steps to install the agent skills and the MCP server.

## Recommended: Global Setup

We recommend installing both the agent skills and the MCP server globally for consistent access across projects.

### 1. Install Firebase Skills
This provides the agent skills for working with Firebase.
```bash
npx skills add firebase/agent-skills --agent antigravity --all --global
```

### 2. Configure Firebase MCP Server
The MCP server allows Antigravity to interact directly with your Firebase projects.

1. Find the `mcp_config.json` file in your system:
  - macOS / Linux: `~/.gemini/antigravity/mcp_config.json`  
  - Windows: `%USERPROFILE%\\.gemini\\antigravity\\mcp_config.json`
2. Add the following to `mcpServers` section in `mcp_config.json`:
    ```json
    "firebase": {
      "command": "npx",
      "args": [
        "-y",
        "firebase-tools@latest",
        "mcp"
      ]
    }
    ```
    For example, the `mcp_config.json` in your system might look like this:
    ```json
    {
      "mcpServers": {
        "firebase": {
          "command": "npx",
          "args": [
            "-y",
            "firebase-tools@latest",
            "mcp"
          ]
        }
      }
    }
    ```

### 3. Verify and Restart
1. Run `npx skills list` to verify the `firebase-basics` skill is present.
2. Verify that the `firebase-tools` server is present in your `mcp_config.json`.
3. Restart Antigravity and check the MCP server list in the UI to confirm `firebase-tools` is connected.
