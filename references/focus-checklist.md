# Focus Checklist

Mark each item as `pass`, `risk`, or `blocked`.

## A. Architecture Consistency
- New backend code follows `controller -> service -> dao -> entity`.
- Frontend code follows `api -> views -> permission/router`.
- Naming is consistent with existing module patterns.

## B. Contract Safety
- Response shape stays aligned with project conventions.
- Field names are consistent between DB, VO, and frontend forms.
- Non-compatible field changes are explicitly versioned or guarded.

## C. Permission Closure
- Every operation endpoint has backend interface permission checks.
- Every read path with business data is data-scope constrained.
- Every frontend operation button has permission mapping to backend perm keys.

## D. Data Permission Safety
- Main table has an explicit permission anchor (`dept_id` or `create_by`).
- `data_scope_sql` alias mapping is validated.
- Custom scope (`2`) has clear `role -> dept` source.

## E. Dictionary Governance
- Enum/status/type fields that need label rendering are evaluated for `/system/dict`.
- Required `sys_dict_type` and `sys_dict_data` SQL is included.
- Frontend uses `useDict()` and `dict-tag` instead of hardcoded label maps.

## F. Operational Risk
- Export/import reads respect the same data scope as list/detail.
- Cross-department or cross-owner bypass attempts are tested.
- Admin and non-admin behavior differences are explicit and expected.

## G. Delivery Readiness
- PR includes a data permission design card.
- Mandatory tests are attached as evidence.
- Merge is blocked if mandatory gate checks are missing.
