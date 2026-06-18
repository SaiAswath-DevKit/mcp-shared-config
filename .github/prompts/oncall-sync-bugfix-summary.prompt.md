---
name: oncall-sync-bugfix-summary
description: "Generate an auto bug-fix summary from bug + linked PR changes, then optionally publish it to Azure DevOps after explicit approval."
argument-hint: "Bug ID (example: 1016100), optional apply=true"
agent: oncall-sync-bugfix-summary
---
Generate a bug-fix summary for the provided Azure DevOps bug ID.

Requirements:
1. Reuse bug details already retrieved in the current flow when available; otherwise read from Azure DevOps.
2. Find pull requests linked to the bug and analyze commit/file changes.
3. Build the summary exactly in this format:
   - What We Fixed -
   - Reason for the change -
   - Test Summary:
   - Impact Areas -
   - Testing Notes -
4. Return draft summary first for review.
5. Publish to Azure DevOps only on explicit user approval (`ok push`, `approve push`, or `apply=true`).
6. When publishing, update only bug-fix summary field (`Custom.BugFixSummary` preferred, `System.History` fallback).
7. Return publish result with field name used and confirmation details.

Do not modify other Azure DevOps work item fields/comments/links/tags/state.