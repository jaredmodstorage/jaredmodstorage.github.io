---
title: "The Facility Is Temporarily Closed. Should It Still Count in the Portfolio?"
subtitle: "Build a Metric-Specific Inclusion Contract Before One Status Flag Rewrites the Story"
author: "Jared Mastroianni"
slot: "2026-11-21 midday systems"
slug: "temporarily-closed-facility-portfolio-inclusion-control"
canonical: "https://jaredmodstorage.github.io/writing/temporarily-closed-facility-portfolio-inclusion-control/"
---

# The Facility Is Temporarily Closed. Should It Still Count in the Portfolio?

## Build a Metric-Specific Inclusion Contract Before One Status Flag Rewrites the Story

**By Jared Mastroianni**

<!-- BODY START -->

A self-storage facility can stop accepting new move-ins while hundreds of customers still have agreements, belongings and payment obligations tied to the property. It can be closed to vehicle entry while the office answers calls. It can suspend public access while expenses continue, work orders remain open and managers coordinate recovery. It can reopen one floor before another.

None of those conditions is captured well by one field called `active`.

Yet a single active/inactive switch often controls whether a property appears in a portfolio dashboard, a comparison group, an alert population or an automated report. Once that switch changes, the same facility can vanish from occupancy, remain in payroll, disappear from lead conversion and continue contributing expenses. Each report may be technically faithful to its filter while the portfolio story becomes internally inconsistent.

The answer is not to keep every facility in every metric forever. It is to define inclusion by purpose, effective time and evidence. A temporary closure is an operating condition. Whether the facility belongs in a particular denominator is a separate governed decision.

## A facility can be open for one purpose and closed for another

Start by separating states that a convenient status field tends to compress.

**Physical operating state** describes what people can do at the property: enter the office, use the gate, reach a floor, load a unit or receive staff assistance.

**Commercial state** describes what the business is offering: new rentals, reservations, transfers, retail sales or other services.

**Customer-obligation state** describes what remains in force for existing customers: agreements, access arrangements, payment processing, notices, support and approved accommodations.

**System state** describes what connected tools currently permit or display: website availability, call routing, access-control commands, task queues, vendor work, alerts and integrations.

**Reporting state** describes which records enter a metric, report or cohort.

These states can change at different times and under different authority. A safety owner may restrict customer entry. A commercial owner may stop new rentals. An accounting process may continue to recognize approved activity. A reporting owner may retain the facility in a portfolio total but remove it from a same-store comparison. One decision should not silently make the others.

The U.S. Census Bureau defines an establishment as a single physical location where business is conducted or services or industrial operations are performed. That definition is useful for keeping the facility identity stable, not for deciding a private operator's metric treatment. The location does not become a different establishment every time its accessibility changes.[1](https://www.census.gov/naics/reference_files_tools/2022_NAICS_Manual.pdf)

## Give every denominator an inclusion contract

A rate is not governed merely because its formula is documented. The population underneath the formula needs its own definition.

For each portfolio metric, name:

- the business question the metric answers;
- the unit of analysis, such as facility, rentable unit, occupied unit, agreement or lead;
- the facility states that are eligible;
- the event time or as-of time used to determine eligibility;
- the treatment of partial operations;
- the owner who can approve an exception;
- the evidence required to apply the rule; and
- the version and effective date of the rule.

Consider occupancy. If a temporarily inaccessible building still contains occupied units and valid agreements, removing the facility may erase real obligations. Keeping every unit in the denominator without identifying unrentable or inaccessible space can also obscure the operating condition. The correct treatment depends on the defined question and the governed source fields, not on which result looks cleaner.

Now consider lead conversion. A facility that intentionally suspended new inquiries may have no eligible leads for part of the period. Including it as though demand generation continued can answer the wrong question. Excluding the entire month can also discard valid pre-closure activity. A daily or event-bounded population may be more faithful than a monthly facility flag.

