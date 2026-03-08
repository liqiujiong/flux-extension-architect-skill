# Frontend Extension Spec (Vue3)

## 1. Module Layout
- Add API wrappers under `src/api/<domain>/`.
- Add pages under `src/views/<domain>/`.
- Add route and menu mappings following current dynamic permission model.

## 2. API Integration
- Keep request wrappers simple and aligned with backend route naming.
- Keep request/response field names consistent with backend VO contracts.
- Ensure list/detail/export/import operations map to expected endpoints.

## 3. Permission Integration
- Use `v-hasPermi` for operation buttons and actionable controls.
- Keep menu/button permission keys aligned with backend `CheckUserInterfaceAuth`.
- Do not rely on frontend permission hiding as the only control.

## 4. Interaction Consistency
- Standardize query form, table actions, dialog behavior, and pagination.
- Provide clear loading and error feedback for every operation.
- Keep destructive actions confirmable and auditable.

## 5. Data Scope UX Expectations
- Reflect filtered results as-is; never imply hidden data is unavailable globally.
- For denied operations, show clear permission-related messages.
- Keep export result expectations aligned with current filtered scope.

## 6. Dictionary Usage
- For dictionary-backed fields, load options with `proxy.useDict('dict_type')`.
- Render table labels with `dict-tag` instead of handwritten `value -> label` mappings.
- Use dictionary options for query filters and edit forms so list, filter, and edit stay consistent.
- If a field should display labels in the admin UI and remain configurable, do not hardcode options in the page.
