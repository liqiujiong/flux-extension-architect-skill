---
name: flux-extension-architect
description: Analyze and standardize FluxPanel feature extensions (FastAPI + Vue3) with a strict governance baseline. Use when planning or reviewing new backend modules, frontend pages, APIs, permissions, data-scope behavior, PR quality gates, and acceptance criteria for admin-panel features.
---

# Flux Extension Architect

Drive FluxPanel extension design and review with a strict, repeatable standard.

Treat data permission control as mandatory, not optional.

## Workflow

1. Normalize extension context
- Capture target business goal, actors, menu entry, permission points, and entities.
- Confirm module boundaries: backend (`controller/service/dao/entity`) and frontend (`api/views/router/permission`).
- For any unknown business rule, state assumptions explicitly.

2. Run architecture dimension analysis
- Read `references/analysis-dimensions.md`.
- Produce conclusions for each required dimension before proposing implementation details.

3. Execute focus checklist
- Read `references/focus-checklist.md`.
- Mark each high-risk item as `pass`, `risk`, or `blocked`.

4. Design backend and frontend extension contracts
- Follow `references/backend-extension-spec.md` and `references/frontend-extension-spec.md`.
- List concrete file-level changes and contracts (request fields, response shape, permission keys).

5. Stage C2: Data permission design and validation (mandatory)
- Read `references/data-permission-architecture.md`.
- Enforce the three-layer permission closure:
  - interface permission (`CheckUserInterfaceAuth`)
  - data permission (`GetDataScope` + `role.data_scope` + `sys_role_dept`)
  - frontend permission (`v-hasPermi` + dynamic menu/button markers)
- Output a data permission decision set:
  - selected data-scope strategy (`1/2/3/4/5`) and business reason
  - alias mapping validation (`query_alias/dept_alias/user_alias`)
  - list APIs that must inject `Depends(GetDataScope(...))`
  - write APIs that must validate operable scope (`check_*_data_scope_services`)
  - admin vs non-admin behavior differences
  - multi-role merge behavior explanation
  - frontend button permission to backend permission mapping table

6. Define quality gates and acceptance tests
- Read `references/quality-gates.md`.
- Apply graded gates and block merge if mandatory checks are missing.

7. Produce standard review package
- Follow `references/report-template.md`.
- Keep the output decision-complete so implementation can start directly.

## Hard Rules

1. Require data permission filtering by default for new admin modules with list/export/detail reads.
2. Require alias consistency checks when DAO uses `data_scope_sql`.
3. Require a permission anchor field on core business tables (`dept_id` first, `create_by` second).
4. Require explicit `role -> dept` source when scope is custom (`data_scope=2`).
5. Reject frontend-only permission control without backend dependency checks.
6. Require "data permission design card" in PRs for new modules or query-scope changes.

## Output Standard

Always include:
- extension goal and scope
- architecture direction and key tradeoffs
- file-level implementation map (backend and frontend)
- permission closure proof (interface/data/frontend)
- graded quality-gate results
- acceptance tests, including data-scope regression scenarios
- assumptions, defaults, and open risks

## References

- `references/analysis-dimensions.md`
- `references/focus-checklist.md`
- `references/backend-extension-spec.md`
- `references/frontend-extension-spec.md`
- `references/data-permission-architecture.md`
- `references/quality-gates.md`
- `references/report-template.md`
