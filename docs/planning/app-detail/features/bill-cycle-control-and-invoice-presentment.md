| Field | Value |
| --- | --- |
| Feature ID | F-billing-payments-account-operations-001 |
| App | Billing Payments Account Operations |
| App slug | `billing-payments-account-operations` |
| Module | Billing, Payments, And Account Operations |
| Source slice | [modules-and-features.md](../modules-and-features.md) |
| Last refined | 2026-06-15 |
| Refiner verdict | Build-ready |

# Bill Cycle Control And Invoice Presentment Feature Specification


Reviewed: 2026-06-07

Suite: BSS Commercial

App: [Billing, Payments, And Account Operations](../README.md)

Source module detail: [Modules And Features](../modules-and-features.md)

Source gap review: [E2E Feature Gap Assessment](../../../e2e-feature-gap-assessment.md)

Feature area slug: `bill-cycle-control-and-invoice-presentment`

E2E gap severity: Critical

## Feature Intent

Operate bill cycles, bill quality gates, rerun controls, invoice rendering, tax invoice compliance, and customer presentment.

Bill Cycle Control And Invoice Presentment turns that intent into a controlled billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition capability: the app owns the bill cycle control and invoice presentment lifecycle state, validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period, and leaves usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data consumers with auditable status rather than spreadsheet or direct-database workarounds.

## Personas Covered

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

## Persona-Specific Outcomes

| Persona | Decision rights and jobs-to-be-done | Feature outcome |
| --- | --- | --- |
| Billing operations user | Reviews and reconciles bill cycle control and invoice presentment financial state, postings, adjustments, settlement, and audit evidence. | Billing operations user can complete, approve, monitor, or audit bill cycle control and invoice presentment with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Care agent | Uses bill cycle control and invoice presentment context to resolve customer care, complaint, billing, order, or assurance handoff without bypassing the owning app. | Care agent can complete, approve, monitor, or audit bill cycle control and invoice presentment with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Finance user | Reviews and reconciles bill cycle control and invoice presentment financial state, postings, adjustments, settlement, and audit evidence. | Finance user can complete, approve, monitor, or audit bill cycle control and invoice presentment with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Collections user | Scores, holds, releases, disputes, or recovers bill cycle control and invoice presentment risk state under approved policy and customer protection controls. | Collections user can complete, approve, monitor, or audit bill cycle control and invoice presentment with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Customer | Views and submits bill cycle control and invoice presentment requests only for their own customer account, consent state, bill/order/usage context, and permitted evidence. | Customer can complete, approve, monitor, or audit bill cycle control and invoice presentment with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |

## Core User Journeys Covered

| Step | User or system intent | Feature responsibility |
| ---: | --- | --- |
| 1 | Intake request, signal, or dependency from the upstream app, user, partner, event, or API consumer. | Bill Cycle Control And Invoice Presentment captures the intake and source authority for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records bill cycle control and invoice presentment state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 2 | Validate eligibility, policy, commercial, operational, regulatory, and data-quality context. | Bill Cycle Control And Invoice Presentment validates eligibility, policy, and dependency state for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records bill cycle control and invoice presentment state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 3 | Coordinate downstream tasks, events, notifications, and state transitions across the owning apps. | Bill Cycle Control And Invoice Presentment orchestrates owned lifecycle updates and downstream handoffs for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records bill cycle control and invoice presentment state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 4 | Resolve exceptions, retries, approvals, compensation, or manual intervention. | Bill Cycle Control And Invoice Presentment routes fallout, approval, retry, cancellation, or compensation work for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records bill cycle control and invoice presentment state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 5 | Close the journey with reconciliation, evidence, reporting, and feedback into planning or operations. | Bill Cycle Control And Invoice Presentment publishes completion, reconciliation, and evidence events for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records bill cycle control and invoice presentment state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |

## Missing Use Cases And Scenarios

| Scenario | Required behavior |
| --- | --- |
| Happy path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: Billing operations validates billing account and bill cycle readiness, releases compliant invoices, receives payments, allocates cash, and posts subledger/GL and revenue recognition evidence. |
| Assisted path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: A care agent explains bill line items, takes approved payments or adjustments, and opens billing dispute or hardship workflow with masked payment data. |
| Automated path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: Payment gateway, charging engine, tax engine, or ERP sends callbacks and receives idempotent allocation, reversal, posting, and reconciliation events. |
| Customer path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: A customer views a bill, invoice, payment method, prepay balance, refund, deposit, or hardship plan through self-care with localized and accessible presentation. |
| Back-office path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: Billing analyst and finance controller reconcile bill runs, chargebacks, refunds, write-offs, deposits, AR, GL, revenue recognition, and close exceptions. |
| Collections path | Bill Cycle Control And Invoice Presentment must support this path for bill cycle control and invoice presentment: Collections receives overdue balance, dunning state, payment promise, hardship protection, restriction eligibility, and reconnection evidence without changing bill/payment masters. |

## Core Workflow And Control Points

