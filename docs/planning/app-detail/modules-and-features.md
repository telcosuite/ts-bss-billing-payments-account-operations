# Billing, Payments, And Account Operations App Modules And Features

Reviewed: 2026-06-06

This document expands each app module into feature-level planning guidance. It should be used to create epics, stories, API contracts, event contracts, screens, permissions, and test cases.

Source overview: [billing-payments-account-operations.md](../billing-payments-account-operations.md)

## App-Level Feature Principles

- Every feature must have an owning module and an owning app API.
- UI actions must call app APIs rather than writing directly to shared data stores.
- Cross-app reads should use APIs, subscribed events, governed projections, or data products.
- Each module should expose enough lifecycle state for operations, audit, automation, and customer/partner visibility.
- Feature design must include happy path, exception path, audit path, and reporting path.

## App Data Ownership Context

Owns billing account operational state, bill view records, payment records, payment method references, prepaid balance view, adjustment requests, and collections account state. External billing engines, tax systems, payment gateways, and GL systems may remain separate integrations.

## First Release Context

Deliver billing account view, customer bill view, payment method, one-time payment, adjustment workflow, and overdue balance state. Add full invoicing engine or deep external billing replacement only if product strategy requires it.

## Module 1: Billing Account

Anchor: `billing-account`

### Capability Intent

Manage billing accounts, bill cycles, invoice delivery, payment terms, tax references, enterprise split billing, cost centers, and account-product-bill links.

### Primary Personas Supported

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

### Feature Backlog Candidates

- Manage billing accounts.
- Invoice delivery.
- Payment terms.
- Tax references.
- Enterprise split billing.
- Cost centers.
- And account-product-bill links.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for billing account records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate billing account changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for billing account work. |
| API and event behavior | Expose command, query, and event contracts for billing account so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Billing Account | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate billing account state available through APIs |
| Handle Billing Account exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Billing Account performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF666](../../../../references/tmforum-open-apis/openapi-specs/TMF666_AccountManagement), [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 2: Customer Bill

Anchor: `customer-bill`

### Capability Intent

Present bills, line items, balances, due dates, payment status, bill history, bill explanation, rebill triggers, and bill inquiry context.

### Primary Personas Supported

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

### Feature Backlog Candidates

- Present bills.
- Payment status.
- Bill history.
- Bill explanation.
- Rebill triggers.
- And bill inquiry context.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for customer bill records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate customer bill changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for customer bill work. |
| API and event behavior | Expose command, query, and event contracts for customer bill so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Customer Bill | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate customer bill state available through APIs |
| Handle Customer Bill exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Customer Bill performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 3: Payment And Payment Method

Anchor: `payment-and-payment-method`

### Capability Intent

Manage payment methods, mandates, card/bank tokens, payment capture, refunds, reversals, allocation, auto-pay, failed payment handling, and gateway integration.

### Primary Personas Supported

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

### Feature Backlog Candidates

- Manage payment methods.
- Card/bank tokens.
- Payment capture.
- Failed payment handling.
- And gateway integration.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for payment and payment method records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate payment and payment method changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for payment and payment method work. |
| API and event behavior | Expose command, query, and event contracts for payment and payment method so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Payment And Payment Method | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate payment and payment method state available through APIs |
| Handle Payment And Payment Method exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Payment And Payment Method performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF676](../../../../references/tmforum-open-apis/openapi-specs/TMF676_PaymentManagement), [TMF670](../../../../references/tmforum-open-apis/openapi-specs/TMF670_PaymentMethods)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 4: Prepay Balance

Anchor: `prepay-balance`

### Capability Intent

Manage prepaid balances, top-ups, reservations, expiries, balance adjustments, threshold notifications, and near-real-time care/self-care views.

### Primary Personas Supported

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

### Feature Backlog Candidates

- Manage prepaid balances.
- Reservations.
- Balance adjustments.
- Threshold notifications.
- And near-real-time care/self-care views.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for prepay balance records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate prepay balance changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for prepay balance work. |
| API and event behavior | Expose command, query, and event contracts for prepay balance so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Prepay Balance | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate prepay balance state available through APIs |
| Handle Prepay Balance exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Prepay Balance performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF654](../../../../references/tmforum-open-apis/openapi-specs/TMF654_PrepayBalanceManagement)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 5: Collections And Adjustment

Anchor: `collections-and-adjustment`

### Capability Intent

Track overdue balances, dunning state, collection actions, payment promises, service restriction triggers, bill adjustments, disputed charges, goodwill credits, and approvals.