Expenses present another problem. Utilities, security, remediation and staffing can continue during a closure. A report that excludes the property from operating expenses because it is inactive does not make those obligations disappear. It merely breaks the connection between the expense and the facility condition that produced it.

The contract should make these differences visible. “Included,” “excluded” and “partially included” are conclusions. Each needs a reason, scope and effective interval.

## Preserve the effective-dated state instead of overwriting it

Do not replace yesterday's `open` with today's `temporarily_closed` and lose the transition. Record the change as an effective-dated event.

At minimum, capture the stable facility ID, prior state, new state, affected operating scope, reason class, source authority, approver, effective timestamp with time zone, expected review time, evidence reference and actual end timestamp when known. Keep the reported condition separate from the approved portfolio treatment.

This is change control applied to operating data. NIST SP 800-53 Revision 5 describes configuration change control as a systematic process for proposing, justifying, implementing, testing, reviewing and disposing of changes, with records retained and changes monitored. Its controls are written for information systems and do not certify a self-storage reporting process. The useful principle is that a consequential state change should have an authorized proposal, impact review, implementation record and post-change verification.[2](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final)

Before the effective time, identify every report and automation that consumes the status. A field may control more than a dashboard filter. It may suppress a website listing, change a call queue, stop a scheduled export, remove alerts or alter a manager's task population. Treat those as downstream consequences to review, not convenient side effects.

After the change, read the governing records back. Verify the physical and commercial restrictions on their own surfaces. Then verify each metric population against its inclusion contract. A successful status update is execution evidence. It is not proof that every downstream population now tells the intended story.

## A fictional eight-facility portfolio

The following example is entirely fictional. Stonehaven Loop Storage, its eight facilities, people, systems, identifiers, dates, conditions and results are invented teaching material. They do not describe modSTORAGE, a customer or a real deployment.

In the fictional scenario, facility `SLS-04` restricts customer entry for twelve days after a water event. The office answers calls remotely. New rentals and move-ins are paused. Existing agreements remain in force. Payments continue through approved channels. Remediation expenses and vendor work continue. One unaffected building returns to scheduled access before the affected building.

The legacy facility master has one status field. An analyst changes it from `active` to `inactive` on the first day. That action removes `SLS-04` from physical occupancy, economic occupancy, lead conversion, work-order aging and portfolio expense per square foot. A separate payroll report continues to include it because that report uses a different facility list.

Nothing about those conflicting results establishes the correct metric treatment. The problem is that one label made five decisions without showing any of them.

Stonehaven's fictional team restores the stable facility identity and records the closure as a scoped, effective-dated operating event. It then applies metric-specific rules. Existing occupied units remain in the occupancy population with the restriction visible. New-rental conversion uses only eligible inquiry periods and carries the paused interval as excluded time. Work-order aging continues because open obligations still require ownership. Expenses remain assigned to the facility. A same-store commercial-performance view places the facility in a separately disclosed exception cohort for the affected interval.

These choices are illustrative, not universal accounting or operating rules. Their value is that each decision can be examined. A reviewer can see the question, eligible population, state source, effective interval, approver and evidence instead of reverse-engineering the treatment from a dashboard total.

## Keep actual, eligible and comparable populations separate

Portfolio reporting becomes easier to defend when it distinguishes three populations.

The **actual population** is what existed at the as-of time: the facilities, units, agreements, leads, costs or tasks recorded by their governing sources.

The **eligible population** is the portion admitted by the current metric contract. It carries the inclusion rule, exclusions and exception states.

The **comparable population** is a cohort constructed for a specific comparison. It may require consistent operating exposure, data coverage or business conditions across periods.

Do not overwrite actual history to create comparability. Keep the underlying records and publish the cohort rule beside the comparison. If a facility is removed from a same-store view, the portfolio should still be able to show that it existed, why it was excluded, the interval affected and where its actual activity remains represented.

The U.S. Government Accountability Office's data-reliability guide frames reliability around accuracy, completeness and applicability for the intended purpose. It is audit guidance, not a private self-storage reporting standard. Its purpose test is still useful: a dataset can be accurate and complete for one question yet unsuitable for another.[3](https://www.gao.gov/products/gao-20-283g)