| Control point | Required behavior | Evidence captured |
| --- | --- | --- |
| Trigger | Start bill cycle control and invoice presentment from a billing account change, bill cycle start, usage/rating feed, invoice release, payment event, refund/chargeback request, adjustment, collections trigger, hardship case, prepay top-up, or finance close run with source channel, actor, tenant, customer/account/product/order references where applicable, and idempotency key. | Intake timestamp, source, actor, correlation ID, initiating record, and submitted payload hash. |
| Validation | Validate billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period before mutating billing account/bill/payment/prepay/finance context state or handing work to another app. | Validation result, policy decision, source authority, missing fields, and permitted next action. |
| Orchestration | Coordinate Usage and Charging for rated usage and balances, tax engines for invoice taxes, payment gateways and token vaults, Credit/Fraud/Collections for dunning and restrictions, Customer 360 and Care for bill inquiries, Order Management for order-to-bill actions, finance/ERP for AR/GL/revenue recognition, partner settlement, and DWH/lakehouse using APIs, events, workflow tasks, or governed projections while preserving app mastership: Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities. | Downstream owner, dependency state, request/response reference, retry counter, and event IDs. |
| Exception | Route bill cycle control and invoice presentment fallout, policy failures, manual approvals, retries, rollback, compensation, and cancellation to accountable queues. | Queue owner, severity, due date, customer/revenue/compliance impact, reason code, comments, and evidence links. |
| Completion | Close bill cycle control and invoice presentment only when owned lifecycle state, downstream handoffs, reconciliation, notifications, and reporting facts are complete or explicitly excepted. | Completion state, before/after values, reconciliation result, notification status, approver, and closure event. |
| Evidence | Preserve audit and regulatory evidence for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency with role-aware masking and retention/legal-hold controls. | Audit log, policy version, document/evidence reference, retention class, legal hold flag, and export controls. |

## Detailed Feature Backlog

| Feature ID | Feature | Parent feature area | Priority guidance |
| --- | --- | --- | --- |
| F-bill-cycle-control-and-invoice-presentment-01 | Bill cycle calendar | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when bill cycle calendar gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |
| F-bill-cycle-control-and-invoice-presentment-02 | Bill quality gate | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when bill quality gate gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |
| F-bill-cycle-control-and-invoice-presentment-03 | Rerun and suppression control | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when rerun and suppression control gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |
| F-bill-cycle-control-and-invoice-presentment-04 | Invoice rendering and delivery | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when invoice rendering and delivery gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |
| F-bill-cycle-control-and-invoice-presentment-05 | Tax invoice evidence | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when tax invoice evidence gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |
| F-bill-cycle-control-and-invoice-presentment-06 | Customer bill presentment status | Bill Cycle Control And Invoice Presentment | P1: closes Critical E2E gap when customer bill presentment status gates usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; implementation must include API/event contract, exception queue, and evidence before pilot exit. |

## Acceptance Criteria

### Intake and ownership

Feature detail: Accept requests from UI, API, event, workflow, partner channel, or upstream app while assigning a clear owner and lifecycle state. For bill cycle control and invoice presentment, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-bill-cycle-control-and-invoice-presentment-01-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete intake and ownership for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-bill-cycle-control-and-invoice-presentment-01-02 Assisted path:** Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in intake and ownership, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-bill-cycle-control-and-invoice-presentment-01-03 Automated path:** Given an API consumer or event submits bill cycle control and invoice presentment data for intake and ownership, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-bill-cycle-control-and-invoice-presentment-01-04 Exception path:** Given validation, downstream response, or compliance control fails during intake and ownership, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-bill-cycle-control-and-invoice-presentment-01-05 Completion evidence:** Given intake and ownership is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Validation and policy control

Feature detail: Validate required data, source authority, permissions, consent, regulatory policy, tenant/geography boundary, and dependency references. For bill cycle control and invoice presentment, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-bill-cycle-control-and-invoice-presentment-02-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete validation and policy control for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-bill-cycle-control-and-invoice-presentment-02-02 Assisted path:** Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in validation and policy control, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-bill-cycle-control-and-invoice-presentment-02-03 Automated path:** Given an API consumer or event submits bill cycle control and invoice presentment data for validation and policy control, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-bill-cycle-control-and-invoice-presentment-02-04 Exception path:** Given validation, downstream response, or compliance control fails during validation and policy control, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-bill-cycle-control-and-invoice-presentment-02-05 Completion evidence:** Given validation and policy control is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Cross-app orchestration

Feature detail: Coordinate APIs, events, tasks, projections, notifications, and retry behavior with each downstream owner. For bill cycle control and invoice presentment, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-bill-cycle-control-and-invoice-presentment-03-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete cross-app orchestration for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-bill-cycle-control-and-invoice-presentment-03-02 Assisted path:** Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in cross-app orchestration, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-bill-cycle-control-and-invoice-presentment-03-03 Automated path:** Given an API consumer or event submits bill cycle control and invoice presentment data for cross-app orchestration, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-bill-cycle-control-and-invoice-presentment-03-04 Exception path:** Given validation, downstream response, or compliance control fails during cross-app orchestration, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-bill-cycle-control-and-invoice-presentment-03-05 Completion evidence:** Given cross-app orchestration is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Exception and compensation

