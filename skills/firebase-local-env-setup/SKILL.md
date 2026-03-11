---
name: firebase-local-env-setup
description: Bare minimum setup for getting started with Firebase for the agent. This covers Node.js installation, Firebase CLI availability, login, and MCP server installation. Use this to ensure the local environment is fully prepared before using Firebase.
---

# Firebase Local Environment Setup

This skill documents the bare minimum setup required for a full Firebase experience for the agent. Before starting to use any Firebase features, you MUST verify that each of the following steps has been completed.

## 1. Verify Node.js
Firebase tools require Node.js version 20 or higher.
- **Action**: Run `node --version`.
- **Handling**: If Node.js is missing or `< v20`, instruct the user to install the latest LTS version of Node.js from [nodejs.org](https://nodejs.org/) or use a version manager like `nvm`. **Stop and wait** for the user to complete this before proceeding.

## 2. Verify Firebase CLI
The Firebase CLI is the primary tool for interacting with Firebase services.
- **Action**: Run `npx -y firebase-tools@latest --version`.
- **Handling**: Ensure this command runs successfully and outputs a version number.

## 3. Verify Firebase Authentication
You must be authenticated to manage Firebase projects.
- **Action**: Run `npx -y firebase-tools@latest login`.
- **Handling**: If the environment is remote or restricted (no browser access), run `npx -y firebase-tools@latest login --no-localhost` instead.

## 4. Install Agent Skills and MCP Server
To fully manage Firebase, the agent needs specific skills and the Firebase MCP server installed. Identify the agent environment you are currently running in and follow the corresponding setup document strictly.

**Read the setup document for your current agent:**
- **Gemini CLI**: Review [references/gemini_cli.md](references/gemini_cli.md)
- **Antigravity**: Review [references/antigravity.md](references/antigravity.md)
- **Claude Code**: Review [references/claude_code.md](references/claude_code.md)
- **Cursor**: Review [references/cursor.md](references/cursor.md)
- **GitHub Copilot**: Review [references/github_copilot.md](references/github_copilot.md)
- **Other Agents** (Windsurf, Cline, etc.): Review [references/other_agents.md](references/other_agents.md)

---
**CRITICAL AGENT RULE:** Do NOT proceed with any other Firebase tasks until EVERY step above has been successfully verified and completed.
