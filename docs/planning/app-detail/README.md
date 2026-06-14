# Billing, Payments, And Account Operations App Detail Pack

Reviewed: 2026-06-06

This folder expands the concise app overview into build-ready module, feature, persona, and user journey planning. The concise source overview remains at [billing-payments-account-operations.md](../billing-payments-account-operations.md).

Suite: BSS Commercial

## Build Intent

Manage customer billing accounts, bills, payment methods, payments, prepaid balances, adjustments, and collections-facing account operations.

## Detail Documents

- [Modules And Features](modules-and-features.md)
- [Feature Specifications](features/README.md)
- [Personas And User Journeys](personas-and-user-journeys.md)

## Primary Personas

- Billing operations user: monitors bill cycles, bill quality, billing account setup, and bill inquiries.
- Care agent: explains bills, takes payments, applies approved adjustments, and sees balance state.
- Finance user: reconciles payments, refunds, reversals, and receivables.
- Collections user: sees overdue balances, dunning state, and payment promises.
- Customer: views bills, pays, changes payment method, and tracks balance through self-care.

## Core Operating Flow

1. Create or maintain billing account, bill cycle, billing preference, tax profile reference, and payment terms.
2. Generate or ingest customer bills and bill line item summaries.
3. Manage payment methods, mandates, tokens, one-time payments, auto-pay, reversals, refunds, and allocation.
4. Manage prepaid balances, top-ups, reservations, expiries, and notifications.
5. Manage adjustments, dunning state, payment promises, write-offs, and service restriction triggers.

## Module Map

| Module | Feature focus | Related APIs |
| --- | --- | --- |
| Billing Account | Manage billing accounts, bill cycles, invoice delivery, payment terms, tax references, enterprise split billing, cost centers, and account-product-bill links. | [TMF666](../../../../references/tmforum-open-apis/openapi-specs/TMF666_AccountManagement), [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill) |
| Customer Bill | Present bills, line items, balances, due dates, payment status, bill history, bill explanation, rebill triggers, and bill inquiry context. | [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill) |
| Payment And Payment Method | Manage payment methods, mandates, card/bank tokens, payment capture, refunds, reversals, allocation, auto-pay, failed payment handling, and gateway integration. | [TMF676](../../../../references/tmforum-open-apis/openapi-specs/TMF676_PaymentManagement), [TMF670](../../../../references/tmforum-open-apis/openapi-specs/TMF670_PaymentMethods) |
| Prepay Balance | Manage prepaid balances, top-ups, reservations, expiries, balance adjustments, threshold notifications, and near-real-time care/self-care views. | [TMF654](../../../../references/tmforum-open-apis/openapi-specs/TMF654_PrepayBalanceManagement) |
| Collections And Adjustment | Track overdue balances, dunning state, collection actions, payment promises, service restriction triggers, bill adjustments, disputed charges, goodwill credits, and approvals. | [TMF678](../../../../references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill), [TMF676](../../../../references/tmforum-open-apis/openapi-specs/TMF676_PaymentManagement) |

## Data Ownership

Owns billing account operational state, bill view records, payment records, payment method references, prepaid balance view, adjustment requests, and collections account state. External billing engines, tax systems, payment gateways, and GL systems may remain separate integrations.

## First Release Scope

Deliver billing account view, customer bill view, payment method, one-time payment, adjustment workflow, and overdue balance state. Add full invoicing engine or deep external billing replacement only if product strategy requires it.

## Build Notes

- Treat this app as an API-first product surface. UI screens, automations, partner access, and internal integrations should use the same app-owned APIs.
- Keep the app database private to this app or its module owners. Other apps should consume APIs, events, governed read models, or data products.
- Create backlog items at feature level, but preserve module ownership so roadmap, permissions, observability, and data stewardship remain clear.

## Implementation Guidance

- [Implementation File Usage](implementation-file-usage.md)
