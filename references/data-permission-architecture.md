# Data Permission Architecture (Mandatory)

Use this file as a hard requirement when reviewing or designing any new admin module.

## 1. Current Mechanism Mapping
- Interface permission: `CheckUserInterfaceAuth`.
- Data permission: `GetDataScope` + role `data_scope` + `sys_role_dept`.
- Frontend permission: `v-hasPermi` + dynamic menu/button permission markers.

## 2. Data Scope Strategy
Choose one or more expected behavior paths and explain why:
- `1`: all data
- `2`: custom data (role-dept mapping)
- `3`: same-department data
- `4`: same-department and descendants
- `5`: self-only data

## 3. Mandatory Alias Validation
When using `GetDataScope(query_alias, db_alias, user_alias, dept_alias)`:
- Ensure `query_alias` matches the DAO query model symbol.
- Ensure `dept_alias` or `user_alias` exists on the target model.
- If aliases mismatch, flag as merge-blocking risk.

## 4. Mandatory Injection Rules
- Read APIs (list/detail/export) with business data: inject `Depends(GetDataScope(...))`.
- Write APIs operating existing records: validate operable scope with service checks.
- If a module is explicitly public read-only, document exemption reason.

## 5. Admin vs Non-Admin
- Describe the expected bypass behavior for admin users.
- Describe restriction behavior for non-admin users.
- Ensure behavior is consistent for list, detail, and export.

## 6. Multi-Role Behavior
- Explain how multiple roles combine (union/override expectations).
- Verify real behavior against assumptions and note gaps.

## 7. Frontend-Backend Permission Mapping
Provide an explicit table:

| Frontend Action | Frontend Perm Key | Backend Endpoint | Backend Perm Check |
|---|---|---|---|
|  |  |  |  |

## 8. Data Permission Design Card (PR Required)
Every new module PR must include:
- Permission anchor field (`dept_id` or `create_by`)
- Selected scope type(s) and rationale
- Required `GetDataScope` injection points
- Required write-scope validation points
- Test evidence for scope and bypass behavior
