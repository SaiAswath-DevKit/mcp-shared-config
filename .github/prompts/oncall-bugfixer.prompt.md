---
name: oncall-bugfixer
description: "Run the OnCall bug-fix workflow from an Azure DevOps bug ID using read-only ADO context and local repo code changes."
argument-hint: "Bug ID (example: 54321)"
agent: oncall-bugfixer-orchestrator
---
Run the OnCall bug-fix workflow for the bug ID provided in the user input.

Requirements:
1. Read bug details from Azure DevOps (read-only).
2. Locate likely files in local repos under `C:\CadSource\git` with priority:
   - `OnCallPresentation`
   - `OnCallWebsite`
3. Apply the smallest targeted fix.
4. Do not modify Azure DevOps work item comments/links/tags, and do not update fields except explicit bug-fix summary publish approval.
5. If the user explicitly requests PR creation after local validation, continue by invoking `oncall-create-ado-pr` using the same bug ID and current repo changes.
6. If the user requests bug-fix summary generation, invoke `oncall-sync-bugfix-summary` to produce draft summary from bug details + linked PR commit/file changes.
7. Publish summary to Azure DevOps only after explicit user approval (`ok push`, `approve push`, or equivalent).
8. If the user requests Jest coverage follow-up, invoke `oncall-jest-coverage-followup` to analyze linked PR/local diffs, add needed tests locally, and return review summary first.
9. Create/push Jest coverage PR only after explicit user approval (`ok create pr`, `approve pr`, or equivalent).
10. End with a concise summary:
   - Bug ID and title
   - Files changed
   - What changed
   - Validation performed
   - PR details when created (branches + PR URL)
   - Bug-fix summary status (draft/published + field used)
   - Jest coverage follow-up status (needed/not needed + local-only or PR created)