For every dashboard, expose at least the eligible facility count, excluded facility count, partial-state count, as-of time and rule version. A percentage without those elements invites false precision. A trend line should identify cohort changes rather than silently redraw prior periods.

## Trace every published number back to the state decision

When a report is generated, retain the facility population, metric-contract version and source-state version used for that run. If the closure decision is corrected later, do not silently regenerate history and present it as though it were the original result.

W3C's PROV-O recommendation provides a formal way to describe entities, activities and agents involved in producing information. A self-storage operator does not need to adopt the ontology to preserve useful provenance. A practical record can still connect the report to its inputs, transformation, rule, accountable owner and generation time.[4](https://www.w3.org/TR/prov-o/)

That lineage makes a correction manageable. The team can identify which dashboards used the old state, which decisions depended on them and which published outputs need a visible restatement. It also prevents a temporary closure from becoming a permanent mystery in the historical data.

## Use the Facility Status and Metric Inclusion Register

The accompanying register turns the method into an operating record. Create one facility-state event, then add one row for each affected metric or automation. Do not copy one inclusion decision across every row.

| Control | Required evidence |
| --- | --- |
| Facility identity | Stable facility ID and governing source |
| Operating event | Scope, reason class, start time, review time and actual end time |
| Source authority | Named role and evidence reference for the condition |
| Metric purpose | The exact question and unit of analysis |
| Inclusion rule | Eligible states, partial-state treatment and rule version |
| Decision | Included, excluded, partial or held, with reason |
| Impact | Numerator, denominator, comparison cohort and downstream automations |
| Approval | Accountable owner, decision time and exception authority |
| Readback | Actual population observed after the change |
| Reconciliation | Variances, owner, due time and closure evidence |

Use `held` when the source condition, rule or authority is missing. Do not convert unknown into excluded. The blank CSV supports implementation; the completed fictional CSV shows how different metrics can reach different decisions for the same operating event without contradicting one another.

## Reopening is another controlled change

When the facility returns, do not simply flip the old flag back to active. Record which scope reopened, when it became available, who verified it and which restrictions remain. A property may resume office service before customer access, or reopen one building while another remains controlled.

Re-evaluate each metric contract at the new effective time. Close the prior interval without erasing it. Verify current website, access, task, alert and reporting populations. If the comparative cohort has a minimum exposure rule, reopening does not automatically restore comparability for the whole period.

The goal is not a more elaborate status vocabulary. It is a portfolio that can explain why a facility counted, where it counted, during which interval and under whose authority.

A temporary closure should change the operation. It should not be allowed to rewrite the portfolio by accident.

<!-- BODY END -->

## Sources

1. U.S. Census Bureau, [*2022 North American Industry Classification System Manual*](https://www.census.gov/naics/reference_files_tools/2022_NAICS_Manual.pdf), accessed November 22, 2026. Used only for the establishment-versus-enterprise identity distinction; it does not determine a private operator's metric population.
2. National Institute of Standards and Technology, [*SP 800-53 Revision 5, Security and Privacy Controls for Information Systems and Organizations*](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), including the August 27, 2025 Release 5.2.0 notice; accessed November 22, 2026. Used by analogy for documented configuration change control, impact review and auditability; no NIST compliance claim is made.
3. U.S. Government Accountability Office, [*Assessing Data Reliability*, GAO-20-283G](https://www.gao.gov/products/gao-20-283g), publicly released December 16, 2019; accessed November 22, 2026. Federal audit guidance used for its stated accuracy, completeness and applicability concepts, not as a private-sector reporting mandate.
4. World Wide Web Consortium, [*PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013; accessed November 22, 2026. Used for provenance concepts; the article does not claim an implementation of the ontology.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial production note

Research, drafting, structured-tool production and QA were completed with AI assistance under Jared Mastroianni's direction. The final article remains bounded by the sources, fictional-example labels and claim limitations recorded in this package.
