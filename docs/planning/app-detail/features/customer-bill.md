# Customer Bill Feature Specification

Reviewed: 2026-06-07

Suite: BSS Commercial

App: [Billing, Payments, And Account Operations App](../README.md)

Source module detail: [Modules And Features](../modules-and-features.md)

Feature area slug: `customer-bill`

## Feature Intent

Present bills, line items, balances, due dates, payment status, bill history, bill explanation, rebill triggers, and bill inquiry context.

Customer Bill turns that intent into a controlled billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition capability: the app owns the customer bill lifecycle state, validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period, and leaves usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data consumers with auditable status rather than spreadsheet or direct-database workarounds.

## Personas Covered

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

## Persona-Specific Outcomes

| Persona | Decision rights and jobs-to-be-done | Feature outcome |
| --- | --- | --- |
| Billing operations user | Reviews and reconciles customer bill financial state, postings, adjustments, settlement, and audit evidence. | Billing operations user can complete, approve, monitor, or audit customer bill with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Care agent | Uses customer bill context to resolve customer care, complaint, billing, order, or assurance handoff without bypassing the owning app. | Care agent can complete, approve, monitor, or audit customer bill with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Finance user | Reviews and reconciles customer bill financial state, postings, adjustments, settlement, and audit evidence. | Finance user can complete, approve, monitor, or audit customer bill with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Collections user | Scores, holds, releases, disputes, or recovers customer bill risk state under approved policy and customer protection controls. | Collections user can complete, approve, monitor, or audit customer bill with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |
| Customer | Views and submits customer bill requests only for their own customer account, consent state, bill/order/usage context, and permitted evidence. | Customer can complete, approve, monitor, or audit customer bill with billing account/bill/payment/prepay/finance context state, usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff status, and immutable policy/evidence trail. |

## Core User Journeys Covered

| Step | User or system intent | Feature responsibility |
| ---: | --- | --- |
| 1 | Create or maintain billing account, bill cycle, billing preference, tax profile reference, and payment terms. | Customer Bill captures the intake and source authority for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records customer bill state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 2 | Generate or ingest customer bills and bill line item summaries. | Customer Bill validates eligibility, policy, and dependency state for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records customer bill state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 3 | Manage payment methods, mandates, tokens, one-time payments, auto-pay, reversals, refunds, and allocation. | Customer Bill orchestrates owned lifecycle updates and downstream handoffs for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records customer bill state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 4 | Manage prepaid balances, top-ups, reservations, expiries, and notifications. | Customer Bill routes fallout, approval, retry, cancellation, or compensation work for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records customer bill state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |
| 5 | Manage adjustments, dunning state, payment promises, write-offs, and service restriction triggers. | Customer Bill publishes completion, reconciliation, and evidence events for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence; it records customer bill state, correlation ID, source channel, owner, policy decision, and usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data handoff evidence. |

## Missing Use Cases And Scenarios

| Scenario | Required behavior |
| --- | --- |
| Happy path | Customer Bill must support this path for customer bill: Billing operations validates billing account and bill cycle readiness, releases compliant invoices, receives payments, allocates cash, and posts subledger/GL and revenue recognition evidence. |
| Assisted path | Customer Bill must support this path for customer bill: A care agent explains bill line items, takes approved payments or adjustments, and opens billing dispute or hardship workflow with masked payment data. |
| Automated path | Customer Bill must support this path for customer bill: Payment gateway, charging engine, tax engine, or ERP sends callbacks and receives idempotent allocation, reversal, posting, and reconciliation events. |
| Customer path | Customer Bill must support this path for customer bill: A customer views a bill, invoice, payment method, prepay balance, refund, deposit, or hardship plan through self-care with localized and accessible presentation. |
| Back-office path | Customer Bill must support this path for customer bill: Billing analyst and finance controller reconcile bill runs, chargebacks, refunds, write-offs, deposits, AR, GL, revenue recognition, and close exceptions. |
| Collections path | Customer Bill must support this path for customer bill: Collections receives overdue balance, dunning state, payment promise, hardship protection, restriction eligibility, and reconnection evidence without changing bill/payment masters. |

## Core Workflow And Control Points