### Primary Personas Supported

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

### Feature Backlog Candidates

- Track overdue balances.
- Dunning state.
- Collection actions.
- Payment promises.
- Service restriction triggers.
- Bill adjustments.
- Disputed charges.
- Goodwill credits.
- And approvals.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for collections and adjustment records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate collections and adjustment changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for collections and adjustment work. |
| API and event behavior | Expose command, query, and event contracts for collections and adjustment so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Collections And Adjustment | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate collections and adjustment state available through APIs |
| Handle Collections And Adjustment exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Collections And Adjustment performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill), [TMF676](../../../../references/tmforum-open-apis/openapi-specs/TMF676_PaymentManagement)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Critical Feature Review Enhancements (2026-06-14)

### Critical Assessment

The baseline billing modules are aligned to TMF, but the implementation detail needs stronger financial operations behavior. Billing and payment features must support bill-cycle control, bill validation, payment allocation, refunds, disputes, adjustments, prepay balance actions, collections handoff, reconciliation, and close evidence from the first release.

### Enhancements To Add

| Enhancement | Modules | Implementation need |
| --- | --- | --- |
| Billing account operations workbench | Billing Account | Manage billing account state, bill cycle, bill format, presentation media, payment method reference, dunning eligibility, tax profile reference, and account holds. |
| Bill run and validation board | Customer Bill | Track generated, pending validation, issued, corrected, suppressed, disputed, reversed, and archived bills with control totals and exception aging. |
| Bill item and usage reconciliation | Customer Bill; Collections And Adjustment | Compare charges, credits, taxes, discounts, usage summaries, order triggers, adjustments, and rerating/rebill indicators before issue and close. |
| Payment allocation and refund control | Payment And Payment Method | Allocate payments across bills/accounts, detect duplicates, manage reversals/refunds, gateway references, settlement status, and failed payment retries. |
| Prepay balance action control | Prepay Balance | Manage top-up, reserve, transfer, adjustment, expiry, shared buckets, low-balance events, and balance action history with idempotency. |
| Dispute and adjustment workflow | Customer Bill; Collections And Adjustment | Capture disputed items, reason, evidence, owner, approval, customer communication, credit/refund decision, and financial posting status. |
| Collections handoff gate | Collections And Adjustment | Publish delinquency, promise-to-pay, hardship, dispute, payment failure, and write-off context to Credit/Fraud/Collections without mastering collections cases here. |

### Required Screens

| Screen | Required behavior |
| --- | --- |
| Billing operations cockpit | Bill cycles, issue readiness, validation failures, disputed value, payment failures, aging, and close status. |
| Bill detail workspace | Bill header, bill items, usage links, taxes, adjustments, disputes, payments, history, and customer-visible rendering status. |
| Payment reconciliation queue | Gateway reference, bank/settlement status, duplicate risk, allocation, reversal/refund state, and retry action. |
| Adjustment and dispute board | Financial impact, approval level, evidence, customer communication, GL/posting status, and closure reason. |

### Open-Source Decision Points

| Need | Candidate options | Decision prompt |
| --- | --- | --- |
| Invoice/PDF rendering | HTML templates; PDFBox; LibreOffice headless | Ask before adding rendering tooling for invoices, statements, or dispute letters. |
| Batch/reconciliation processing | Spring Batch; PostgreSQL procedures; scheduled Spring jobs | Use Spring/PostgreSQL first; add batch framework only if volume and restartability require it. |
| Payment integration adapters | Spring adapter layer; Apache Camel | Ask before adding an integration framework around payment gateways or bank files. |

### API/Event/Data Additions

| Area | Additions |
| --- | --- |
| APIs | Bill cycle manage, bill validate/issue/reverse, payment allocate/refund/retry, prepay action, adjustment approve, dispute open/resolve, collections handoff publish. |
| Events | `BillingAccountChanged`, `BillRunStarted`, `BillIssued`, `BillValidationFailed`, `PaymentAllocated`, `PaymentFailed`, `AdjustmentApproved`, `DisputeOpened`, `CollectionsHandoffReady`. |
| Data | Bills, payments, adjustments, and prepay balances are mastered here; collections cases and usage CDRs remain mastered by their owning apps. |

### First Release Scope

Include billing account operations, bill validation/issue, bill detail, payment allocation, dispute/adjustment workflow, prepay action control, and collections handoff. Defer deep finance subledger and advanced bill-cycle optimization until reconciliation controls are stable.
