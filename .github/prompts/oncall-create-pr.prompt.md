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
5. If unstaged tracked local changes exist and the user explicitly wants to create PR from current local work, stage those tracked changes and continue.
6. Create/switch to the source branch in the target local repo.
7. Check for staged/unstaged/uncommitted changes and apply create-PR safety checks.
8. If staged changes exist, commit staged changes with a bug-focused commit message.
9. Ensure source branch is pushed to remote.
10. Create an Azure DevOps PR targeting the configured/default base branch.
11. Link the bug work item to the created PR artifact (mandatory). If the create call did not link it automatically, add the relation immediately after PR creation.
12. In the PR description, include `Related Bug: <bug-id>` and a direct Azure DevOps bug URL built from `AZURE_DEVOPS_ORG_URL` and `AZURE_DEVOPS_DEFAULT_PROJECT`.
13. Return a concise summary with PR URL, branch names, commit, bug-link status, and any skipped/blocking conditions.

Do not modify Azure DevOps work item fields/comments unless explicitly requested. Exception: adding or verifying the required bug-to-PR link relation is allowed in this workflow.
