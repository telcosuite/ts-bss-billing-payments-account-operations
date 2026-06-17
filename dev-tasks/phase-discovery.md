# Billing, Payments, And Account Operations Phase Discovery

## App Identity

| Field | Value |
| --- | --- |
| Suite | BSS Commercial |
| App | Billing, Payments, And Account Operations |
| App slug | `billing-payments-account-operations` |
| Implementation repo | `ts-bss-billing-payments-account-operations` |
| Database | `ts_bss_commercial` |
| Schema | `billing_payments` |
| APIs | TMF666, TMF678, TMF676, TMF670, TMF654 |
| Generated date | 2026-06-17 |
| Phase/task signature | 5 phases / P01=14, P02=5, P03=3, P04=3, P05=9 |

Phase count decision: 5 phases are evidence-derived from the current app-repo state, P01 runtime bootstrap requirements, and 8 build-ready feature files grouped by lifecycle, UI/API/data/event ownership, integration risk, and release gates.

Repeated skeleton audit: Evidence-derived and accepted for this app. Even when another app shares a phase/task-count signature, this discovery file cites this app's feature files, phase files, current repo state, and split/merge decisions; regenerate and split or merge phases if those inputs change.

## Input Evidence Inventory

| Evidence | Link | Status |
| --- | --- | --- |
| App implementation usage | [../implementation-file-usage.md](../implementation-file-usage.md) | Present |
| App README | [../README.md](../README.md) | Present |
| Modules and features | [../modules-and-features.md](../modules-and-features.md) | Present |
| Personas and journeys | [../personas-and-user-journeys.md](../personas-and-user-journeys.md) | Present |
| Suite data model | [../../data-model.md](../../data-model.md) | Present |
| Suite tech/UI guidance | [../../tech-and-ui-guidance.md](../../tech-and-ui-guidance.md) | Present |
| Suite implementation guide | [../../implementation-file-usage-guide.md](../../implementation-file-usage-guide.md) | Present |
| Repository strategy | [../../../../repository-strategy.md](../../../../repository-strategy.md) | Present |
| Feature: Bill Cycle Control And Invoice Presentment | [../features/bill-cycle-control-and-invoice-presentment.md](../features/bill-cycle-control-and-invoice-presentment.md) | Present |
| Feature: Billing Account | [../features/billing-account.md](../features/billing-account.md) | Present |
| Feature: Collections And Adjustment | [../features/collections-and-adjustment.md](../features/collections-and-adjustment.md) | Present |
| Feature: Customer Bill | [../features/customer-bill.md](../features/customer-bill.md) | Present |
| Feature: Finance Subledger GL And Revenue Recognition | [../features/finance-subledger-gl-and-revenue-recognition.md](../features/finance-subledger-gl-and-revenue-recognition.md) | Present |
| Feature: Payment And Payment Method | [../features/payment-and-payment-method.md](../features/payment-and-payment-method.md) | Present |
| Feature: Prepay Balance | [../features/prepay-balance.md](../features/prepay-balance.md) | Present |
| Feature: Refund Chargeback Deposit And Hardship Controls | [../features/refund-chargeback-deposit-and-hardship-controls.md](../features/refund-chargeback-deposit-and-hardship-controls.md) | Present |

## App Repository Current State Inventory

| Marker | Value |
| --- | --- |
| Repo exists | Yes |
| Runnable frontend: | No |
| Runnable backend: | No |
| App-specific migrations: | Yes |
| OpenAPI contract | Yes |
| Event contracts | Yes |
| Deployment skeleton | Yes |
| CI workflow | No |
| Current implementation conclusion: | Keep the zero-to-one foundation explicit until runnable frontend, backend, migrations, contracts, CI, deployment, and proof-slice evidence are all present in `ts-bss-billing-payments-account-operations`. |

## Feature/Module Cluster Analysis