Feature detail: Route fallout, partial failure, rollback, cancellation, amendment, or compensation to accountable queues with evidence. For bill cycle control and invoice presentment, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-bill-cycle-control-and-invoice-presentment-04-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete exception and compensation for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-bill-cycle-control-and-invoice-presentment-04-02 Assisted path:** Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in exception and compensation, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-bill-cycle-control-and-invoice-presentment-04-03 Automated path:** Given an API consumer or event submits bill cycle control and invoice presentment data for exception and compensation, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-bill-cycle-control-and-invoice-presentment-04-04 Exception path:** Given validation, downstream response, or compliance control fails during exception and compensation, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-bill-cycle-control-and-invoice-presentment-04-05 Completion evidence:** Given exception and compensation is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Reporting and closure

Feature detail: Close only after reconciliation, evidence capture, operational metrics, and downstream completion signals are available. For bill cycle control and invoice presentment, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-bill-cycle-control-and-invoice-presentment-05-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete reporting and closure for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-bill-cycle-control-and-invoice-presentment-05-02 Assisted path:** Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in reporting and closure, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-bill-cycle-control-and-invoice-presentment-05-03 Automated path:** Given an API consumer or event submits bill cycle control and invoice presentment data for reporting and closure, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-bill-cycle-control-and-invoice-presentment-05-04 Exception path:** Given validation, downstream response, or compliance control fails during reporting and closure, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-bill-cycle-control-and-invoice-presentment-05-05 Completion evidence:** Given reporting and closure is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

## Negative Scenarios

| Scenario | Expected behavior |
| --- | --- |
| Unauthorized bill cycle control and invoice presentment access or mutation | Reject the request, mask billing account/bill/payment/prepay/finance context data, and record actor, channel, tenant, policy decision, and correlation ID. |
| Missing mandatory bill cycle control and invoice presentment context | Keep bill cycle control and invoice presentment in draft, blocked, or rejected state with field-level errors for billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and do not publish downstream handoff events. |
| Invalid bill cycle control and invoice presentment lifecycle transition | Block the transition, show allowed next states, preserve prior state/version, and require permitted role or automated policy to resubmit. |
| Conflicting master data for bill cycle control and invoice presentment | Route correction to the owning app named by data mastery and prevent local shadow updates to customer, catalog, order, inventory, billing, usage, risk, or partner masters. |
| Downstream usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency unavailable | Fail fast for synchronous decisions or queue controlled retry with owner, due date, backoff policy, and customer/revenue impact flag. |
| Duplicate, stale, or out-of-order bill cycle control and invoice presentment request | Use optimistic locking, event version, source timestamp, and idempotency key so retries cannot duplicate work or corrupt current state. |
| Policy, consent, regulatory, or geography breach | Stop the transaction, preserve the policy decision, notify only permitted roles, and enforce PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency. |
| Manual override for bill cycle control and invoice presentment | Require approval role, reason code, expiry, compensating action, post-action review, and searchable audit evidence. |
| Sensitive evidence requested for bill cycle control and invoice presentment | Mask or deny restricted KYC, payment, fraud, complaint, usage, tax, or legal evidence while keeping operational task status visible. |
| Reconciliation mismatch after bill cycle control and invoice presentment completion | Reopen or hold closure until usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data state agrees or an approved exception with finance/customer/compliance impact is recorded. |

## Edge Cases

| Edge case | Expected handling |
| --- | --- |
| Bulk or project-scale bill cycle control and invoice presentment processing | Support validation preview, staged commit, partial failure report, throttling, replay, and rollback or repair plan before production release. |
| Long-running bill cycle control and invoice presentment journey | Expose waiting, blocked, retrying, escalated, compensated, corrected, and completed states with timers, owners, and customer/revenue impact. |
| Historical bill cycle control and invoice presentment correction | Allow effective-dated correction with reason, old/new values, approver, downstream recalculation trigger, and retention/legal-hold validation. |
| Multi-brand, multi-tenant, or data-residency boundary | Apply tenant, brand, market, geography, language, currency, and data-residency controls consistently in UI, API, event, and reporting paths. |
| High-volume operational period for bill cycle control and invoice presentment | Protect critical flows with pagination, async export, queue back-pressure, circuit breakers, dashboard filters, and runbook-defined load-shedding. |
| Late usage after bill cycle close | Route to rebill, adjustment, or next-cycle treatment with customer-bill evidence and finance impact visible. |
| Payment gateway duplicate callback | Use idempotency and gateway reference to prevent duplicate payment allocation, refund, or reversal. |
| Tax jurisdiction correction | Preserve original tax invoice evidence, create corrected bill/credit note path, and trigger finance and customer communication events. |
| Hardship or vulnerable customer active | Block automated restriction/dunning escalation and require permitted hardship treatment evidence. |
| Finance period closed | Prevent backdated posting without finance-controller approval, reason code, and controlled subledger/GL adjustment. |

