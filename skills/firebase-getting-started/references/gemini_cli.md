# Gemini CLI Setup

To get the most out of Firebase in the Gemini CLI, follow these steps to install the agent extension and the MCP server.

## Recommended: Installing Extensions

We recommend installing the following extensions to get both the agent skills and the MCP server.

### 1. Install Firebase Extension
This provides both the agent skills and the MCP server for working with Firebase.
```bash
gemini extensions install https://github.com/firebase/agent-skills
```

### 2. Verify and Restart
1. Run `gemini extensions list` to verify the `firebase` extension is present. This should include both MCP server and agent skills.
2. Run `gemini mcp list` to verify `firebase-tools` is present.
3. Run `gemini skills list` to verify `firebase-basic` skill is present.
4. Restart the Gemini CLI.

---

## Alternative: Manual MCP Configuration (Project Scope)

If you only want the MCP server for the current project:
```bash
gemini mcp add firebase "npx -y firebase-tools@latest mcp" -e IS_GEMINI_CLI_EXTENSION=true
```