| Control point | Required behavior | Evidence captured |
| --- | --- | --- |
| Trigger | Start customer bill from a billing account change, bill cycle start, usage/rating feed, invoice release, payment event, refund/chargeback request, adjustment, collections trigger, hardship case, prepay top-up, or finance close run with source channel, actor, tenant, customer/account/product/order references where applicable, and idempotency key. | Intake timestamp, source, actor, correlation ID, initiating record, and submitted payload hash. |
| Validation | Validate billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period before mutating billing account/bill/payment/prepay/finance context state or handing work to another app. | Validation result, policy decision, source authority, missing fields, and permitted next action. |
| Orchestration | Coordinate Usage and Charging for rated usage and balances, tax engines for invoice taxes, payment gateways and token vaults, Credit/Fraud/Collections for dunning and restrictions, Customer 360 and Care for bill inquiries, Order Management for order-to-bill actions, finance/ERP for AR/GL/revenue recognition, partner settlement, and DWH/lakehouse using APIs, events, workflow tasks, or governed projections while preserving app mastership: Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities. | Downstream owner, dependency state, request/response reference, retry counter, and event IDs. |
| Exception | Route customer bill fallout, policy failures, manual approvals, retries, rollback, compensation, and cancellation to accountable queues. | Queue owner, severity, due date, customer/revenue/compliance impact, reason code, comments, and evidence links. |
| Completion | Close customer bill only when owned lifecycle state, downstream handoffs, reconciliation, notifications, and reporting facts are complete or explicitly excepted. | Completion state, before/after values, reconciliation result, notification status, approver, and closure event. |
| Evidence | Preserve audit and regulatory evidence for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency with role-aware masking and retention/legal-hold controls. | Audit log, policy version, document/evidence reference, retention class, legal hold flag, and export controls. |

## Detailed Feature Backlog

| Feature ID | Feature | Parent feature area | Priority guidance |
| --- | --- | --- | --- |
| F-customer-bill-01 | Present bills | Customer Bill | P2: required when present bills blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |
| F-customer-bill-02 | Payment status | Customer Bill | P1: required when payment status blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |
| F-customer-bill-03 | Bill history | Customer Bill | P2: required when bill history blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |
| F-customer-bill-04 | Bill explanation | Customer Bill | P2: required when bill explanation blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |
| F-customer-bill-05 | Rebill triggers | Customer Bill | P2: required when rebill triggers blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |
| F-customer-bill-06 | bill inquiry context | Customer Bill | P2: required when bill inquiry context blocks billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition; phase optimization after the app-owned lifecycle, handoff, and audit controls are stable. |

## Acceptance Criteria

### Record and lifecycle management

Feature detail: Create, search, view, update, retire, reinstate, and track lifecycle state for customer bill records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-01-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete record and lifecycle management for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-01-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in record and lifecycle management, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-01-03 Automated path:** Given an API consumer or event submits customer bill data for record and lifecycle management, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-01-04 Exception path:** Given validation, downstream response, or compliance control fails during record and lifecycle management, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-01-05 Completion evidence:** Given record and lifecycle management is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Validation, policy, and eligibility

Feature detail: Validate customer bill changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-02-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete validation, policy, and eligibility for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-02-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in validation, policy, and eligibility, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-02-03 Automated path:** Given an API consumer or event submits customer bill data for validation, policy, and eligibility, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-02-04 Exception path:** Given validation, downstream response, or compliance control fails during validation, policy, and eligibility, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-02-05 Completion evidence:** Given validation, policy, and eligibility is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Work queues and approvals

Feature detail: Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-03-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete work queues and approvals for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-03-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in work queues and approvals, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-03-03 Automated path:** Given an API consumer or event submits customer bill data for work queues and approvals, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-03-04 Exception path:** Given validation, downstream response, or compliance control fails during work queues and approvals, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-03-05 Completion evidence:** Given work queues and approvals is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Search, timeline, and operational views

Feature detail: Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for customer bill work. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-04-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete search, timeline, and operational views for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-04-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in search, timeline, and operational views, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-04-03 Automated path:** Given an API consumer or event submits customer bill data for search, timeline, and operational views, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-04-04 Exception path:** Given validation, downstream response, or compliance control fails during search, timeline, and operational views, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-04-05 Completion evidence:** Given search, timeline, and operational views is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### API and event behavior

Feature detail: Expose command, query, and event contracts for customer bill so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-05-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete API and event behavior for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-05-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in API and event behavior, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-05-03 Automated path:** Given an API consumer or event submits customer bill data for API and event behavior, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-05-04 Exception path:** Given validation, downstream response, or compliance control fails during API and event behavior, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-05-05 Completion evidence:** Given API and event behavior is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

