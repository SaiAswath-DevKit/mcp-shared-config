---
description: "Use when fixing Azure DevOps bugs for OnCall repos, locating candidate files in C:\\CadSource\\git, or prioritizing search between OnCallPresentation and OnCallWebsite."
name: "oncall-bugfixer-codebase"
---
# OnCall Bug Fix Codebase Guidance

## Repo Priority
1. Search `C:\CadSource\git\OnCallPresentation` first.
2. If not found, search `C:\CadSource\git\OnCallWebsite`.
3. If the issue spans frontend and backend, include candidates from both repos.

## Known Structure
- `OnCallPresentation`: Nx monorepo (React/TypeScript) with `apps/` and `libs/`.
- `OnCallWebsite`: .NET backend (`OnCall.Website`, `OnCall.Proxy`) plus frontend under `Presentation/`.

## Common Hotspots
- UI/state bugs: Redux stores, reducers, selectors, component state wiring.
- API/contract bugs: Website controllers, proxy/service layers, request/response mappings.
- Config/feature issues: feature flags, config service usage, environment-specific branching.

## Fix Expectations
- Make the smallest targeted code change required to address the bug.
- Preserve existing patterns and naming conventions.
- Prefer adding or updating tests when a clear nearby test pattern exists.

## Workflow Boundary
- Azure DevOps is read-only in this workflow.
- Do not post comments, update status, or modify work items.
- End with a concise chat summary for user review.
