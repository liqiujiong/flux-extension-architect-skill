# Extension Analysis Dimensions

Use all dimensions. Do not skip any.

## 1. Domain And Scope
- What user problem is solved?
- Which actors and roles are involved?
- What is explicitly in scope and out of scope?

## 2. Data Model And Storage
- Which entities and relationships are introduced or changed?
- Which table fields are core keys and permission anchors?
- What migration or compatibility concerns exist?

## 3. API Contract
- Which endpoints are added or changed?
- What are request/response fields and validation rules?
- How is backward compatibility preserved?

## 4. Permission Architecture
- Which interface permissions are required?
- Which data scope strategy is selected?
- How are frontend permissions mapped to backend perms?

## 5. Frontend Interaction
- Which pages, dialogs, and operation buttons change?
- Which permissions control visibility and operation?
- What loading, error, and empty-state behavior is required?

## 6. Observability And Audit
- Which actions require operation logs?
- Which failure points require structured logging?
- How are key identifiers captured for traceability?

## 7. Delivery And Rollback
- What can be released incrementally?
- What is the rollback strategy for API and data changes?
- Which feature toggles or safeguards are needed?

## 8. Verification And Acceptance
- Which unit, integration, and permission tests are required?
- Which regression scenarios are mandatory?
- What are objective acceptance criteria?
