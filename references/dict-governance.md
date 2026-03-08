# Dictionary Governance

Use this file when a module introduces statuses, types, flags, modes, levels, or other enum-like values that must display human-readable labels in the admin UI.

## 1. When To Use `/system/dict`
- Use `/system/dict` when the field is a business enum and the frontend must show labels directly.
- Use `/system/dict` when options may need to be maintained by admins instead of being fixed in code.
- Do not hardcode label maps in frontend pages for dictionary-backed fields.

## 2. Naming Rules
- Use lowercase snake_case for `dict_type`, for example `car_type`, `order_status`, `roas_calc_mode`.
- Reserve `sys_` prefixes for platform/system dictionaries.
- Keep `dict_type` stable after release because backend cache and frontend lookup both depend on it.

## 3. Required SQL Deliverables
- Provide one `sys_dict_type` insert statement.
- Provide one or more `sys_dict_data` insert statements.
- Keep `status='0'` for active records unless there is a concrete reason not to.
- Set `list_class` intentionally because it affects tag styling in the UI.

## 4. Backend Rules
- Treat dictionary data as configuration, not business code constants.
- If the field is generated from table metadata, set the column `dict_type` in `gen_table_column`.
- If dictionary definitions are part of initialization, include them in SQL deliverables or migration deliverables.

## 5. Frontend Rules
- Load dictionary options with `proxy.useDict('dict_type')`.
- Render table labels with `dict-tag`.
- Use the same dictionary source in query filters, edit dialogs, and detail views.
- Avoid duplicate option arrays in page code when a dictionary exists.

## 6. Review Checklist
- Is the field really dictionary-backed instead of free text?
- Is `dict_type` named consistently with the domain?
- Are SQL statements included in the implementation package?
- Does the page use `useDict()` and `dict-tag` where appropriate?
- Is the storage value type consistent with the frontend usage (`string` vs `number`)?

## 7. Example Pattern
- Dictionary type:
  - `dict_name`: `车辆类型`
  - `dict_type`: `car_type`
- Frontend usage:
  - `const { car_type } = proxy.useDict('car_type')`
  - table display: `dict-tag`
  - select options: `v-for="dict in car_type"`
