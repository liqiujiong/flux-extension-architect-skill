# Quality Gates (Strict + Graded)

## Gate Levels

### Level P0 (new module or core query-scope change)
- Must pass architecture consistency checks.
- Must pass permission closure checks (interface/data/frontend).
- Must pass dictionary governance checks for new enum/status/type fields.
- Must provide data permission design card.
- Must provide mandatory regression evidence.
- Merge is blocked on any missing mandatory item.

### Level P1 (feature update affecting existing module reads/writes)
- Must verify changed endpoints and permission mapping.
- Must retest impacted data-scope paths.
- Must verify dictionary changes when enum fields are added or modified.
- Must add/update tests for changed behavior.

### Level P2 (UI-only or non-scope-impacting updates)
- Must verify no permission key drift.
- Must verify no backend contract drift.
- Spot-check key flows.

## Mandatory Regression Scenarios
- Five-scope regression: all/custom/dept/dept+child/self.
- Multi-role combination behavior validation.
- Cross-department access probe.
- Export consistency with list/detail scope.
- Admin bypass versus non-admin restriction.

## Merge Blocking Rules
- Missing backend auth dependency for protected endpoint.
- Missing data-scope filtering on required read API.
- Alias mismatch that can break scope filtering.
- Missing dictionary SQL or frontend dict usage for new dictionary-backed fields.
- Missing design-card evidence for P0 changes.