### Audit, evidence, and reporting

Feature detail: Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. For customer bill, this controls billing account/bill/payment/prepay/finance context through billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition while respecting that Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.

Acceptance criteria:

1. **AC-customer-bill-06-01 Happy path:** Given a permitted Billing operations user has valid billing account/bill/payment/prepay/finance context, when they complete audit, evidence, and reporting for customer bill, then the app validates billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and stores the accepted lifecycle state with owner, timestamp, source channel, and correlation ID.
2. **AC-customer-bill-06-02 Assisted path:** Given customer bill needs manual review, when a persona resolves missing data, approval, or policy conflict in audit, evidence, and reporting, then the app shows the blocking usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency, captures comments/evidence, and resumes the same lifecycle instance without duplicate work.
3. **AC-customer-bill-06-03 Automated path:** Given an API consumer or event submits customer bill data for audit, evidence, and reporting, when the payload is valid and idempotent, then the app returns a contract-compliant state, emits the required event, and keeps read projections separate from app-owned writes.
4. **AC-customer-bill-06-04 Exception path:** Given validation, downstream response, or compliance control fails during audit, evidence, and reporting, when the exception is raised, then the app assigns an accountable queue with severity, due date, retry/rollback/compensation option, customer or revenue impact, and evidence requirements.
5. **AC-customer-bill-06-05 Completion evidence:** Given audit, evidence, and reporting is ready to close for customer bill, when downstream handoffs and reconciliation are complete, then the app records before/after values, approval or policy decision, related entity references, metrics, and evidence links for audit and reporting.

## Negative Scenarios

| Scenario | Expected behavior |
| --- | --- |
| Unauthorized customer bill access or mutation | Reject the request, mask billing account/bill/payment/prepay/finance context data, and record actor, channel, tenant, policy decision, and correlation ID. |
| Missing mandatory customer bill context | Keep customer bill in draft, blocked, or rejected state with field-level errors for billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period and do not publish downstream handoff events. |
| Invalid customer bill lifecycle transition | Block the transition, show allowed next states, preserve prior state/version, and require permitted role or automated policy to resubmit. |
| Conflicting master data for customer bill | Route correction to the owning app named by data mastery and prevent local shadow updates to customer, catalog, order, inventory, billing, usage, risk, or partner masters. |
| Downstream usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependency unavailable | Fail fast for synchronous decisions or queue controlled retry with owner, due date, backoff policy, and customer/revenue impact flag. |
| Duplicate, stale, or out-of-order customer bill request | Use optimistic locking, event version, source timestamp, and idempotency key so retries cannot duplicate work or corrupt current state. |
| Policy, consent, regulatory, or geography breach | Stop the transaction, preserve the policy decision, notify only permitted roles, and enforce PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency. |
| Manual override for customer bill | Require approval role, reason code, expiry, compensating action, post-action review, and searchable audit evidence. |
| Sensitive evidence requested for customer bill | Mask or deny restricted KYC, payment, fraud, complaint, usage, tax, or legal evidence while keeping operational task status visible. |
| Reconciliation mismatch after customer bill completion | Reopen or hold closure until usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data state agrees or an approved exception with finance/customer/compliance impact is recorded. |

## Edge Cases

| Edge case | Expected handling |
| --- | --- |
| Bulk or project-scale customer bill processing | Support validation preview, staged commit, partial failure report, throttling, replay, and rollback or repair plan before production release. |
| Long-running customer bill journey | Expose waiting, blocked, retrying, escalated, compensated, corrected, and completed states with timers, owners, and customer/revenue impact. |
| Historical customer bill correction | Allow effective-dated correction with reason, old/new values, approver, downstream recalculation trigger, and retention/legal-hold validation. |
| Multi-brand, multi-tenant, or data-residency boundary | Apply tenant, brand, market, geography, language, currency, and data-residency controls consistently in UI, API, event, and reporting paths. |
| High-volume operational period for customer bill | Protect critical flows with pagination, async export, queue back-pressure, circuit breakers, dashboard filters, and runbook-defined load-shedding. |
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
| Critical | Bill explanation and dispute-safe dunning journey. | Add concrete happy path, negative path, edge-case, API/event/data control, reporting, and test evidence for this feature area. |

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