## Suite Gap Review Closure Addendum

Source review: [02 Bss Commercial Gap Review](../../../../suite-gap-reviews/02-bss-commercial-gap-review.md)

This addendum applies the suite gap-review findings tied to this feature file. It supplements the baseline feature specification and should be carried into epic, story, API, event, data, and test refinement.

### Review Backlog Items Addressed

| Severity | Gap-review item | Closure expectation |
| --- | --- | --- |
| High | Finance close exception cockpit and reconciliation proof. | Add concrete happy path, negative path, edge-case, API/event/data control, reporting, and test evidence for this feature area. |

### Acceptance Criteria Additions

1. Given a customer disputes a bill line, when collections evaluates dunning or restriction, then disputed amounts are excluded or treated under approved policy and the care agent sees bill-line source, reason, owner, and resolution deadline.
2. Given a bill cycle is ready to close, when usage, rating, tax, payment, adjustment, subledger, or GL reconciliation has unresolved mismatches, then close is blocked or approved as an exception with finance owner, materiality, and expiry.
3. Given a payment callback is received twice or out of order, when the gateway reference and idempotency key match prior processing, then no duplicate allocation, refund, or receipt is created.

### Negative Scenario Additions

1. Tax jurisdiction changes after invoice release; preserve original invoice evidence and require corrected invoice/credit note and finance approval.
2. A hardship flag is active and automated dunning tries to restrict service; block the action and route to hardship policy owner.
3. Prepay balance reservation expires while a payment reversal arrives; prevent negative balance corruption and create reconciliation fallout.

### API, Event, Data, And Reporting Updates

- Add or refine command/query APIs so the owning app remains the system of record and consumers do not bypass app APIs.
- Add lifecycle events for the reviewed gap, including created, validated, blocked, approved, completed, failed, corrected, replayed, and reconciliation-failed variants where applicable.
- Capture idempotency keys, correlation IDs, source freshness, lineage, confidence, policy version, owner, SLA/OLA timers, and audit evidence.
- Add dashboards or operational reports for aging, failure reason, confidence/quality, consumer impact, exception backlog, and closure proof.
- Extend the test approach with happy-path, negative, edge-case, contract, event replay, data reconciliation, security, accessibility, and operational-readiness tests for the listed review items.

## API, Event, And Data Requirements

Related APIs and API areas: [TMF678](../../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill), [TMF681](../../../../../references/tmforum-open-apis/openapi-specs/TMF681_Communication), [TMF667](../../../../../references/tmforum-open-apis/openapi-specs/TMF667_Document), [TMF666](../../../../../references/tmforum-open-apis/openapi-specs/TMF666_AccountManagement)

TMF API fit and extension notes:

- Use TMF678, TMF681, TMF667, TMF666 for the TMF resource areas already identified in this feature specification; do not replace those resources with local-only contracts when the TMF API covers the lifecycle or query behavior.
- Extension APIs are allowed only for bill run quality gates, invoice rendering/presentment, subledger/GL close control, revenue recognition policy, hardship workflow, chargeback evidence, deposit lifecycle, and tax invoice evidence where no direct TMF resource exists; each extension must be explicitly labelled non-TMF, documented with OpenAPI, and aligned to TMF-style id, href, lifecycle state, relatedParty, relatedEntity, error, pagination, and event-envelope patterns where practical.
- Command APIs for bill cycle control and invoice presentment must cover create/initiate, validate, update, approve/reject, hold/release, cancel, rollback or compensate where applicable, retry, correct, and close.
- Query APIs for bill cycle control and invoice presentment must cover search, detail, timeline, related billing account/bill/payment/prepay/finance context references, dependency graph, work queue, metrics, and audit/evidence retrieval with role-aware masking.
- Domain events for bill cycle control and invoice presentment must include created, validated, blocked, approved, rejected, updated, handoff requested, exception raised, exception resolved, cancelled, compensated, completed, corrected, and reconciliation failed where the lifecycle uses those states.

Data and ownership requirements:

- Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities; other apps consume bill cycle control and invoice presentment state through APIs, events, governed projections, workflow tasks, or certified data products.
- Store source channel, actor, tenant/brand/market, external references, status reason, timestamps, policy decision, before/after values, related customer/account/product/order/bill/usage/ticket references where applicable, and evidence links.
- Keep read projections, analytics extracts, and DWH/lakehouse outputs separate from operational writes so Bill Cycle Control And Invoice Presentment does not create shadow mastership.
- Provide reconciliation outputs that prove usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependencies have completed, failed, or remain explicitly owned.

Integration and handoff requirements:

- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with Usage and Charging for rated usage and balances through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with tax engines for invoice taxes through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with payment gateways and token vaults through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with Credit/Fraud/Collections for dunning and restrictions through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with Customer 360 and Care for bill inquiries through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with Order Management for order-to-bill actions through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with finance/ERP for AR/GL/revenue recognition through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with partner settlement through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Bill Cycle Control And Invoice Presentment must exchange bill cycle control and invoice presentment state or evidence with DWH/lakehouse through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.

