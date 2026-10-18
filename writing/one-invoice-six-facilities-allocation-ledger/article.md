# One Invoice, Six Facilities: The Allocation Ledger Behind Comparable Operating Costs

**Deck:** A shared vendor bill does not become facility-level operating data when someone divides it by six. It becomes comparable only when the benefited sites, allocation basis, service period, residual and posting evidence are visible.

**By Jared Mastroianni**

<!-- BODY START -->

A vendor sends one invoice for work across six self-storage facilities. The total is correct. The purchase order matches. The invoice is approved.

Then someone splits the amount evenly across the portfolio.

That may be reasonable. It may also be wrong in a way that survives every top-level check. One site may have received most of the work. Another may not have been in service for the full period. A third may have a direct line item buried in the attachment. If the allocation logic is invisible, the general ledger can balance while facility comparisons drift.

This is not merely an accounting concern. Allocated costs flow into property reviews, vendor evaluations, maintenance planning, operating budgets and decisions about where a problem is growing. When the basis changes quietly from month to month, managers can appear to improve or deteriorate without any change in the work performed.

The operating requirement is straightforward: **treat every shared-cost allocation as a governed transformation, not a spreadsheet convenience.** Preserve the source invoice. Identify what each facility benefited from. Record the rule that converts that evidence into facility amounts. Reconcile the result to the source total. Then verify what was actually posted.

## Begin with the cost object, not the formula

Before choosing square footage, unit count, transaction volume or an even split, define what is being assigned.

A cost object is the thing that will receive the amount. In a self-storage portfolio, that may be a facility, region, project, operating function or period. “Operations” is too broad. “Facility `FAC-204` for the September 2026 pest-control service period” is usable because the identity, purpose and time boundary are explicit.

The invoice itself is not always one cost object. It may contain direct work for one site, a shared base fee, taxes, credits, after-hours charges and work outside the current period. Split it into allocation components before applying a single formula to the total.

Use direct evidence first. If a vendor attachment states that three hours were spent at one facility and one hour at another, those line items should not be overwritten by a portfolio-wide unit-count ratio. Allocate only the genuinely shared remainder.

This article offers an operating-control method, not a determination of generally accepted accounting principles, tax treatment, capitalization, contract compliance or legal responsibility. The company’s finance, accounting, tax and legal owners still govern those conclusions.

## Define who actually benefited

The most common allocation error begins before the math: the eligible facility set is wrong.

A six-site contract does not prove that every invoice benefited all six sites during the billed period. A facility may have joined the contract midmonth. One may have a separate service agreement. Another may have been excluded from a scheduled visit. A credit may apply only to the location where work was missed.

Create an eligibility row for every candidate facility with:

- stable facility ID and display name;
- service-period start and end;
- eligibility state;
- evidence reference;
- inclusion or exclusion reason; and
- reviewer and review time.

Use exact states such as `eligible`, `ineligible`, `direct-charge-only`, `shared-benefit-unverified` and `held`. Do not turn an unverified facility into an eligible one simply to make the denominator complete.

The federal cost-allocation rule in 2 CFR 200.405 uses “relative benefits received” and allows reasonable documented methods when exact proportions cannot be determined. That rule applies to federal awards, not ordinary self-storage operations. It is cited here for a narrow design lesson: allocation needs a relationship between the cost and the benefited objective, and approximation should be documented rather than disguised as precision.[^1]

## Choose a basis that explains the work

An allocation basis should represent the way the service was consumed or the benefit was received. No single basis works for every invoice.

Examples include:

- **Direct vendor detail:** documented visits, hours, devices, inspections or line items by facility.
- **Measured consumption:** approved usage records for utilities or metered services.
- **Relevant asset count:** covered gates, cameras, HVAC units or other assets actually within service scope.
- **Activity volume:** completed transactions, calls or tickets when the charge genuinely varies with that activity.
- **Time in scope:** eligible facility-days when a fixed shared service applies over a period.
- **Equal split:** appropriate only when the service and benefit are reasonably equal and the rationale is recorded.

Square footage and unit count are convenient, but convenience is not causation. Unit count may be a defensible proxy for a service that scales with occupied storage capacity. It is a weak proxy for a fixed software license, a site-specific repair or work driven by the number of access devices.

Give every approved basis a version. Record its numerator definition, denominator definition, source, effective date, owner, rounding rule and conditions that force review. If the basis changes, do not overwrite the prior version. The change may alter comparisons even when the invoice total is unchanged.

## Keep the arithmetic reproducible

For each shared component, the calculation can be simple:

> Facility allocation = allocable component amount × facility basis quantity ÷ eligible basis total

Simple does not mean self-explanatory. The ledger should retain the source amount, basis quantity, denominator, unrounded result, rounding result and final assigned amount for every facility.

Rounding deserves its own rule. Six independently rounded rows may not add back to the invoice component. The residual might be one cent or several cents, depending on currency, quantity and formula. Assign that residual through an approved deterministic rule—for example, to the eligible row with the largest fractional remainder—and identify the receiving row. Do not hide the difference in a manually overwritten total.

Credits, rebates and adjustments also need lineage. A credit tied to one facility should follow that facility unless an authorized accounting rule says otherwise. A general contract credit may use the same benefited-facility set and basis as the original shared charge. In either case, link it to the original invoice or allocation event.

The W3C PROV-O Recommendation defines a general model for describing entities, activities, agents, derivations and responsibility across systems. It does not prescribe a self-storage ledger. Its structure supports a useful technical pattern: the source invoice is an entity, the allocation is an activity, facility rows are derived entities, and named owners are responsible agents.[^2]