Related APIs and API areas: [TMF678](../../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill)

TMF API fit and extension notes:

- Use TMF678 for the TMF resource areas already identified in this feature specification; do not replace those resources with local-only contracts when the TMF API covers the lifecycle or query behavior.
- Extension APIs are allowed only for bill run quality gates, invoice rendering/presentment, subledger/GL close control, revenue recognition policy, hardship workflow, chargeback evidence, deposit lifecycle, and tax invoice evidence where no direct TMF resource exists; each extension must be explicitly labelled non-TMF, documented with OpenAPI, and aligned to TMF-style id, href, lifecycle state, relatedParty, relatedEntity, error, pagination, and event-envelope patterns where practical.
- Command APIs for customer bill must cover create/initiate, validate, update, approve/reject, hold/release, cancel, rollback or compensate where applicable, retry, correct, and close.
- Query APIs for customer bill must cover search, detail, timeline, related billing account/bill/payment/prepay/finance context references, dependency graph, work queue, metrics, and audit/evidence retrieval with role-aware masking.
- Domain events for customer bill must include created, validated, blocked, approved, rejected, updated, handoff requested, exception raised, exception resolved, cancelled, compensated, completed, corrected, and reconciliation failed where the lifecycle uses those states.

Data and ownership requirements:

- Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities; other apps consume customer bill state through APIs, events, governed projections, workflow tasks, or certified data products.
- Store source channel, actor, tenant/brand/market, external references, status reason, timestamps, policy decision, before/after values, related customer/account/product/order/bill/usage/ticket references where applicable, and evidence links.
- Keep read projections, analytics extracts, and DWH/lakehouse outputs separate from operational writes so Customer Bill does not create shadow mastership.
- Provide reconciliation outputs that prove usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependencies have completed, failed, or remain explicitly owned.

Integration and handoff requirements:

- Customer Bill must exchange customer bill state or evidence with Usage and Charging for rated usage and balances through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with tax engines for invoice taxes through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with payment gateways and token vaults through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with Credit/Fraud/Collections for dunning and restrictions through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with Customer 360 and Care for bill inquiries through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with Order Management for order-to-bill actions through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with finance/ERP for AR/GL/revenue recognition through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with partner settlement through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.
- Customer Bill must exchange customer bill state or evidence with DWH/lakehouse through APIs, events, workflow tasks, files, or governed projections as appropriate to that owner.

## Non-Functional Requirements

- Scale and latency: bill and payment query P95 below 500 ms, payment status callback processing within agreed gateway SLA, 99.9% availability for payment and bill-view APIs, resilient bill-cycle batch restart, immutable finance audit evidence, and localized invoice rendering.
- Availability and resilience: Customer Bill must support 99.9% or higher availability for interactive and API paths that gate usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence, with queue back-pressure, retry, replay, and circuit-breaker controls for downstream integrations.
- Auditability and retention: customer bill history must preserve actor, channel, reason, old/new value, policy version, approval, event ID, external reference, and retention/legal-hold class for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency.
- Localization and accessibility: Customer Bill user tasks, customer/partner communications, currency/date formats, invoice or offer disclosures where applicable, and error messages must support market localization, WCAG-aligned accessibility, and role-aware data masking.
- Data protection: API, event, export, and dashboard paths must enforce tenant isolation, data residency, purpose limitation, least privilege, field-level masking, and secure evidence storage for billing account/bill/payment/prepay/finance context.

## Compliance, Security, And Privacy

- Customer Bill must enforce PCI token handling for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce payment mandate evidence for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce tax invoice compliance for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce refund/chargeback evidence for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce hardship and vulnerable-customer protections for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce revenue recognition control for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce finance close audit for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce retention for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce legal hold for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce localization for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce accessibility for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce tenant isolation for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Customer Bill must enforce data residency for customer bill records, UI actions, API payloads, events, reports, and evidence exports.
- Privileged actions on customer bill require role-based approval, reason code, expiration where relevant, and post-action review by billing operations, payments operations, revenue accounting, collections operations, and finance control.
- Sensitive billing account/bill/payment/prepay/finance context evidence must be masked in search, timelines, exports, analytics, partner views, and operational dashboards unless the persona has a permitted purpose.

## Observability And Operations

