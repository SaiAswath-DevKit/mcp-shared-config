# Shared MCP Configuration

This repository shares a ready-to-use MCP setup for VS Code.

## Included

- `.vscode/mcp.json`
  - Azure DevOps MCP server
  - Playwright MCP server (Edge)

## Quick Start (New System)

1. Install Node.js (LTS)
2. Install Visual Studio Code
3. Install GitHub Copilot extension in VS Code
4. Clone this repository
5. Open the repository folder in VS Code
6. When prompted, enter:
   - Azure DevOps Organization URL
   - Azure DevOps PAT
   - Default Project (optional)

VS Code will detect `.vscode/mcp.json` automatically.

## Notes

- The config does not hardcode secrets.
- PAT is provided at runtime through input prompts.
- If someone wants to reuse an existing Edge profile session, they can add `--user-data-dir` to the Playwright server args on their machine.
