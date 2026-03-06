# Flux Extension Architect

对 FluxPanel（FastAPI + Vue3）功能扩展进行架构分析与标准化，在严格治理基线之上规划或评审新后台模块、前端页面、API、权限与数据范围行为、PR 质量门禁及验收标准。

## 适用场景

在以下情况使用本 Skill：

- 规划或评审新的后台模块、前端页面、API
- 设计或审查权限点与数据范围（data-scope）行为
- 制定 PR 质量门禁与验收标准
- 需要统一、可复用的管理后台扩展设计规范

## 核心原则

**数据权限按默认必做，而非可选。**  
新管理端模块的列表/导出/详情等读操作，默认要求数据权限过滤；前端仅做权限控制而后端不做依赖校验的方案不予接受。

## 工作流概览

1. **归一化扩展上下文** — 明确业务目标、角色、菜单入口、权限点与实体，确认前后端模块边界。
2. **架构维度分析** — 按 `references/analysis-dimensions.md` 逐项给出结论。
3. **焦点检查清单** — 按 `references/focus-checklist.md` 对高风险项标记 pass/risk/blocked。
4. **前后端扩展契约** — 遵循 `references/backend-extension-spec.md` 与 `references/frontend-extension-spec.md`，列出文件级变更与契约（请求字段、响应结构、权限 key）。
5. **数据权限设计与校验（必做）** — 按 `references/data-permission-architecture.md` 落实三层权限闭环：接口权限、数据权限、前端权限，并输出数据权限决策集。
6. **质量门禁与验收** — 按 `references/quality-gates.md` 应用分级门禁，缺失必检项则禁止合入。
7. **标准评审包** — 按 `references/report-template.md` 产出可直接支撑实施的决策完整输出。

## 硬性规则摘要

- 新管理端模块的列表/导出/详情读操作默认要求数据权限过滤。
- DAO 使用 `data_scope_sql` 时须做别名一致性检查。
- 核心业务表须有权限锚点字段（优先 `dept_id`，其次 `create_by`）。
- 自定义范围（`data_scope=2`）须明确 role → dept 数据来源。
- 禁止仅靠前端权限控制、无后端依赖校验。
- 新模块或查询范围变更的 PR 须包含「数据权限设计卡」。

## 输出标准

每次分析/评审输出应包含：

- 扩展目标与范围
- 架构方向与主要权衡
- 文件级实施映射（后端 + 前端）
- 权限闭环证明（接口 / 数据 / 前端）
- 分级质量门禁结果
- 验收用例（含数据范围回归场景）
- 假设、默认值与未决风险

## 参考文档

| 文档 | 说明 |
|------|------|
| `references/analysis-dimensions.md` | 架构分析维度 |
| `references/focus-checklist.md` | 焦点检查清单 |
| `references/backend-extension-spec.md` | 后端扩展规范 |
| `references/frontend-extension-spec.md` | 前端扩展规范 |
| `references/data-permission-architecture.md` | 数据权限架构 |
| `references/quality-gates.md` | 质量门禁 |
| `references/report-template.md` | 评审报告模板 |

## 使用方式

在 Cursor 中规划或评审 FluxPanel 相关功能时，通过 @ 引用本 Skill（`flux-extension-architect`），Agent 将按上述工作流与硬性规则执行分析与产出标准评审包。
