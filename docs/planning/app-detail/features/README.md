# Billing, Payments, And Account Operations App Feature Specifications

Reviewed: 2026-06-07

This folder contains the build-ready feature specifications for the Billing, Payments, And Account Operations app in Suite 02 BSS Commercial. Each specification defines concrete billing account/bill/payment/prepay/finance context lifecycle behavior, personas and decision rights, use cases, workflow controls, Given/When/Then acceptance criteria, TMF API fit, extension notes, integrations, NFRs, compliance controls, observability, and definition of done.

Parent app: [Billing, Payments, And Account Operations App](../README.md)

## Suite 02 Domain Lenses

- Primary journey coverage: billing account setup, bill cycle, invoice presentment, payment, collections/adjustment, prepay, refund, chargeback, deposit, hardship, subledger, GL, and revenue recognition.
- BSS lens: usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence.
- Data boundary: Billing, Payments, And Account Operations owns billing account operational state, customer-facing bill view, payment lifecycle view, payment method reference, prepay product view, adjustment, deposit, refund, chargeback, hardship, subledger, GL, and revenue-recognition control context while gateways, tax engines, charging engines, and ERP may remain external authorities.
- Integration handoffs: Usage and Charging for rated usage and balances, tax engines for invoice taxes, payment gateways and token vaults, Credit/Fraud/Collections for dunning and restrictions, Customer 360 and Care for bill inquiries, Order Management for order-to-bill actions, finance/ERP for AR/GL/revenue recognition, partner settlement, and DWH/lakehouse.
- Compliance focus: PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency.

## Feature Specification Index

| Feature specification | Commercial outcome | API basis | Evidence and control focus |
| --- | --- | --- | --- |
| [Bill Cycle Control And Invoice Presentment](bill-cycle-control-and-invoice-presentment.md) | Operate bill cycles, bill quality gates, rerun controls, invoice rendering, tax invoice compliance, and customer presentment. | TMF678, TMF681, TMF667, TMF666 | Bill Cycle Control And Invoice Presentment must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Billing Account](billing-account.md) | Manage billing accounts, bill cycles, invoice delivery, payment terms, tax references, enterprise split billing, cost centers, and account-product-bill links. | TMF666, TMF678 | Billing Account must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Collections And Adjustment](collections-and-adjustment.md) | Track overdue balances, dunning state, collection actions, payment promises, service restriction triggers, bill adjustments, disputed charges, goodwill credits, and approvals. | TMF678, TMF676 | Collections And Adjustment must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Customer Bill](customer-bill.md) | Present bills, line items, balances, due dates, payment status, bill history, bill explanation, rebill triggers, and bill inquiry context. | TMF678 | Customer Bill must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Finance Subledger GL And Revenue Recognition](finance-subledger-gl-and-revenue-recognition.md) | Create finance-ready AR subledger, GL posting, revenue recognition, tax evidence, and close controls from billing, payment, refund, and adjustment activity. | TMF678, TMF676, TMF670, TMF666, TMF635 | Finance Subledger GL And Revenue Recognition must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Payment And Payment Method](payment-and-payment-method.md) | Manage payment methods, mandates, card/bank tokens, payment capture, refunds, reversals, allocation, auto-pay, failed payment handling, and gateway integration. | TMF676, TMF670 | Payment And Payment Method must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Prepay Balance](prepay-balance.md) | Manage prepaid balances, top-ups, reservations, expiries, balance adjustments, threshold notifications, and near-real-time care/self-care views. | TMF654 | Prepay Balance must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |
| [Refund Chargeback Deposit And Hardship Controls](refund-chargeback-deposit-and-hardship-controls.md) | Manage refunds, reversals, chargebacks, deposits, guarantees, payment plans, hardship protections, and write-off accounting. | TMF676, TMF670, TMF666, TMF678, TMF681 | Refund Chargeback Deposit And Hardship Controls must preserve lifecycle state, decision owner, correlation ID, exception queue, and reconciliation evidence for usage-to-cash, bill-to-pay, trouble-to-resolve billing dispute handoff, finance close, and govern-to-comply tax/payment evidence. |

## Implementation Guardrails

- Keep app-owned writes inside the app boundary; other apps use APIs, events, governed projections, workflow tasks, or certified data products.
- Preserve the TMF API references already identified in each feature file and label any non-TMF extension API explicitly.
- Validate billing account status, customer/account authority, bill cycle lock, tax profile, invoice compliance, payment token/mandate, PCI boundary, allocation rules, adjustment approval, hardship protection, deposit state, revenue account, and finance period before accepting work that affects billing account/bill/payment/prepay/finance context state.
- Record source channel, actor, tenant/market, related entity references, policy decision, before/after values, correlation ID, and evidence links for every material billing account/bill/payment/prepay/finance context change.
- Route unresolved usage, charging, tax, payment gateway, risk/collections, customer care, order, finance, partner settlement, and data dependencies to visible queues with owner, severity, due date, retry/rollback/compensation path, and customer/revenue/compliance impact.
- Enforce PCI token handling, payment mandate evidence, tax invoice compliance, refund/chargeback evidence, hardship and vulnerable-customer protections, revenue recognition control, finance close audit, retention, legal hold, localization, accessibility, tenant isolation, and data residency in UI, API, event, dashboard, export, and evidence-retrieval paths.

## Definition Of Feature Completion

A feature specification in this folder is implementation-ready only when product, architecture, QA, operations, data, security, and compliance owners can trace the feature from persona decision rights through API/event contracts, negative scenarios, NFRs, observability, evidence retention, and cross-app handoff closure.

## Feature Detail Review Alignment (2026-06-14)

Source: [Suite Feature Detail Review](../../feature-detail-review.md) and [Critical Feature Review Enhancements](../modules-and-features.md#critical-feature-review-enhancements-2026-06-14).

The 2026-06-14 review upgrades this app feature set with required scope: billing account operations, bill-cycle control, payment allocation, disputes, adjustments, dunning and collections handoff, and financial close evidence.

Apply this scope when refining the feature specifications in this folder:

- Add or update epics, stories, UI workbenches, APIs, events, app-owned data fields, DDL gaps, test cases, observability, runbooks, and definition-of-done evidence for the review scope.
- Preserve the app data ownership boundary. Cross-app access must use APIs, events, workflow tasks, governed projections, or certified data products rather than direct database sharing.
- If this scope needs technology beyond Angular, Spring Boot, PostgreSQL, and PrimeNG, offer open-source options with pros, cons, and a recommendation before implementation.