## Non-Functional Requirements

- Scale and latency: bill and payment query P95 below 500 ms, payment status callback processing within agreed gateway SLA, 99.9% availability for payment and bill-view APIs, resilient bill-cycle batch restart, immutable finance audit evidence, and localized invoice rendering.
- Availability and resilience: Bill Cycle Control And Invoice Presentment must support 99.9% or higher availability for interactive and API paths that gate usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence, with queue back-pressure, retry, replay, and circuit-breaker controls for downstream integrations.
- Auditability and retention: bill cycle control and invoice presentment history must preserve actor, channel, reason, old/new value, policy version, approval, event ID, external reference, and retention/legal-hold class for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency.
- Localization and accessibility: Bill Cycle Control And Invoice Presentment user tasks, customer/partner communications, currency/date formats, invoice or offer disclosures where applicable, and error messages must support market localization, WCAG-aligned accessibility, and role-aware data masking.
- Data protection: API, event, export, and dashboard paths must enforce tenant isolation, data residency, purpose limitation, least privilege, field-level masking, and secure evidence storage for billing account/bill/payment/prepay/finance context.

## Compliance, Security, And Privacy

- Bill Cycle Control And Invoice Presentment must enforce PCI token handling for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce payment mandate evidence for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce tax invoice compliance for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce refund/chargeback evidence for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce hardship and vulnerable-customer protections for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce revenue recognition control for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce finance close audit for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce retention for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce legal hold for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce localization for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce accessibility for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce tenant isolation for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Bill Cycle Control And Invoice Presentment must enforce data residency for bill cycle control and invoice presentment records, UI actions, API payloads, events, reports, and evidence exports.
- Privileged actions on bill cycle control and invoice presentment require role-based approval, reason code, expiration where relevant, and post-action review by billing operations, payments operations, revenue accounting, collections operations, and finance control.
- Sensitive billing account/bill/payment/prepay/finance context evidence must be masked in search, timelines, exports, analytics, partner views, and operational dashboards unless the persona has a permitted purpose.

## Observability And Operations

- Metrics: track bill cycle control and invoice presentment intake volume, validation failure rate, policy rejection rate, automation rate, manual override rate, queue aging, retry count, cancellation/rollback/compensation count, reconciliation mismatch, and completion quality by tenant, market, channel, product, partner, and owning team.
- Queues: provide work queues for draft, pending validation, pending approval, blocked dependency, exception, retrying, customer-impacting, revenue-impacting, compliance-impacting, compensated, corrected, completed, and archived bill cycle control and invoice presentment records.
- Alerts: alert billing operations, payments operations, revenue accounting, collections operations, and finance control when bill cycle control and invoice presentment queue aging, downstream failure, event publication failure, reconciliation mismatch, abnormal policy override, or SLA/OLA breach risk exceeds threshold.
- Runbooks: document triage, retry, replay, rollback, compensation, manual approval, customer/partner communication, evidence export, and reconciliation steps for Bill Cycle Control And Invoice Presentment.
- Replay and reconciliation: support idempotent replay for events, files, callbacks, and workflow tasks so Bill Cycle Control And Invoice Presentment can recover without duplicate billing account/bill/payment/prepay/finance context state or lost audit history.
- Ownership: billing operations, payments operations, revenue accounting, collections operations, and finance control owns first-line operational health; architecture, data, security, and compliance teams own policy and conformance review for the bill cycle control and invoice presentment lifecycle.

## Test Approach

| Test layer | Required coverage |
| --- | --- |
| Unit tests | Field rules, lifecycle transitions, policy decisions, duplicate detection, effective dating, masking, and billing account/bill/payment/prepay/finance context state calculations for bill cycle control and invoice presentment. |
| API contract tests | Commands, queries, errors, idempotency, pagination, filtering, version compatibility, and TMF-aligned payloads for TMF678, TMF681, TMF667, TMF666 plus documented extension APIs. |
| Event contract tests | bill cycle control and invoice presentment event names, payload shape, changed fields, correlation ID, idempotency key, ordering metadata, replay behavior, and subscriber compatibility. |
| Workflow tests | Happy path, assisted path, automated path, partner/channel path, approval, exception, timeout, retry, cancellation, rollback, compensation, correction, and closure for billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition. |
| Integration tests | Handoffs with usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data owners, external provider unavailability, eventual consistency, reconciliation, and no direct database access. |
| Security and privacy tests | Tenant isolation, role permissions, consent/purpose checks, sensitive-data masking, malicious payloads, audit logging, legal hold, retention, and export controls for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency. |
| Data tests | Source authority, referential integrity, historical correction, projection refresh, DWH/lakehouse extract, reporting metrics, and data-quality stewardship for billing account/bill/payment/prepay/finance context. |
| Performance and resilience tests | Search, list, bulk import/export, queue throughput, API throughput, event replay, retry storm, downstream outage, and batch recovery under realistic telecom volumes. |
| Operational acceptance tests | Dashboards, alerts, runbooks, queue ownership, SLA/OLA reporting, reconciliation reports, and evidence export for billing operations, payments operations, revenue accounting, collections operations, and finance control. |

