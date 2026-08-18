---
name: project-update-audit
description: Audit project updates before Codex changes PRDs, field lists, API contracts, frontend/backend code, prompts, workflow rules, data migration plans, or sync messages. Use when the user asks to modify project facts, output Sync to Frontend or Sync to Backend, update a multi-thread workflow, revise prompt rules, check whether files match the latest confirmed scope, or prevent stale context, mixed projects, deleted fields, permission boundary mistakes, and missed downstream synchronization.
---

# Project Update Audit

Use this skill to run a short pre-update audit before changing project artifacts. The goal is to make project boundary checks, fact-source checks, impact checks, and sync decisions happen automatically without turning every conversation into a long review.

## Core Rule

Before any eligible update, perform the **30-second audit** internally first. Show only a compact summary unless the user asks for the full audit.

Eligible updates include:

- PRD, product plan, roadmap, success metrics, or workflow changes
- Field list, data model, schema, migration, SQL, or report metric changes
- `API_CONTRACT.md`, frontend service, backend route, adapter, or mock data changes
- Prompt rules, classification logic, AI recognition rules, or evaluation criteria changes
- Sync messages between frontend, backend, product, docs, or operations threads
- Project fact-source synchronization, file range audits, or "check 01-14 files" requests
- Any request that says "do not mix projects", "use latest confirmed scope", "write into workflow", "evaluate whether sync is needed", or similar

## 30-Second Audit

Answer these five questions before editing or writing the final answer:

1. **Project Boundary**: Which project is this? Which projects, old conversations, or documents must not be mixed in?
2. **Current Action**: What is being changed now? What is explicitly out of scope?
3. **Latest Fact Sources**: Which files, docs, links, sync messages, or user confirmations are authoritative? Which older facts are superseded?
4. **Impact Scope**: Does this affect PRD, field list, API contract, frontend, backend, prompts, mock data, tests, docs, deployment, permissions, or operations?
5. **Sync Decision**: Should this produce `Sync to Frontend`, `Sync to Backend`, workflow updates, changelog notes, or no sync?

If any answer is uncertain and the choice could cause project drift, ask one concise question before making changes. If the uncertainty is low risk, state the assumption and continue.

## User-Facing Summary

Use this compact format when the audit matters to the user:

```text
更新前审计：
- 项目边界：...
- 本轮只改：...
- 最新事实源：...
- 影响范围：...
- 同步判断：需要/不需要 Sync to ...
```

Do not show the audit when it would add noise and all five answers are obvious. Still perform it internally.

## Sync Decision Rules

Output `Sync to Frontend` when an update affects pages, fields, states, mock data, frontend API calls, validation, UI copy, frontend workflow, or browser behavior.

Output `Sync to Backend` when an update affects APIs, data model, persistence, external service adapters, jobs, logs, auth, deployment, schema, migrations, or backend business rules.

Output both when a business rule or data structure crosses the frontend/backend boundary.

Do not output sync when the change is only wording, report formatting, or a local note with no downstream implementation impact. In that case, say "同步判断：不需要输出 Sync".

## Anti-Drift Checks

Before making changes, explicitly protect against these common failures:

- Do not reuse old project facts after the user says a scope, field, or source has changed.
- Do not mix similarly named projects or earlier conversations when the user provides a newer source.
- Do not preserve fields, links, or workflows that the user confirmed should be deleted.
- Do not let frontend directly call systems that the architecture says belong behind backend services.
- Do not treat permission, network, or tool failures as user capability problems.
- Do not expand the update into a broad refactor unless the user asked for it.

## Artifact Update Pattern

When editing files:

1. Locate the authoritative file(s).
2. Search for old terms and affected duplicates.
3. Update the smallest necessary set of files.
4. Re-scan for stale terms.
5. Report what changed and whether sync is needed.

When updating a workflow:

1. Add the trigger condition.
2. Add the audit card.
3. Add the output format.
4. Add sync rules.
5. Add a frequency guard: keep routine audit summaries brief.

## References

For a reusable card and examples, read `references/audit-cards.md` when the user asks to write the workflow into docs, share the template, or create a repeatable checklist.
