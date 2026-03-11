---
name: firebase-local-env-setup
description: Bare minimum setup for getting started with Firebase for the agent. This covers Node.js installation, Firebase CLI availability, login, and MCP server installation. Use this to ensure the local environment is fully prepared before using Firebase.
---

# Firebase Local Environment Setup

This skill documents the bare minimum setup required for a full Firebase experience for the agent. Before starting to use any Firebase features, you MUST verify that each of the following steps has been completed.

## 1. Verify Node.js
- **Action**: Run `node --version`.
- **Handling**: Ensure Node.js is installed and the version is `>= 24`. If Node.js is missing or `< v24`, install it based on the operating system:

  **For macOS or Linux:**
  We recommend using `nvm` (Node Version Manager):

  1. Install `nvm`:
     ```bash
     curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash
     ```
  2. Make `nvm` available in the current session. You normally need to restart the terminal or source one of the following configuration files based on the active shell:
     ```bash
     # For Bash Shell
     source ~/.bash_profile
     source ~/.bashrc

     # For Zsh
     source ~/.zprofile
     source ~/.zshrc

     # For non-bash or sh shells, often used on Debian-based systems
     source ~/.profile
     ```
  3. Install Node.js 24:
     ```bash
     nvm install 24
     nvm use 24
     ```

  **For Windows:**
  1. Guide the user to the [download page](https://nodejs.org/en/download) or download the Windows packages [here](https://nodejs.org/download/release/latest-v24.x/).
  2. Request the user to manually install Node.js and reply when finished. **Stop and wait** for the user's confirmation.
  3. After the user confirms, check if Node.js is available using the following command:
     ```bash
     node --version
     ```


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