- Metrics: track customer bill intake volume, validation failure rate, policy rejection rate, automation rate, manual override rate, queue aging, retry count, cancellation/rollback/compensation count, reconciliation mismatch, and completion quality by tenant, market, channel, product, partner, and owning team.
- Queues: provide work queues for draft, pending validation, pending approval, blocked dependency, exception, retrying, customer-impacting, revenue-impacting, compliance-impacting, compensated, corrected, completed, and archived customer bill records.
- Alerts: alert billing operations, payments operations, revenue accounting, collections operations, and finance control when customer bill queue aging, downstream failure, event publication failure, reconciliation mismatch, abnormal policy override, or SLA/OLA breach risk exceeds threshold.
- Runbooks: document triage, retry, replay, rollback, compensation, manual approval, customer/partner communication, evidence export, and reconciliation steps for Customer Bill.
- Replay and reconciliation: support idempotent replay for events, files, callbacks, and workflow tasks so Customer Bill can recover without duplicate billing account/bill/payment/prepay/finance context state or lost audit history.
- Ownership: billing operations, payments operations, revenue accounting, collections operations, and finance control owns first-line operational health; architecture, data, security, and compliance teams own policy and conformance review for the customer bill lifecycle.

## Test Approach

| Test layer | Required coverage |
| --- | --- |
| Unit tests | Field rules, lifecycle transitions, policy decisions, duplicate detection, effective dating, masking, and billing account/bill/payment/prepay/finance context state calculations for customer bill. |
| API contract tests | Commands, queries, errors, idempotency, pagination, filtering, version compatibility, and TMF-aligned payloads for TMF678 plus documented extension APIs. |
| Event contract tests | customer bill event names, payload shape, changed fields, correlation ID, idempotency key, ordering metadata, replay behavior, and subscriber compatibility. |
| Workflow tests | Happy path, assisted path, automated path, partner/channel path, approval, exception, timeout, retry, cancellation, rollback, compensation, correction, and closure for billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition. |
| Integration tests | Handoffs with usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data owners, external provider unavailability, eventual consistency, reconciliation, and no direct database access. |
| Security and privacy tests | Tenant isolation, role permissions, consent/purpose checks, sensitive-data masking, malicious payloads, audit logging, legal hold, retention, and export controls for PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency. |
| Data tests | Source authority, referential integrity, historical correction, projection refresh, DWH/lakehouse extract, reporting metrics, and data-quality stewardship for billing account/bill/payment/prepay/finance context. |
| Performance and resilience tests | Search, list, bulk import/export, queue throughput, API throughput, event replay, retry storm, downstream outage, and batch recovery under realistic telecom volumes. |
| Operational acceptance tests | Dashboards, alerts, runbooks, queue ownership, SLA/OLA reporting, reconciliation reports, and evidence export for billing operations, payments operations, revenue accounting, collections operations, and finance control. |

## Out Of Scope And Dependencies

- Customer Bill does not master entities assigned to another app in the data mastery document; it stores only its app-owned customer bill state, transaction snapshots, references, projections, and evidence.
- Direct writes to another app database, reference database, external engine, payment gateway, tax engine, credit bureau, fraud provider, clearinghouse, ERP, network controller, or partner platform remain out of scope.
- Downstream execution by usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data owners remains with those apps; Customer Bill must track dependency state, retry status, and reconciliation evidence.
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

This refinement converts the feature review material for Customer Bill into delivery slices that can become epics, stories, API contracts, migrations, and test cases. Treat Billing, Payments, And Account Operations App as the owning application for this feature within Suite BSS Commercial and schema `billing_payments`.

