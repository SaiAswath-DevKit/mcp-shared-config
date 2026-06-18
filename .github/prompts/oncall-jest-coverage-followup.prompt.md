---
name: oncall-jest-coverage-followup
description: "Analyze bugfix changes for Jest coverage needs, add tests when needed, and create PR only after explicit approval."
argument-hint: "Bug ID (example: 1016100), optional repo path/base branch, optional apply=true"
agent: oncall-jest-coverage-followup
---
Analyze Jest test coverage needs for the provided Azure DevOps bug ID and prepare follow-up test changes.

Requirements:
1. Reuse bug details already retrieved in the current flow when available; otherwise read from Azure DevOps.
2. If bug has linked PRs, analyze PR commit/file changes.
3. If local changes are present, analyze local diff as source of truth.
4. Decide whether Jest coverage is needed and provide rationale.
5. If needed, add minimal targeted Jest test cases for the changed behavior.
6. Run focused validation using this exact single-file command (update repo path only if needed) and report result:
   - `node "C:/CadSource/git/OnCallPresentation/node_modules/jest/bin/jest.js" "C:/CadSource/git/OnCallPresentation/libs/administrator/src/components/UnitTypes/__tests__/UnitTypesComponent.spec.tsx" -t "^UnitTypesComponent(\s.*)?$"`
   - Do not use `nx test administrator` for this step.
7. Default to local review mode only: do not push and do not create PR.
8. Only when user explicitly confirms (`ok create pr`, `approve pr`, or `apply=true`), invoke `oncall-create-ado-pr` to create branch/push/PR.
9. Return summary with:
   - coverage decision
   - evidence analyzed
   - test files added/updated
   - validation status
   - publish status (`Local review only` or `PR Created`)

Do not modify Azure DevOps work item fields/comments/links/tags/state.