## Separate calculated, approved and posted

An allocation workbook is not the accounting system. Preserve these as different states:

1. **Prepared:** the benefited set, components and basis have been assembled.
2. **Calculated:** the facility rows reconcile mathematically to the source components.
3. **Reviewed:** an authorized reviewer accepts the eligibility, basis and exceptions.
4. **Approved for posting:** the appropriate owner authorizes the specific allocation version.
5. **Posted:** a system or person reports that entries were accepted.
6. **Read back:** the exact facility, period and amount are visible in the governing destination.
7. **Reconciled:** the readback amounts equal the approved allocation and source total, subject to recorded scope.
8. **Closed:** discrepancies and exceptions are resolved or transferred to named open items.

A successful import receipt is not readback. A balanced allocation file is not proof of posting. A posted batch is not reconciled if one facility landed in the wrong property, department or period.

The U.S. Government Accountability Office’s 2025 Green Book is mandatory for federal executive agencies and optional as a framework for certain nonfederal organizations. It is not a self-storage accounting standard. Its emphasis on documented internal controls, reliable reporting and control activities is still a useful reference for separating authorization, processing, verification and evidence.[^3]

## A fictional six-facility allocation

Consider **Harborline Storage Group**, an entirely fictional six-facility operator. A fictional vendor invoice totals **$6,480** for a one-month preventive-maintenance program.

The invoice contains three components:

- $1,200 of documented direct work at Harborline East;
- a $180 site-specific credit for a missed visit at Harborline North; and
- $5,460 of genuinely shared program cost.

The shared program covers eligible facility-days. Five sites were eligible for all 30 days. Harborline Annex joined the program on day 16, so it has 15 eligible days. The denominator is 165 facility-days, not six facilities and not 180 facility-days.

Each full-period site receives 30 ÷ 165 of the shared component, or an unrounded $992.7272. The Annex receives 15 ÷ 165, or an unrounded $496.3636. The approved rounding rule resolves the one-cent difference created by independently rounding all six rows, using fractional remainder and stable facility ID. Harborline East then receives its direct $1,200. Harborline North receives its site-specific $180 credit.

The final facility rows add to $6,480. That mathematical agreement is necessary, but it is not the release decision. The reviewer still checks the service-period evidence, confirms the Annex effective date, verifies that the credit is site-specific, approves the basis version and compares the posted destination rows to the approved ledger.

Every facility, vendor, amount, invoice, service event and result in this example is fictional. It demonstrates the method and does not report a real customer, provider relationship, operating expense, posting, savings or performance result.

## Make comparability visible in the monthly review

Facility leaders should not have to open the allocation workbook to discover that a cost moved because the basis changed.

For every allocated metric shown in a portfolio review, include:

- allocated amount;
- source invoice and component identity;
- basis name and version;
- eligibility-set version;
- direct versus shared amount;
- allocation status;
- prior-period comparability state; and
- open exception count.

Use comparability states such as `comparable`, `comparable_after_restated_basis`, `not_comparable_basis_change`, `held_source_gap` and `held_posting_mismatch`. A manager can then distinguish a real operating change from a change in allocation mechanics.

Do not restate history merely to smooth a chart. Restatement should have an owner, scope, reason, approved method and preserved prior version. Sometimes the right answer is to leave the earlier period unchanged and mark the break in comparability.

## The next portfolio review

Take one shared vendor invoice currently spread across facilities and ask eight questions:

1. What exact component is being allocated?
2. Which facilities benefited during the stated service period?
3. Which amounts have direct evidence and should bypass the shared formula?
4. What basis best explains the shared benefit?
5. Where are the numerator, denominator, source and version recorded?
6. How is the rounding residual assigned?
7. Who approved the calculated allocation?
8. What destination readback proves the facility rows were posted as approved?

If those questions cannot be answered, the total may still be correct. The facility story is not ready.

The accompanying **Shared-Service Allocation and Reconciliation Ledger** provides a component register, facility allocation rows, posting readback fields and a fictional worked example. Its purpose is not to make every allocation complicated. It is to make the consequential assumptions visible before they become operating facts.

Comparable facility costs are built one transformation at a time. Preserve the invoice. Name the benefited facilities. Use a basis that explains the work. Reconcile the math. Verify the posting. Then let the portfolio compare.

<!-- BODY END -->

---

## Operator tool

Use the accompanying **Shared-Service Allocation and Reconciliation Ledger** and CSV template. The fictional example demonstrates direct charges, a site-specific credit, eligible facility-days, deterministic rounding, approval and posting readback without representing an actual vendor or portfolio result.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. His work focuses on facility operations, multi-location systems, data governance and responsible artificial intelligence.

## Sources

[^1]: Electronic Code of Federal Regulations, 2 CFR 200.405, “Allocable costs,” current text reviewed October 18, 2026: https://www.ecfr.gov/current/title-2/part-200/section-200.405
[^2]: World Wide Web Consortium, “PROV-O: The PROV Ontology,” W3C Recommendation, April 30, 2013, reviewed October 18, 2026: https://www.w3.org/TR/prov-o/
[^3]: U.S. Government Accountability Office, “The Green Book,” 2025 revision effective beginning fiscal year 2026, reviewed October 18, 2026: https://www.gao.gov/greenbook

## Disclosure

This article and its operator tool were produced with AI assistance under human direction and review. The governed editorial image is AI-generated and is not documentary evidence of a real invoice, vendor, facility, meeting, allocation, posting or result.
