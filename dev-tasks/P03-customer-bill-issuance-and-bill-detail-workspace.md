# Billing, Payments, And Account Operations P03 - Customer Bill Issuance And Bill Detail Workspace Development Tasks

Suite: BSS Commercial

App: Billing, Payments, And Account Operations

App slug: `billing-payments-account-operations`

Implementation repository: `ts-bss-billing-payments-account-operations`

Phase: P03 - Customer Bill Issuance And Bill Detail Workspace

Phase file: `P03-customer-bill-issuance-and-bill-detail-workspace.md`

Phase rationale: Build the Customer Bill capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work.

Phase exit gate: Billing, Payments, And Account Operations can execute the Customer Bill workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests.

Out of scope for this phase: Runtime bootstrap is in P01; unrelated feature clusters and post-launch operations remain in their own phases.

Source tracker: [development-task-tracker.md](development-task-tracker.md)

Repository strategy: [TelcoSuite Repository Strategy](../../../../repository-strategy.md)

## Phase Coverage

- [Customer Bill](../features/customer-bill.md)

## Phase Tasks

### DT-02-billing-payments-account-operations-P03-T001: Build Customer Bill API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P03 - Customer Bill Issuance And Bill Detail Workspace |
| Priority | P0 |
| Source evidence | [Customer Bill](../features/customer-bill.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Customer Bill |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/bsscommercial/billingpaymentsaccountoperations/CustomerBillController.java`, `billing_payments.customer_bill`, `contracts/events/CustomerBillStateChangedEvent.json`, and `/api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill` |
| Dependencies | DT-02-billing-payments-account-operations-P01-T013 |
| Outputs | `CustomerBillController`, `CustomerBillService`, `billing_payments.customer_bill` migration, `CustomerBillStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill` using TMF654, TMF666, TMF670, TMF676, TMF678, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Customer Bill` state in `billing_payments.customer_bill` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `CustomerBillStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: create or update, validate, close.
- Carry source details into code and tests for personas authorized operator and objects customer bill; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `billing_payments.customer_bill.id`, and appends `CustomerBillStateChangedEvent` to `billing_payments.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Customer Bill` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `billing_payments.customer_bill` is required.

#### Definition Of Done

- `CustomerBillController`, service, repository, DTOs, validation, error model, and migration for `billing_payments.customer_bill` are committed under `ts-bss-billing-payments-account-operations`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill`, `billing_payments.customer_bill`, and `CustomerBillStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill` return `403` and write a denial audit row instead of exposing `Customer Bill` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `billing_payments.customer_bill` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `CustomerBillStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Customer Bill` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `billing_payments.customer_bill` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `CustomerBillService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/customer-bill` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `billing_payments.customer_bill` columns and indexes; event replay tests validate `contracts/events/CustomerBillStateChangedEvent.json` and `billing_payments.event_outbox` ordering.

### DT-02-billing-payments-account-operations-P03-T002: Build Customer Bill workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P03 - Customer Bill Issuance And Bill Detail Workspace |
| Priority | P1 |
| Source evidence | [Customer Bill](../features/customer-bill.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Customer Bill |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/customer-bill/`, `tests/e2e/customer-bill.spec.ts`, Grafana panel `customer-bill`, and `docs/operations-runbook.md#customer-bill` |
| Dependencies | DT-02-billing-payments-account-operations-P03-T001 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/customer-bill/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas authorized operator.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows create or update, validate, close, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/billing-payments-account-operations/customer-bill`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Customer Bill` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `customer-bill` refreshes, then it shows the metric and links to `docs/operations-runbook.md#customer-bill`.

#### Definition Of Done

- `frontend/src/app/pages/customer-bill/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/customer-bill.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Customer Bill` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Customer Bill` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/customer-bill.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-02-billing-payments-account-operations-P03-T003: Prove Customer Bill Issuance And Bill Detail Workspace release gate, replay, and handoff evidence

| Field | Value |
| --- | --- |
| Phase | P03 - Customer Bill Issuance And Bill Detail Workspace |
| Priority | P1 |
| Source evidence | [Customer Bill](../features/customer-bill.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Customer Bill Issuance And Bill Detail Workspace |
| Build area | Test/Ops/Release/Event |
| Target artifact | `tests/release/customer-bill-issuance-and-bill-detail-workspace.spec.ts`, `docs/release-notes/customer-bill-issuance-and-bill-detail-workspace.md`, Grafana dashboard `customer-bill-issuance-and-bill-detail-workspace`, and replay fixtures |
| Dependencies | DT-02-billing-payments-account-operations-P03-T002 |
| Outputs | Release-gate test, replay/reconciliation evidence, accessibility/security/performance reports, dashboard/runbook links, support handoff notes |
| Missing evidence | No |

#### Implementation Notes

- Create a release-gate checklist for `customer-bill-issuance-and-bill-detail-workspace` covering Customer Bill, with happy path, assisted path, negative path, edge cases, event replay, data reconciliation, security, accessibility, performance, and support evidence.
- Record producer and consumer acknowledgements for phase events, reconcile `billing_payments.event_outbox`, and link replay fixtures and correlation IDs.
- Update `docs/operations-runbook.md`, `docs/release-notes/customer-bill-issuance-and-bill-detail-workspace.md`, and `development-task-tracker.md` with release evidence and unresolved blockers.

#### Acceptance Criteria

1. Given all tasks in `P03-customer-bill-issuance-and-bill-detail-workspace.md` are complete, when `tests/release/customer-bill-issuance-and-bill-detail-workspace.spec.ts` runs, then it returns exit code `0` and links evidence for UI, API, data, event, security, ops, and test gates.
2. Given a consumer rejects an event from `customer-bill-issuance-and-bill-detail-workspace`, when replay is triggered, then the replay fixture preserves `$.correlationId`, `$.eventId`, and consumer acknowledgement state.
3. Given release notes are generated, when support reviews `docs/release-notes/customer-bill-issuance-and-bill-detail-workspace.md`, then open blockers, rollback steps, runbook links, and ownership contacts are present.

#### Definition Of Done

- `tests/release/customer-bill-issuance-and-bill-detail-workspace.spec.ts`, replay fixtures, dashboard/runbook links, and release notes are committed.
- Accessibility, security, contract, migration, event replay, performance, and operational-readiness evidence is linked from the tracker.
- Open blockers have owner, due date, target increment, and rollback or removal criteria.

#### Negative Scenarios

- Do not mark the phase Done if event replay, reconciliation, accessibility, security, or downstream acknowledgement evidence is missing.
- Do not release `customer-bill-issuance-and-bill-detail-workspace` with unresolved cross-app writes, direct schema coupling, or stale source authority assumptions.
- Do not suppress failed release gates; record failures with owner, due date, and target increment.

#### Edge Cases

- Coordinated release gates may require downstream app windows; record scheduling, owner, and fallback route in release notes.
- Historical backfill, replay, bulk update, or migration repair runs must include preview, partial failure report, and rollback evidence.
- High-volume launch periods require dashboard thresholds, alert owners, queue back-pressure, and support escalation paths.

#### Test Expectations

- `tests/release/customer-bill-issuance-and-bill-detail-workspace.spec.ts`, `mvn test`, OpenAPI/event replay tests, Flyway checks, Playwright/Cypress E2E, accessibility, security, and k6/performance gates pass.
- `docker compose config`, clean-checkout smoke, `helm lint`, Kubernetes dry-run, dashboard JSON validation, and runbook link checks pass.
- Tracker evidence links command output, PRs, screenshots, replay payloads, dashboards, release notes, and support handoff notes.
