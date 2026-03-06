---
name: firebase-getting-started
description: Bare minimum setup for getting started with Firebase for the agent. This covers Node.js installation, Firebase CLI availability, login, and MCP server installation. Use this to ensure the local environment is fully prepared before using Firebase.
---

# Firebase Getting Started

This skill documents the bare minimum setup required for a full Firebase experience for the agent. Before starting to use any Firebase features, you MUST verify that each of the following steps has been completed.

## 1. Install Node.js
Firebase tools require Node.js version 20 or higher.

**Verification:**
Run `node --version`.

**Action if missing or version < 20:**
Install the latest LTS version of Node.js from [nodejs.org](https://nodejs.org/) or use a version manager like `nvm`.

## 2. Ensure Firebase CLI is Available
The Firebase CLI is the primary tool for interacting with Firebase services.

**Verification & Setup:**
Run the following command to ensure the latest version of the Firebase CLI is available via `npx`:
```bash
npx -y firebase-tools@latest --version
```

## 3. Log In to Firebase
You must authenticate with your Google account to manage Firebase projects.

**Verification:**
Run `npx -y firebase-tools@latest login` to ensure you are logged in.

*Note: If you are in a remote shell or a restricted environment where a browser cannot be opened, use `npx -y firebase-tools@latest login --no-localhost`.*

## 4. Installing extension/plugin
To get the most out of Firebase, you should install the Firebase agent skills and the Firebase MCP server. For many agents, this can be done through a single extension or plugin installation.

Choose your agent for detailed setup instructions:
- **Gemini CLI**: See [references/gemini_cli.md](references/gemini_cli.md)
- **Antigravity**: See [references/antigravity.md](references/antigravity.md)
- **Claude Code**: See [references/claude_code.md](references/claude_code.md)
- **Cursor**: See [references/cursor.md](references/cursor.md)
- **GitHub Copilot**: See [references/github_copilot.md](references/github_copilot.md)
- **Other Agents**: (Windsurf, Cline, etc.) See [references/other_agents.md](references/other_agents.md)

*Note: If both agent skills and MCP server can be installed through an extension or plugin, we recommend that method by default.*

---

**Crucial:** Do not proceed with any other Firebase tasks until every step above has been verified and completed.