## Out Of Scope And Dependencies

- Bill Cycle Control And Invoice Presentment does not master entities assigned to another app in the data mastery document; it stores only its app-owned bill cycle control and invoice presentment state, transaction snapshots, references, projections, and evidence.
- Direct writes to another app database, reference database, external engine, payment gateway, tax engine, credit bureau, fraud provider, clearinghouse, ERP, network controller, or partner platform remain out of scope.
- Downstream execution by usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data owners remains with those apps; Bill Cycle Control And Invoice Presentment must track dependency state, retry status, and reconciliation evidence.
- Platform identity, authorization, policy, audit, notification, eventing, API gateway, workflow, reporting, data retention, and data residency capabilities must be available before production rollout.
- Any non-TMF extension API must be documented, reviewed by architecture, and tested alongside TMF Open API contracts before external exposure.

## Feature Detail Review Implementation Alignment (2026-06-14)

Source: [App Feature Detail Review Alignment](README.md#feature-detail-review-alignment-2026-06-14) and [Suite Feature Detail Review](../../feature-detail-review.md).

Apply this app review scope to this feature: billing account operations, bill-cycle control, payment allocation, disputes, adjustments, dunning and collections handoff, and financial close evidence.

Implementation updates required for this feature:

- Re-check the core workflows and add or adjust happy paths, approval paths, exception queues, rollback or compensation behavior, and handoffs so the review scope is directly represented in build stories.
- Add or refine UI workbench expectations, including operator queues, evidence panels, policy decision traces, preview/simulation views, and status dashboards where this feature owns the behavior.
- Add or refine command APIs, query APIs, events, app-owned data fields, DDL gap notes, and integration handoffs needed to support the review scope without crossing app data ownership boundaries.
- Add acceptance criteria for source authority, tenant and residency controls, lifecycle state, approval evidence, idempotency, correlation IDs, SLA/OLA timers, and downstream acknowledgement where applicable.
- Add negative scenarios for stale data, duplicate events, policy denial, missing evidence, downstream outage, unauthorized access, bulk/replay risk, and manual override misuse.
- Extend tests to include happy path, negative path, edge case, API contract, event replay, data reconciliation, security, accessibility, observability, runbook, and release-gate evidence for the review scope.

## Build-Ready Refinement (2026-06-14)

This refinement converts the feature review material for Bill Cycle Control And Invoice Presentment into delivery slices that can become epics, stories, API contracts, migrations, and test cases. Treat Billing, Payments, And Account Operations as the owning application for this feature within Suite BSS Commercial and schema `billing_payments`.

| Workstream | Build-ready delivery guidance |
| --- | --- |
| UX and workflow | Build the Bill Cycle Control And Invoice Presentment workbench for Billing operations user, Care agent, Finance user, Collections user, Customer. Include search or intake, guided validation, detail view, lifecycle timeline, decision panel, evidence drawer, exception queue, bulk or replay controls where relevant, saved filters, SLA/OLA aging, empty/error states, and role-aware masking. The UI must expose create, validate, approve, correct, close, and audit bill cycle control and invoice presentment state and block closure when required evidence, approval, reconciliation, or downstream acknowledgement is missing. |
| API and events | Implement command and query APIs around bill-cycle-control-and-invoice-presentment using TMF678, TMF681, TMF667, TMF666. Command APIs for bill cycle control and invoice presentment must cover create/initiate, validate, update, approve/reject, hold/release, cancel, rollback or compensate where applicable, retry, correct, and close. Query APIs for bill cycle control and invoice presentment must cover search, detail, timeline, related billing account/bill/payment/prepay/finance context references, dependency graph, work queue, metrics, and... Domain events for bill cycle control and invoice presentment must include created, validated, blocked, approved, rejected, updated, handoff requested, exception raised, exception resolved, cancelled, compensated... Extension APIs are allowed only for bill run quality gates, invoice rendering/presentment, subledger/GL close control, revenue recognition policy, hardship workflow, chargeback evidence, deposit lifecycle, and tax... Every command, query, and event must carry tenant/brand/market where applicable, actor, source channel, reason code, idempotency key, correlation ID, external reference, lifecycle state, and version metadata. |
| Data and controls | Persist bill cycle control and invoice presentment record inside `billing_payments` with typed lifecycle, owner, status reason, timestamps, policy decision, source freshness, confidence, old/new value, evidence, and reconciliation fields. Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship... Keep TMF payloads, extension characteristics, imported evidence, and low-stability metadata in JSONB while promoting operationally searched lifecycle fields to typed columns. |
| Integration and handoff | Exchange not yet specified with the upstream and downstream owners named in the app README, modules-and-features, suite data model, TMF review, and DDL traceability files only through APIs, events, workflow tasks, governed projections, adapters, evidence packages, or certified data products. Show source owner, freshness, confidence, dependency state, retry status, blocked consumer, and completion evidence so the app does not create shadow mastership or direct cross-schema coupling. |
| Security, privacy, and compliance | Enforce RBAC/ABAC, tenant and residency boundaries, least privilege, separation of duties, masking, purpose limitation, retention, legal hold, export control, manual override expiry, immutable audit, and evidence chain of custody for Bill Cycle Control And Invoice Presentment. Sensitive customer, revenue, partner, security, network, credential, or regulatory evidence must be masked unless the persona has explicit operational purpose. |
| Tests and operations | Create unit, API contract, event replay/idempotency, workflow, integration, migration, data reconciliation, security/privacy, accessibility/localization, performance, dashboard, alert, and runbook tests for Bill Cycle Control And Invoice Presentment. Cover happy path, assisted path, automated path, exception path, bulk/project path, stale or duplicate input, downstream outage, policy denial, manual override, and reconciliation mismatch. Use the existing review scope - billing account operations, bill-cycle control, payment allocation, disputes, adjustments, dunning and collections handoff, and financial close evidence. - as mandatory backlog and test evidence. |

Implementation notes:

- Treat Billing, Payments, And Account Operations as the lifecycle owner for bill cycle control and invoice presentment record; referenced data such as not yet specified must remain references, snapshots, projections, evidence packages, or consumer acknowledgements unless the source file explicitly gives this app mastership.
- Make TMF alignment visible in every story: use named TMF resources where they fit, document non-TMF extension APIs with OpenAPI, and keep extension payloads compatible with TMF-style identifiers, lifecycle state, related entities, pagination, errors, and event envelopes.
- Build UI and API behavior around decision evidence, not only CRUD: surface the permitted next actions, policy decision, state reason, owner, SLA/OLA timer, blocked dependency, retry or compensation path, and closure proof.
- Add development tasks for route/page/component work, command/query handlers, DTO validation, entity/repository/migration changes, outbox/event contracts, projection refresh, privacy/security checks, and operational dashboards.
- Definition-of-done evidence must show downstream consumers can use published state through APIs, events, projections, workflow tasks, or certified data products without direct database reads or manual spreadsheet reconciliation.

## Definition Of Done

1. Product owner has approved Bill Cycle Control And Invoice Presentment scope for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence with personas, decision rights, happy path, assisted path, automated path, partner/channel path, and back-office path covered.
2. Architecture owner has approved ODA boundaries, TMF678, TMF681, TMF667, TMF666 usage, extension API notes, event contracts, integration handoffs, and private app database assumptions for bill cycle control and invoice presentment.
3. QA owner has automated or explicitly documented acceptance, negative, edge, API, event, workflow, integration, security, privacy, data, performance, resilience, and regression tests for bill cycle control and invoice presentment.
4. Operations owner has dashboards, queues, alerts, runbooks, replay/reconciliation procedures, SLA/OLA measures, and ownership model ready for billing operations, payments operations, revenue accounting, collections operations, and finance control.
5. Data owner has confirmed source authority, app-owned fields, related entity references, projection/data-product behavior, lineage, retention, legal hold, and reporting measures for billing account/bill/payment/prepay/finance context.
6. Compliance and security owners have approved PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency controls, evidence retention, masking, tenant/data-residency enforcement, and privileged-action review.


## Build-Ready Refinement (2026-06-15)

Header added at the top of this file. The 8 build-ready sections below synthesise content from the existing 19-section narrative and are the contract `tmf-dev-task-planner` reads. Source citations are inline.

## Persona & decision

- Not applicable — feature has no separate persona (single shared workflow).

## Lifecycle ownership

- This app owns the lifecycle state of the planning record listed in the source `## Telecom Objects And Decision Rights`. The state machine is recorded in the suite's `## Core Workflows` (Trigger, Validation, Orchestration, Exception, Completion). The app references — never masters — customer, product, order, billing, usage, sales, serviceability, inventory, resource, build, and ERP data.
- Source: [features/<this>.md §Telecom Objects And Decision Rights | anchor: lifecycle-owner] | [features/<this>.md §Core Workflows | anchor: lifecycle-states]

## TMF fit

- TMF API baseline for this app: TMF666, TMF678, TMF676, TMF670, TMF654.
- Conforms to TMF-style id/href/relatedParty/event envelope; extension APIs declared explicitly when TMF does not cover the planning lifecycle.
- Source: [planning/suite-details/tmf-api-ddl-reviews/billing-payments.md | anchor: tmf-fit]

## Data fit

- Owns schema `billing_payments_account_operations`; the V001 migration lists the owned tables: (none captured).
- Source: [database/postgres/suites/ts_bss_commercial/V001__create_app_schemas_and_starter_tables.sql §schema | anchor: schema-list]

## Path coverage

- Happy path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Assisted path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Automated path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Exception path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Bulk path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Historical path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Multi-tenant path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Regulatory path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Source: [features/<this>.md §Edge Cases | anchor: paths] | [features/<this>.md §Missing Use Cases And Scenarios | anchor: paths]

## UI implications

- Pages / workbenches (per the app's `Required app screens / workbenches` block in `dev-tasks/development-task-tracker.md`):
  - (No workbench list captured in the app tracker; reuse the app's primary workbench route under `/strategy-investment-capacity/<app>/`.)
- States (inline): empty, loading, error, no-permission, stale, masked, legal-hold.
- Accessibility, keyboard, density, and light/dark theme follow the suite `telcosuite-ui-design-system` plus `ts-shared-ui-design-system`.
- Source: [development-task-tracker.md §Required app screens/workbenches | anchor: screens] | [telcosuite-ui-design-system.md | anchor: ux-baseline]

## Acceptance & tests

- AC1 (AC-bill-cycle-control-and-invoice-presentment-01-01): Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete intake and ownership for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
- AC2 (AC-bill-cycle-control-and-invoice-presentment-01-02): Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in intake and ownership, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
- AC3 (AC-bill-cycle-control-and-invoice-presentment-01-03): Given an API consumer or event submits bill cycle control and invoice presentment data for intake and ownership, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
- AC4 (AC-bill-cycle-control-and-invoice-presentment-01-04): Given validation, downstream response, or compliance control fails during intake and ownership, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
- AC5 (AC-bill-cycle-control-and-invoice-presentment-01-05): Given intake and ownership is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.
- AC6 (AC-bill-cycle-control-and-invoice-presentment-02-01): Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete validation and policy control for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
- AC7 (AC-bill-cycle-control-and-invoice-presentment-02-02): Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in validation and policy control, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
- AC8 (AC-bill-cycle-control-and-invoice-presentment-02-03): Given an API consumer or event submits bill cycle control and invoice presentment data for validation and policy control, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
- AC9 (AC-bill-cycle-control-and-invoice-presentment-02-04): Given validation, downstream response, or compliance control fails during validation and policy control, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
- AC10 (AC-bill-cycle-control-and-invoice-presentment-02-05): Given validation and policy control is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.
- AC11 (AC-bill-cycle-control-and-invoice-presentment-03-01): Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete cross-app orchestration for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
- AC12 (AC-bill-cycle-control-and-invoice-presentment-03-02): Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in cross-app orchestration, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
- AC13 (AC-bill-cycle-control-and-invoice-presentment-03-03): Given an API consumer or event submits bill cycle control and invoice presentment data for cross-app orchestration, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
- AC14 (AC-bill-cycle-control-and-invoice-presentment-03-04): Given validation, downstream response, or compliance control fails during cross-app orchestration, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
- AC15 (AC-bill-cycle-control-and-invoice-presentment-03-05): Given cross-app orchestration is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.
- AC16 (AC-bill-cycle-control-and-invoice-presentment-04-01): Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete exception and compensation for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
- AC17 (AC-bill-cycle-control-and-invoice-presentment-04-02): Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in exception and compensation, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
- AC18 (AC-bill-cycle-control-and-invoice-presentment-04-03): Given an API consumer or event submits bill cycle control and invoice presentment data for exception and compensation, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
- AC19 (AC-bill-cycle-control-and-invoice-presentment-04-04): Given validation, downstream response, or compliance control fails during exception and compensation, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
- AC20 (AC-bill-cycle-control-and-invoice-presentment-04-05): Given exception and compensation is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.
- AC21 (AC-bill-cycle-control-and-invoice-presentment-05-01): Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete reporting and closure for bill cycle control and invoice presentment, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
- AC22 (AC-bill-cycle-control-and-invoice-presentment-05-02): Given bill cycle control and invoice presentment needs manual review, when a persona resolves missing data, approval, or policy conflict in reporting and closure, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
- AC23 (AC-bill-cycle-control-and-invoice-presentment-05-03): Given an API consumer or event submits bill cycle control and invoice presentment data for reporting and closure, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
- AC24 (AC-bill-cycle-control-and-invoice-presentment-05-04): Given validation, downstream response, or compliance control fails during reporting and closure, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
- AC25 (AC-bill-cycle-control-and-invoice-presentment-05-05): Given reporting and closure is ready to close for bill cycle control and invoice presentment, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.
- Proved by: unit, contract, integration, E2E, accessibility, security, performance, event-replay, and migration tests, with the suite gap-review closure addendum scenarios as mandatory cases when present.
- Source: [features/<this>.md §Acceptance Criteria | anchor: ac-list]

## Dependencies & release gate

- Depends on: dev-tasks tracker `Required app screens/workbenches` block; the suite's P01 foundation tasks; cross-app TMF and event contracts listed under `## API, Event, And Data Requirements`.
- Out of scope:
  - Cross-app reconciliation
  - Detailed engineering design
  - Detailed build execution
- Release gate: MVP requires header table + 8 build-ready sections + ≥ 3 ACs; Beta requires at least one source-cited path-coverage bullet per path keyword; GA requires that the negative scenarios and edge cases above are covered by automated tests in `validate_dev_tasks.py`.
- Source: [development-task-tracker.md | anchor: release-gate]