| Workstream | Build-ready delivery guidance |
| --- | --- |
| UX and workflow | Build the Customer Bill workbench for Billing operations user, Care agent, Finance user, Collections user, Customer. Include search or intake, guided validation, detail view, lifecycle timeline, decision panel, evidence drawer, exception queue, bulk or replay controls where relevant, saved filters, SLA/OLA aging, empty/error states, and role-aware masking. The UI must expose create, validate, approve, correct, close, and audit customer bill state and block closure when required evidence, approval, reconciliation, or downstream acknowledgement is missing. |
| API and events | Implement command and query APIs around customer-bill using TMF678. Command APIs for customer bill must cover create/initiate, validate, update, approve/reject, hold/release, cancel, rollback or compensate where applicable, retry, correct, and close. Query APIs for customer bill must cover search, detail, timeline, related billing account/bill/payment/prepay/finance context references, dependency graph, work queue, metrics, and audit/evidence retrieval with... Domain events for customer bill must include created, validated, blocked, approved, rejected, updated, handoff requested, exception raised, exception resolved, cancelled, compensated, completed, corrected, and... Extension APIs are allowed only for bill run quality gates, invoice rendering/presentment, subledger/GL close control, revenue recognition policy, hardship workflow, chargeback evidence, deposit lifecycle, and tax... Every command, query, and event must carry tenant/brand/market where applicable, actor, source channel, reason code, idempotency key, correlation ID, external reference, lifecycle state, and version metadata. |
| Data and controls | Persist customer bill record inside `billing_payments` with typed lifecycle, owner, status reason, timestamps, policy decision, source freshness, confidence, old/new value, evidence, and reconciliation fields. Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship... Keep TMF payloads, extension characteristics, imported evidence, and low-stability metadata in JSONB while promoting operationally searched lifecycle fields to typed columns. |
| Integration and handoff | Exchange not yet specified with the upstream and downstream owners named in the app README, modules-and-features, suite data model, TMF review, and DDL traceability files only through APIs, events, workflow tasks, governed projections, adapters, evidence packages, or certified data products. Show source owner, freshness, confidence, dependency state, retry status, blocked consumer, and completion evidence so the app does not create shadow mastership or direct cross-schema coupling. |
| Security, privacy, and compliance | Enforce RBAC/ABAC, tenant and residency boundaries, least privilege, separation of duties, masking, purpose limitation, retention, legal hold, export control, manual override expiry, immutable audit, and evidence chain of custody for Customer Bill. Sensitive customer, revenue, partner, security, network, credential, or regulatory evidence must be masked unless the persona has explicit operational purpose. |
| Tests and operations | Create unit, API contract, event replay/idempotency, workflow, integration, migration, data reconciliation, security/privacy, accessibility/localization, performance, dashboard, alert, and runbook tests for Customer Bill. Cover happy path, assisted path, automated path, exception path, bulk/project path, stale or duplicate input, downstream outage, policy denial, manual override, and reconciliation mismatch. Use the existing review scope - billing account operations, bill-cycle control, payment allocation, disputes, adjustments, dunning and collections handoff, and financial close evidence. - as mandatory backlog and test evidence. |

Implementation notes:

- Treat Billing, Payments, And Account Operations App as the lifecycle owner for customer bill record; referenced data such as not yet specified must remain references, snapshots, projections, evidence packages, or consumer acknowledgements unless the source file explicitly gives this app mastership.
- Make TMF alignment visible in every story: use named TMF resources where they fit, document non-TMF extension APIs with OpenAPI, and keep extension payloads compatible with TMF-style identifiers, lifecycle state, related entities, pagination, errors, and event envelopes.
- Build UI and API behavior around decision evidence, not only CRUD: surface the permitted next actions, policy decision, state reason, owner, SLA/OLA timer, blocked dependency, retry or compensation path, and closure proof.
- Add development tasks for route/page/component work, command/query handlers, DTO validation, entity/repository/migration changes, outbox/event contracts, projection refresh, privacy/security checks, and operational dashboards.
- Definition-of-done evidence must show downstream consumers can use published state through APIs, events, projections, workflow tasks, or certified data products without direct database reads or manual spreadsheet reconciliation.

## Definition Of Done

1. Product owner has approved Customer Bill scope for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence with personas, decision rights, happy path, assisted path, automated path, partner/channel path, and back-office path covered.
2. Architecture owner has approved ODA boundaries, TMF678 usage, extension API notes, event contracts, integration handoffs, and private app database assumptions for customer bill.
3. QA owner has automated or explicitly documented acceptance, negative, edge, API, event, workflow, integration, security, privacy, data, performance, resilience, and regression tests for customer bill.
4. Operations owner has dashboards, queues, alerts, runbooks, replay/reconciliation procedures, SLA/OLA measures, and ownership model ready for billing operations, payments operations, revenue accounting, collections operations, and finance control.
5. Data owner has confirmed source authority, app-owned fields, related entity references, projection/data-product behavior, lineage, retention, legal hold, and reporting measures for billing account/bill/payment/prepay/finance context.
6. Compliance and security owners have approved PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency controls, evidence retention, masking, tenant/data-residency enforcement, and privileged-action review.
