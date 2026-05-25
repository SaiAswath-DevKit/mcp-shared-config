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
4. Do not write back to Azure DevOps.
5. End with a concise summary:
   - Bug ID and title
   - Files changed
   - What changed
   - Validation performed
