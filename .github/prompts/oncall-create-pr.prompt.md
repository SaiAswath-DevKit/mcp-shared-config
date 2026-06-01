---
name: oncall-create-pr
description: "Create an Azure DevOps PR for an OnCall bugfix using MCP settings and branch naming skylanders/bugfixes/<bug-id>-<slug>."
argument-hint: "Bug ID (example: 1016100), optional repo path/base branch"
agent: oncall-create-ado-pr
---
Create an Azure DevOps pull request for the provided bug ID.

Requirements:
1. Read bug title/details from Azure DevOps (prefer subagent `oncall-bugfixer-ado-reader`).
2. Read `.vscode/mcp.json` and use Azure DevOps MCP settings (`AZURE_DEVOPS_ORG_URL`, `AZURE_DEVOPS_DEFAULT_PROJECT`) as defaults.
3. Build source branch name as: `skylanders/bugfixes/<bug-id>-<title-slug>`.
4. If staged changes already exist in the target repo, skip code locator/discovery and create PR directly from staged changes.
5. Create/switch to the source branch in the target local repo.
6. Check for staged/unstaged/uncommitted changes and apply create-PR safety checks.
7. If staged changes exist, commit staged changes with a bug-focused commit message.
8. Ensure source branch is pushed to remote.
9. Create an Azure DevOps PR targeting the configured/default base branch.
10. In the PR description, include `Related Bug: <bug-id>` and a direct Azure DevOps bug URL built from `AZURE_DEVOPS_ORG_URL` and `AZURE_DEVOPS_DEFAULT_PROJECT`.
11. Return a concise summary with PR URL, branch names, commit, and any skipped/blocking conditions.

Do not modify Azure DevOps work item fields/comments unless explicitly requested.
