# Backend Extension Spec (FastAPI)

## 1. Module Layout
- Add controller under `module_admin/controller/`.
- Add service under `module_admin/service/`.
- Add dao under `module_admin/dao/`.
- Add DO/VO models under `module_admin/entity/do` and `module_admin/entity/vo`.
- Register router in `router/router_manager.py`.

## 2. Endpoint Conventions
- Use clear prefixes and action naming consistent with existing modules.
- Enforce interface auth via `Depends(CheckUserInterfaceAuth('xxx:yyy:zzz'))`.
- Wrap business responses with project response conventions.

## 3. Validation And Errors
- Validate request models in VO layer.
- Raise business exceptions with explicit user-facing messages.
- Keep error handling predictable and traceable.

## 4. Service Layer Rules
- Keep service methods focused on domain logic and transaction boundaries.
- Do uniqueness and permission checks before write operations.
- Separate write validation and read filtering logic.

## 5. DAO Layer Rules
- Keep query assembly explicit and auditable.
- For `data_scope_sql`, validate alias and anchor-field compatibility.
- Ensure list/detail/export read paths apply the same scope strategy.

## 6. Data Permission Requirements
- Read endpoints with business data must inject `Depends(GetDataScope(...))`.
- Write endpoints that act on existing records must validate operable scope.
- Keep admin bypass behavior explicit and constrained.

## 7. Logging And Audit
- Add operation logs for create/update/delete/import/export/reset flows.
- Include actor, target ID, and operation result for traceability.

## 8. Dictionary Governance
- For enum-like business fields, prefer `/system/dict` over frontend hardcoded mappings.
- Provide `sys_dict_type` and `sys_dict_data` SQL as part of the delivery package.
- If using code generation metadata, set the column `dict_type` so generated pages/forms inherit dictionary behavior.
- Keep dictionary type names stable because backend cache and frontend `useDict('dict_type')` depend on them.