| Feature | Feature ID | Source detail carried into tasks | Implementing task IDs | Phase |
| --- | --- | --- | --- | --- |
| [Bill Cycle Control And Invoice Presentment](../features/bill-cycle-control-and-invoice-presentment.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P02-T003, DT-02-billing-payments-account-operations-P02-T004, DT-02-billing-payments-account-operations-P02-T005 | P02 - Billing Account Lifecycle And Bill Cycle Operations |
| [Billing Account](../features/billing-account.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P02-T001, DT-02-billing-payments-account-operations-P02-T002, DT-02-billing-payments-account-operations-P02-T005 | P02 - Billing Account Lifecycle And Bill Cycle Operations |
| [Collections And Adjustment](../features/collections-and-adjustment.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P05-T003, DT-02-billing-payments-account-operations-P05-T004, DT-02-billing-payments-account-operations-P05-T009 | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| [Customer Bill](../features/customer-bill.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P03-T001, DT-02-billing-payments-account-operations-P03-T002, DT-02-billing-payments-account-operations-P03-T003 | P03 - Customer Bill Issuance And Bill Detail Workspace |
| [Finance Subledger GL And Revenue Recognition](../features/finance-subledger-gl-and-revenue-recognition.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P05-T007, DT-02-billing-payments-account-operations-P05-T008, DT-02-billing-payments-account-operations-P05-T009 | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| [Payment And Payment Method](../features/payment-and-payment-method.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P04-T001, DT-02-billing-payments-account-operations-P04-T002, DT-02-billing-payments-account-operations-P04-T003 | P04 - Payment Allocation And Payment Method Operations |
| [Prepay Balance](../features/prepay-balance.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P05-T001, DT-02-billing-payments-account-operations-P05-T002, DT-02-billing-payments-account-operations-P05-T009 | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |
| [Refund Chargeback Deposit And Hardship Controls](../features/refund-chargeback-deposit-and-hardship-controls.md) | F-billing-payments-account-operations-001 |  | DT-02-billing-payments-account-operations-P05-T005, DT-02-billing-payments-account-operations-P05-T006, DT-02-billing-payments-account-operations-P05-T009 | P05 - Prepay Adjustment Refund Hardship And Collections Handoff |

## Phase Decision Matrix

| Phase file | Task count | Evidence basis | Exit gate |
| --- | --- | --- | --- |
| [P01-from-scratch-app-foundation-and-delivery-runtime.md](P01-from-scratch-app-foundation-and-delivery-runtime.md) | 14 | The planning pack and local repo inspection do not prove a complete runnable implementation for `ts-bss-billing-payments-account-operations`; this from-scratch foundation phase creates the app-root runtime, governance, contracts, data, CI, deployment, observability, and proof slice before feature delivery. | A clean checkout of `ts-bss-billing-payments-account-operations` can run Angular and Spring Boot, apply `billing_payments` migrations, validate contracts/events, run Docker Compose and Helm checks, and prove one UI/API/data/event slice. |
| [P02-billing-account-lifecycle-and-bill-cycle-operations.md](P02-billing-account-lifecycle-and-bill-cycle-operations.md) | 5 | Build the Billing Account, Bill Cycle Control And Invoice Presentment capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Billing, Payments, And Account Operations can execute the Billing Account, Bill Cycle Control And Invoice Presentment workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests. |
| [P03-customer-bill-issuance-and-bill-detail-workspace.md](P03-customer-bill-issuance-and-bill-detail-workspace.md) | 3 | Build the Customer Bill capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Billing, Payments, And Account Operations can execute the Customer Bill workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests. |
| [P04-payment-allocation-and-payment-method-operations.md](P04-payment-allocation-and-payment-method-operations.md) | 3 | Build the Payment And Payment Method capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Billing, Payments, And Account Operations can execute the Payment And Payment Method workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests. |
| [P05-prepay-adjustment-refund-hardship-and-collections-handoff.md](P05-prepay-adjustment-refund-hardship-and-collections-handoff.md) | 9 | Build the Prepay Balance, Collections And Adjustment, Refund Chargeback Deposit And Hardship Controls, Finance Subledger GL And Revenue Recognition capability cluster for Billing, Payments, And Account Operations, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Billing, Payments, And Account Operations can execute the Prepay Balance, Collections And Adjustment, Refund Chargeback Deposit And Hardship Controls, Finance Subledger GL And Revenue Recognition workflows through UI, API, `billing_payments` persistence, outbox events, audit evidence, and release tests. |

## Split/Merge Decisions

- P01 remains the app-runtime foundation because the local repo inspection does not prove a complete runnable implementation for `ts-bss-billing-payments-account-operations`.
- Feature phases are grouped from source `features/*.md` files by lifecycle ownership, UI workbench/API/data/event coupling, security/privacy controls, observability, and release-test needs.
- Every feature file appears in task `Source evidence`, the tracker coverage matrix, and this discovery artifact; tracker-only feature references are not accepted as coverage.
- Generic phase names from older task packs are retired by this refresh and replaced with feature-derived phase names.

## Validator and Regeneration Notes

- Run `python3 telcosuite-skills/skills/tmf-dev-task-planner/scripts/validate_dev_tasks.py --root ts-planning/planning/suite-details/02-bss-commercial/billing-payments-account-operations --strict` after refresh.
- Re-run the mirror driver after validation so `ts-bss-billing-payments-account-operations/dev-tasks/` remains byte-identical to the planning source.
- If a source feature changes, refresh this app pack and verify phase count, feature coverage, task detail quality, and mirror parity again.
