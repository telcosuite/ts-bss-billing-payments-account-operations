# Billing, Payments, And Account Operations P05 - Prepay Adjustment Refund Hardship And Collections Handoff Development Tasks

Suite: BSS Commercial

App: Billing, Payments, And Account Operations

App slug: `billing-payments-account-operations`

Implementation repository: `ts-bss-billing-payments-account-operations`

Phase: P05 - Prepay Adjustment Refund Hardship And Collections Handoff

Phase file: `P05-prepay-adjustment-refund-hardship-and-collections-handoff.md`

Phase rationale: Build the Prepay Balance, Collections And Adjustment, Refund Chargeback Deposit And Hardship Controls, Finance Subledger GL And Revenue Recognition capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work.

Phase exit gate: Billing, Payments, And Account Operations can execute the Prepay Balance, Collections And Adjustment, Refund Chargeback Deposit And Hardship Controls, Finance Subledger GL And Revenue Recognition workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests.

Out of scope for this phase: Runtime bootstrap is in P01; unrelated feature clusters and post-launch operations remain in their own phases.

Source tracker: [development-task-tracker.md](development-task-tracker.md)

Repository strategy: [TelcoSuite Repository Strategy](../../../../repository-strategy.md)

## Phase Coverage

- [Prepay Balance](../features/prepay-balance.md)
- [Collections And Adjustment](../features/collections-and-adjustment.md)
- [Refund Chargeback Deposit And Hardship Controls](../features/refund-chargeback-deposit-and-hardship-controls.md)
- [Finance Subledger GL And Revenue Recognition](../features/finance-subledger-gl-and-revenue-recognition.md)

## Phase Tasks

