# Billing, Payments, And Account Operations TMF API To DDL Review

Reviewed: 2026-06-14

Status: Complete for baseline app implementation. Endpoint-specific contract tests and final story-level field promotion still happen during build.

## Scope

This review covers `billing_payments` in suite database `ts_bss_commercial`. It uses the local TMF Open API reference set, the suite data model, the API-to-DDL traceability matrix, and the V001 starter DDL.

The review confirms that the app can move into implementation with a V002 typed DDL baseline while preserving full TMF payload compatibility through validated `tmf_payload`, typed common TMF columns, and normalized support tables.

## TMF API Baseline Selection

| TMF API | Local baseline spec | Resources/path roots reviewed | V001 table groups |
| --- | --- | --- | --- |
| TMF666 | `references/tmforum-open-apis/openapi-specs/TMF666_AccountManagement/TMF666-Account_Management-v5.0.0.oas.yaml` | `billFormat`, `billPresentationMedia`, `billingAccount`, `billingCycleSpecification`, `financialAccount`, `partyAccount`, `settlementAccount` | customer_account_hierarchy; billing_account_operation references |
| TMF678 | `references/tmforum-open-apis/openapi-specs/TMF678_CustomerBill/TMF678-CustomerBill-v5.0.0.oas.yaml` | `appliedCustomerBillingRate`, `billCycle`, `customerBill`, `customerBillOnDemand` | customer_bill; bill_item; billing_adjustment; revenue_margin_scenario references |
| TMF676 | `references/tmforum-open-apis/openapi-specs/TMF676_PaymentManagement/TMF676_Payment_Management_API_v4.0.0_swagger.json` | `payment`, `refund` | payment; payment_allocation; billing_adjustment references |
| TMF670 | `references/tmforum-open-apis/openapi-specs/TMF670_PaymentMethods/TMF670_Payment_Method_Management_API_v4.0.0_swagger.json` | `paymentMethod` | payment_method_reference |
| TMF654 | `references/tmforum-open-apis/openapi-specs/TMF654_PrepayBalanceManagement/TMF654_Prepay_Balance_Management_API_v4.0.0_swagger.json` | `accumulatedBalance`, `adjustBalance`, `balanceActionHistory`, `bucket`, `reserveBalance`, `topupBalance`, `transferBalance` | prepay_balance |

## Current DDL Coverage

Current starter DDL is in `database/postgres/suites/ts_bss_commercial/V001__create_app_schemas_and_starter_tables.sql` under schema `billing_payments`.

| Current table | TMF purpose | V002 decision |
| --- | --- | --- |
| `billing_payments.billing_account_operation` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.bill_cycle` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.customer_bill` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.bill_item` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.payment` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.payment_allocation` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.payment_method_reference` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.prepay_balance` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.billing_adjustment` | Starter table for Billing, Payments, And Account Operations; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| `billing_payments.event_outbox` | App outbox for domain and TMF notification events. | Keep and refine through `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |

## Resource To Table Decisions

| TMF API/resource | Master or anchor table | Path coverage | Promoted field candidates | Field handling strategy |
| --- | --- | --- | --- | --- |
| TMF666 `billFormat` | `billing_payments.bill_cycle` | `/billFormat`, `/billFormat/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `billPresentationMedia` | `billing_payments.bill_cycle` | `/billPresentationMedia`, `/billPresentationMedia/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `billingAccount` | `billing_payments.billing_account_operation` | `/billingAccount`, `/billingAccount/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `billingCycleSpecification` | `billing_payments.billing_account_operation` | `/billingCycleSpecification`, `/billingCycleSpecification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `financialAccount` | `billing_payments.billing_account_operation` | `/financialAccount`, `/financialAccount/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `partyAccount` | `billing_payments.billing_account_operation` | `/partyAccount`, `/partyAccount/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF666 `settlementAccount` | `billing_payments.billing_account_operation` | `/settlementAccount`, `/settlementAccount/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF678 `appliedCustomerBillingRate` | `billing_payments.customer_bill` | `/appliedCustomerBillingRate`, `/appliedCustomerBillingRate/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF678 `billCycle` | `billing_payments.bill_cycle` | `/billCycle`, `/billCycle/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF678 `customerBill` | `billing_payments.customer_bill` | `/customerBill`, `/customerBill/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF678 `customerBillOnDemand` | `billing_payments.customer_bill` | `/customerBillOnDemand`, `/customerBillOnDemand/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF676 `payment` | `billing_payments.payment` | `/payment`, `/payment/{id}` | `id`, `href`, `authorizationCode`, `correlatorId`, `description`, `name`, `paymentDate`, `status` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF676 `refund` | `billing_payments.payment` | `/refund`, `/refund/{id}` | `id`, `href`, `authorizationCode`, `correlatorId`, `description`, `name`, `refundDate`, `status` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF670 `paymentMethod` | `billing_payments.payment_method_reference` | `/paymentMethod`, `/paymentMethod/{id}` | `name`, `description`, `isPreferred`, `authorizationCode`, `status`, `statusDate`, `statusReason`, `validFor` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `accumulatedBalance` | `billing_payments.prepay_balance` | `/accumulatedBalance`, `/accumulatedBalance/{id}` | `id`, `href`, `description`, `name`, `bucket`, `logicalResource`, `partyAccount`, `product` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `adjustBalance` | `billing_payments.prepay_balance` | `/adjustBalance`, `/adjustBalance/{id}` | `id`, `href`, `confirmationDate`, `description`, `reason`, `requestedDate`, `adjustType`, `amount` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `balanceActionHistory` | `billing_payments.prepay_balance` | `/balanceActionHistory`, `/balanceActionHistory/{id}` | `id`, `href`, `confirmationDate`, `description`, `isAutoTopup`, `numberOfPeriods`, `reason`, `requestedDate` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `bucket` | `billing_payments.prepay_balance` | `/bucket`, `/bucket/{id}` | `id`, `href`, `confirmationDate`, `description`, `isShared`, `name`, `remainingValueName`, `requestedDate` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `reserveBalance` | `billing_payments.prepay_balance` | `/reserveBalance`, `/reserveBalance/{id}` | `id`, `href`, `confirmationDate`, `description`, `reason`, `requestedDate`, `amount`, `bucket` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `topupBalance` | `billing_payments.prepay_balance` | `/topupBalance`, `/topupBalance/{id}` | `id`, `href`, `confirmationDate`, `description`, `isAutoTopup`, `numberOfPeriods`, `reason`, `requestedDate` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF654 `transferBalance` | `billing_payments.prepay_balance` | `/transferBalance`, `/transferBalance/{id}` | `id`, `href`, `confirmationDate`, `description`, `reason`, `requestedDate`, `amount`, `bucket` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |

## V002 DDL Refinement

Migration: `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql`

The migration adds this implementation baseline for the app:

| Area | Decision |
| --- | --- |
| Common TMF fields | Add reusable typed columns such as `tmf_id`, `tmf_href`, `tmf_type`, `tmf_base_type`, `tmf_schema_location`, `tmf_referred_type`, `tmf_name`, `tmf_description`, `tmf_lifecycle_status`, `tmf_state`, dates, priority, and external ID to every V001 app table. |
| Full TMF compatibility | Keep the V001 `tmf_payload` column as the complete validated TMF resource snapshot for fields that are not yet promoted to typed columns. |
| Characteristics and references | Add normalized `tmf_characteristic`, `tmf_resource_reference`, `tmf_external_identifier`, `tmf_related_party`, `tmf_note`, `tmf_attachment`, and `tmf_relationship` support tables. |
| API/resource map | Add `tmf_api_resource_map` rows for the selected local TMF APIs and resource roots. |
| Event contracts | Add baseline event contract rows for create, update, state-change, and delete events per reviewed API resource. |
| Privacy and audit | Add table-level privacy, retention, legal-hold, residency, masking, and audit policy rows. |
| High-volume candidates | `billing_payments.event_outbox` |

## Event Contract Baseline

Events are registered in `billing_payments.event_contract` using `billing_payments.event_outbox` as the publication basis. Consumers must be added when integrations are designed; no app should directly write another app schema.

## Privacy, Retention, And Audit Baseline

| Table | Data classification | Retention class | Audit level |
| --- | --- | --- | --- |
| `billing_payments.billing_account_operation` | restricted | regulated_lifecycle | high |
| `billing_payments.bill_cycle` | restricted | regulated_lifecycle | high |
| `billing_payments.customer_bill` | restricted | regulated_lifecycle | high |
| `billing_payments.bill_item` | restricted | regulated_lifecycle | high |
| `billing_payments.payment` | restricted | regulated_lifecycle | high |
| `billing_payments.payment_allocation` | restricted | regulated_lifecycle | high |
| `billing_payments.payment_method_reference` | restricted | regulated_lifecycle | high |
| `billing_payments.prepay_balance` | restricted | regulated_lifecycle | high |
| `billing_payments.billing_adjustment` | restricted | regulated_lifecycle | high |
| `billing_payments.event_outbox` | restricted | regulated_lifecycle | high |

## Build Gate Result

| Gate item | Result |
| --- | --- |
| API/resource review | Complete for baseline implementation |
| V002 typed DDL | Complete: `database/postgres/suites/ts_bss_commercial/V005__refine_billing_payments_tmf_core.sql` |
| Event contract register | Baseline complete |
| Privacy/retention/audit classification | Baseline complete |
| Remaining implementation control | Validate exact endpoint operations and contract tests as Angular/Spring Boot features are built |