### DT-02-billing-payments-account-operations-P05-T001: Build Prepay Balance API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P0 |
| Source evidence | [Prepay Balance](../features/prepay-balance.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Prepay Balance |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/bsscommercial/billingpaymentsaccountoperations/PrepayBalanceController.java`, `billing_payments.prepay_balance`, `contracts/events/PrepayBalanceStateChangedEvent.json`, and `/api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance` |
| Dependencies | DT-02-billing-payments-account-operations-P01-T013 |
| Outputs | `PrepayBalanceController`, `PrepayBalanceService`, `billing_payments.prepay_balance` migration, `PrepayBalanceStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance` using TMF654, TMF666, TMF670, TMF676, TMF678, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Prepay Balance` state in `billing_payments.prepay_balance` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `PrepayBalanceStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: create or update, validate, close.
- Carry source details into code and tests for personas authorized operator and objects prepay balance; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `billing_payments.prepay_balance.id`, and appends `PrepayBalanceStateChangedEvent` to `billing_payments.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Prepay Balance` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `billing_payments.prepay_balance` is required.

#### Definition Of Done

- `PrepayBalanceController`, service, repository, DTOs, validation, error model, and migration for `billing_payments.prepay_balance` are committed under `ts-bss-billing-payments-account-operations`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance`, `billing_payments.prepay_balance`, and `PrepayBalanceStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance` return `403` and write a denial audit row instead of exposing `Prepay Balance` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `billing_payments.prepay_balance` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `PrepayBalanceStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Prepay Balance` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `billing_payments.prepay_balance` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `PrepayBalanceService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/prepay-balance` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `billing_payments.prepay_balance` columns and indexes; event replay tests validate `contracts/events/PrepayBalanceStateChangedEvent.json` and `billing_payments.event_outbox` ordering.

### DT-02-billing-payments-account-operations-P05-T002: Build Prepay Balance workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P1 |
| Source evidence | [Prepay Balance](../features/prepay-balance.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Prepay Balance |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/prepay-balance/`, `tests/e2e/prepay-balance.spec.ts`, Grafana panel `prepay-balance`, and `docs/operations-runbook.md#prepay-balance` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T001 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/prepay-balance/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas authorized operator.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows create or update, validate, close, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/billing-payments-account-operations/prepay-balance`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Prepay Balance` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `prepay-balance` refreshes, then it shows the metric and links to `docs/operations-runbook.md#prepay-balance`.

#### Definition Of Done

- `frontend/src/app/pages/prepay-balance/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/prepay-balance.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Prepay Balance` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Prepay Balance` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/prepay-balance.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-02-billing-payments-account-operations-P05-T003: Build Collections And Adjustment API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P0 |
| Source evidence | [Collections And Adjustment](../features/collections-and-adjustment.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Collections And Adjustment |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/bsscommercial/billingpaymentsaccountoperations/CollectionsAndAdjustmentController.java`, `billing_payments.collections_and_adjustment`, `contracts/events/CollectionsAndAdjustmentStateChangedEvent.json`, and `/api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T001 |
| Outputs | `CollectionsAndAdjustmentController`, `CollectionsAndAdjustmentService`, `billing_payments.collections_and_adjustment` migration, `CollectionsAndAdjustmentStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment` using TMF654, TMF666, TMF670, TMF676, TMF678, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Collections And Adjustment` state in `billing_payments.collections_and_adjustment` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `CollectionsAndAdjustmentStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: create or update, validate, close.
- Carry source details into code and tests for personas authorized operator and objects collections and adjustment; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `billing_payments.collections_and_adjustment.id`, and appends `CollectionsAndAdjustmentStateChangedEvent` to `billing_payments.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Collections And Adjustment` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `billing_payments.collections_and_adjustment` is required.

#### Definition Of Done

- `CollectionsAndAdjustmentController`, service, repository, DTOs, validation, error model, and migration for `billing_payments.collections_and_adjustment` are committed under `ts-bss-billing-payments-account-operations`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment`, `billing_payments.collections_and_adjustment`, and `CollectionsAndAdjustmentStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment` return `403` and write a denial audit row instead of exposing `Collections And Adjustment` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `billing_payments.collections_and_adjustment` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `CollectionsAndAdjustmentStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Collections And Adjustment` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `billing_payments.collections_and_adjustment` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `CollectionsAndAdjustmentService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/collections-and-adjustment` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `billing_payments.collections_and_adjustment` columns and indexes; event replay tests validate `contracts/events/CollectionsAndAdjustmentStateChangedEvent.json` and `billing_payments.event_outbox` ordering.

### DT-02-billing-payments-account-operations-P05-T004: Build Collections And Adjustment workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P1 |
| Source evidence | [Collections And Adjustment](../features/collections-and-adjustment.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Collections And Adjustment |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/collections-and-adjustment/`, `tests/e2e/collections-and-adjustment.spec.ts`, Grafana panel `collections-and-adjustment`, and `docs/operations-runbook.md#collections-and-adjustment` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T003 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/collections-and-adjustment/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas authorized operator.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows create or update, validate, close, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/billing-payments-account-operations/collections-and-adjustment`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Collections And Adjustment` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `collections-and-adjustment` refreshes, then it shows the metric and links to `docs/operations-runbook.md#collections-and-adjustment`.

#### Definition Of Done

- `frontend/src/app/pages/collections-and-adjustment/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/collections-and-adjustment.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Collections And Adjustment` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Collections And Adjustment` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/collections-and-adjustment.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-02-billing-payments-account-operations-P05-T005: Build Refund Chargeback Deposit And Hardship Controls API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P0 |
| Source evidence | [Refund Chargeback Deposit And Hardship Controls](../features/refund-chargeback-deposit-and-hardship-controls.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Refund Chargeback Deposit And Hardship Controls |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/bsscommercial/billingpaymentsaccountoperations/RefundChargebackDepositAndHardshipControlsController.java`, `billing_payments.refund_chargeback_deposit_and_hardship_controls`, `contracts/events/RefundChargebackDepositAndHardshipControlsStateChangedEvent.json`, and `/api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T003 |
| Outputs | `RefundChargebackDepositAndHardshipControlsController`, `RefundChargebackDepositAndHardshipControlsService`, `billing_payments.refund_chargeback_deposit_and_hardship_controls` migration, `RefundChargebackDepositAndHardshipControlsStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls` using TMF654, TMF666, TMF670, TMF676, TMF678, TMF681, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Refund Chargeback Deposit And Hardship Controls` state in `billing_payments.refund_chargeback_deposit_and_hardship_controls` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `RefundChargebackDepositAndHardshipControlsStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: create or update, validate, close.
- Carry source details into code and tests for personas authorized operator and objects refund chargeback deposit and hardship controls; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `billing_payments.refund_chargeback_deposit_and_hardship_controls.id`, and appends `RefundChargebackDepositAndHardshipControlsStateChangedEvent` to `billing_payments.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Refund Chargeback Deposit And Hardship Controls` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `billing_payments.refund_chargeback_deposit_and_hardship_controls` is required.

#### Definition Of Done

- `RefundChargebackDepositAndHardshipControlsController`, service, repository, DTOs, validation, error model, and migration for `billing_payments.refund_chargeback_deposit_and_hardship_controls` are committed under `ts-bss-billing-payments-account-operations`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls`, `billing_payments.refund_chargeback_deposit_and_hardship_controls`, and `RefundChargebackDepositAndHardshipControlsStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls` return `403` and write a denial audit row instead of exposing `Refund Chargeback Deposit And Hardship Controls` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `billing_payments.refund_chargeback_deposit_and_hardship_controls` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `RefundChargebackDepositAndHardshipControlsStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Refund Chargeback Deposit And Hardship Controls` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `billing_payments.refund_chargeback_deposit_and_hardship_controls` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `RefundChargebackDepositAndHardshipControlsService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/refund-chargeback-deposit-and-hardship-controls` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `billing_payments.refund_chargeback_deposit_and_hardship_controls` columns and indexes; event replay tests validate `contracts/events/RefundChargebackDepositAndHardshipControlsStateChangedEvent.json` and `billing_payments.event_outbox` ordering.

### DT-02-billing-payments-account-operations-P05-T006: Build Refund Chargeback Deposit And Hardship Controls workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P1 |
| Source evidence | [Refund Chargeback Deposit And Hardship Controls](../features/refund-chargeback-deposit-and-hardship-controls.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Refund Chargeback Deposit And Hardship Controls |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/refund-chargeback-deposit-and-hardship-controls/`, `tests/e2e/refund-chargeback-deposit-and-hardship-controls.spec.ts`, Grafana panel `refund-chargeback-deposit-and-hardship-controls`, and `docs/operations-runbook.md#refund-chargeback-deposit-and-hardship-controls` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T005 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/refund-chargeback-deposit-and-hardship-controls/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas authorized operator.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows create or update, validate, close, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/billing-payments-account-operations/refund-chargeback-deposit-and-hardship-controls`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Refund Chargeback Deposit And Hardship Controls` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `refund-chargeback-deposit-and-hardship-controls` refreshes, then it shows the metric and links to `docs/operations-runbook.md#refund-chargeback-deposit-and-hardship-controls`.

#### Definition Of Done

- `frontend/src/app/pages/refund-chargeback-deposit-and-hardship-controls/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/refund-chargeback-deposit-and-hardship-controls.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Refund Chargeback Deposit And Hardship Controls` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Refund Chargeback Deposit And Hardship Controls` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/refund-chargeback-deposit-and-hardship-controls.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-02-billing-payments-account-operations-P05-T007: Build Finance Subledger GL And Revenue Recognition API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P0 |
| Source evidence | [Finance Subledger GL And Revenue Recognition](../features/finance-subledger-gl-and-revenue-recognition.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Finance Subledger GL And Revenue Recognition |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/bsscommercial/billingpaymentsaccountoperations/FinanceSubledgerGlAndRevenueRecognitionController.java`, `billing_payments.finance_subledger_gl_and_revenue_recognition`, `contracts/events/FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent.json`, and `/api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T005 |
| Outputs | `FinanceSubledgerGlAndRevenueRecognitionController`, `FinanceSubledgerGlAndRevenueRecognitionService`, `billing_payments.finance_subledger_gl_and_revenue_recognition` migration, `FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition` using TMF635, TMF654, TMF666, TMF670, TMF676, TMF678, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Finance Subledger GL And Revenue Recognition` state in `billing_payments.finance_subledger_gl_and_revenue_recognition` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: create or update, validate, close.
- Carry source details into code and tests for personas authorized operator and objects finance subledger gl and revenue recognition; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `billing_payments.finance_subledger_gl_and_revenue_recognition.id`, and appends `FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent` to `billing_payments.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Finance Subledger GL And Revenue Recognition` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `billing_payments.finance_subledger_gl_and_revenue_recognition` is required.

#### Definition Of Done

- `FinanceSubledgerGlAndRevenueRecognitionController`, service, repository, DTOs, validation, error model, and migration for `billing_payments.finance_subledger_gl_and_revenue_recognition` are committed under `ts-bss-billing-payments-account-operations`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition`, `billing_payments.finance_subledger_gl_and_revenue_recognition`, and `FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition` return `403` and write a denial audit row instead of exposing `Finance Subledger GL And Revenue Recognition` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `billing_payments.finance_subledger_gl_and_revenue_recognition` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Finance Subledger GL And Revenue Recognition` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `billing_payments.finance_subledger_gl_and_revenue_recognition` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `FinanceSubledgerGlAndRevenueRecognitionService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/02-bss-commercial/billing-payments-account-operations/v1/finance-subledger-gl-and-revenue-recognition` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `billing_payments.finance_subledger_gl_and_revenue_recognition` columns and indexes; event replay tests validate `contracts/events/FinanceSubledgerGlAndRevenueRecognitionStateChangedEvent.json` and `billing_payments.event_outbox` ordering.

### DT-02-billing-payments-account-operations-P05-T008: Build Finance Subledger GL And Revenue Recognition workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P1 |
| Source evidence | [Finance Subledger GL And Revenue Recognition](../features/finance-subledger-gl-and-revenue-recognition.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Finance Subledger GL And Revenue Recognition |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/finance-subledger-gl-and-revenue-recognition/`, `tests/e2e/finance-subledger-gl-and-revenue-recognition.spec.ts`, Grafana panel `finance-subledger-gl-and-revenue-recognition`, and `docs/operations-runbook.md#finance-subledger-gl-and-revenue-recognition` |
| Dependencies | DT-02-billing-payments-account-operations-P05-T007 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/finance-subledger-gl-and-revenue-recognition/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas authorized operator.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows create or update, validate, close, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/billing-payments-account-operations/finance-subledger-gl-and-revenue-recognition`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Finance Subledger GL And Revenue Recognition` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `finance-subledger-gl-and-revenue-recognition` refreshes, then it shows the metric and links to `docs/operations-runbook.md#finance-subledger-gl-and-revenue-recognition`.

#### Definition Of Done

- `frontend/src/app/pages/finance-subledger-gl-and-revenue-recognition/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/finance-subledger-gl-and-revenue-recognition.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Finance Subledger GL And Revenue Recognition` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Finance Subledger GL And Revenue Recognition` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/finance-subledger-gl-and-revenue-recognition.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-02-billing-payments-account-operations-P05-T009: Prove Prepay Adjustment Refund Hardship And Collections Handoff release gate, replay, and handoff evidence

| Field | Value |
| --- | --- |
| Phase | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| Priority | P1 |
| Source evidence | [Prepay Balance](../features/prepay-balance.md), [Collections And Adjustment](../features/collections-and-adjustment.md), [Refund Chargeback Deposit And Hardship Controls](../features/refund-chargeback-deposit-and-hardship-controls.md), [Finance Subledger GL And Revenue Recognition](../features/finance-subledger-gl-and-revenue-recognition.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../billing-payments-account-operations.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Prepay Adjustment Refund Hardship And Collections Handoff |
| Build area | Test/Ops/Release/Event |
| Target artifact | `tests/release/prepay-adjustment-refund-hardship-and-collections-handoff.spec.ts`, `docs/release-notes/prepay-adjustment-refund-hardship-and-collections-handoff.md`, Grafana dashboard `prepay-adjustment-refund-hardship-and-collections-handoff`, and replay fixtures |
| Dependencies | DT-02-billing-payments-account-operations-P05-T002, DT-02-billing-payments-account-operations-P05-T004, DT-02-billing-payments-account-operations-P05-T006, DT-02-billing-payments-account-operations-P05-T008 |
| Outputs | Release-gate test, replay/reconciliation evidence, accessibility/security/performance reports, dashboard/runbook links, support handoff notes |
| Missing evidence | No |

#### Implementation Notes

- Create a release-gate checklist for `prepay-adjustment-refund-hardship-and-collections-handoff` covering Prepay Balance, Collections And Adjustment, Refund Chargeback Deposit And Hardship Controls, Finance Subledger GL And Revenue Recognition, with happy path, assisted path, negative path, edge cases, event replay, data reconciliation, security, accessibility, performance, and support evidence.
- Record producer and consumer acknowledgements for phase events, reconcile `billing_payments.event_outbox`, and link replay fixtures and correlation IDs.
- Update `docs/operations-runbook.md`, `docs/release-notes/prepay-adjustment-refund-hardship-and-collections-handoff.md`, and `development-task-tracker.md` with release evidence and unresolved blockers.

#### Acceptance Criteria

1. Given all tasks in `P05-prepay-adjustment-refund-hardship-and-collections-handoff.md` are complete, when `tests/release/prepay-adjustment-refund-hardship-and-collections-handoff.spec.ts` runs, then it returns exit code `0` and links evidence for UI, API, data, event, security, ops, and test gates.
2. Given a consumer rejects an event from `prepay-adjustment-refund-hardship-and-collections-handoff`, when replay is triggered, then the replay fixture preserves `$.correlationId`, `$.eventId`, and consumer acknowledgement state.
3. Given release notes are generated, when support reviews `docs/release-notes/prepay-adjustment-refund-hardship-and-collections-handoff.md`, then open blockers, rollback steps, runbook links, and ownership contacts are present.

#### Definition Of Done

- `tests/release/prepay-adjustment-refund-hardship-and-collections-handoff.spec.ts`, replay fixtures, dashboard/runbook links, and release notes are committed.
- Accessibility, security, contract, migration, event replay, performance, and operational-readiness evidence is linked from the tracker.
- Open blockers have owner, due date, target increment, and rollback or removal criteria.

#### Negative Scenarios

- Do not mark the phase Done if event replay, reconciliation, accessibility, security, or downstream acknowledgement evidence is missing.
- Do not release `prepay-adjustment-refund-hardship-and-collections-handoff` with unresolved cross-app writes, direct schema coupling, or stale source authority assumptions.
- Do not suppress failed release gates; record failures with owner, due date, and target increment.

#### Edge Cases

- Coordinated release gates may require downstream app windows; record scheduling, owner, and fallback route in release notes.
- Historical backfill, replay, bulk update, or migration repair runs must include preview, partial failure report, and rollback evidence.
- High-volume launch periods require dashboard thresholds, alert owners, queue back-pressure, and support escalation paths.

#### Test Expectations

- `tests/release/prepay-adjustment-refund-hardship-and-collections-handoff.spec.ts`, `mvn test`, OpenAPI/event replay tests, Flyway checks, Playwright/Cypress E2E, accessibility, security, and k6/performance gates pass.
- `docker compose config`, clean-checkout smoke, `helm lint`, Kubernetes dry-run, dashboard JSON validation, and runbook link checks pass.
- Tracker evidence links command output, PRs, screenshots, replay payloads, dashboards, release notes, and support handoff notes.
