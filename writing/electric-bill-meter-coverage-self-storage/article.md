---
title: "The Electric Bill Jumped. What Does the Meter Actually Cover?"
slug: electric-bill-meter-coverage-self-storage
author: Jared Mastroianni
intended_slot: 2026-11-24 midday systems
assigned_destination: Jared Mastroianni personal authority site
canonical: https://jaredmodstorage.github.io/writing/electric-bill-meter-coverage-self-storage/
publisher_owner: Master Personal Site Authority
description: "A reconciliation method for multi-site self-storage teams comparing electric bills, meter coverage and billed usage before assigning an operating variance."
---

# The Electric Bill Jumped. What Does the Meter Actually Cover?

By Jared Mastroianni

![Jared Mastroianni and a technician talk in a storage corridor in an AI-generated editorial illustration.](assets/015-professional-technician-walkthrough.png)

*A walkthrough gives the facilities team context for checking the utility records. AI-generated editorial illustration.*

<!-- BODY_START -->

In a fictional portfolio review, Cobalt Marsh Storage lands at the top of the electric expense report. Its latest bill is $3,540. The previous one was $2,400. A regional manager is ready to call the site and ask why the climate-controlled building used so much more power.

The two bills tell a narrower story. The first lists 12,000 kilowatt-hours across 30 service days. The second lists 14,000 across 35. Both average 400 kilowatt-hours a day. The newer statement includes an earlier-period adjustment, and an expansion behind the same service meter opened during that billing cycle. The bill increased by 47.5 percent. Explaining that increase and comparing the buildings are now two different assignments.

For a multi-site operator, a utility variance has three parts. What did the utility charge? What energy did it report for the service dates? What did the contributing meters serve during those dates? Give the first question to the person who can read and reconcile the invoice. Give the third to someone who knows the building and can verify the service boundary. The second becomes much more useful once both have done their work.

## Put the invoice and the meter on different rows

Accounts payable needs to know which account was billed, which document is current and which amount the company owes. Facilities needs the electricity quantity and the part of the property it covers. One statement can support both jobs. Your data model should give each its own record.

Keep the original invoice ID, account reference, statement date and relevant charge lines together. On a linked usage record, preserve the service start and end, billed service days, meter or utility aggregation identifier, reported kilowatt-hours, read status and billed demand if present. Record the effective statement version. A corrected document should point to the document it replaced so a reviewer can reproduce what the dashboard showed at the original close.

The U.S. Energy Information Administration distinguishes power in kilowatts from energy used over time in kilowatt-hours. So give the two different columns. A billed demand figure also needs its own description from the utility bill or account terms before you compare it with another site's figure. Keep supply, delivery, demand-related charges, fixed charges, taxes and prior-period items distinct wherever the statement breaks them out. Two bills can show the same daily usage while carrying different charges. [EIA, Measuring Electricity](https://www.eia.gov/energyexplained/electricity/measuring-electricity.php)

Keep current-period charges apart from an amount due that may reflect prior balances or credits. If the source will only support a total and a short list of adjustments, retain that level of detail. A guessed allocation makes the portfolio report look more precise than the underlying documents.

## Map the space each meter actually serves

Start with the facility ID. Add the utility account and service point, meter or aggregate ID, effective dates and the area or load it serves. At a self-storage property that could include a heated office, conditioned storage buildings, a gate, yard lighting or a separately operated space. A second provider account can cover a real part of the property while being invisible to the analyst who imports bills from the first. A former meter can also carry the same site name as its replacement.

Ask the site or facilities lead to confirm the boundary from the records they are authorized to use. Use the provider's service record, documented building or electrical information and qualified confirmation where mapping remains uncertain. Record the evidence reference and date. Keep a coverage status of whole property, partial property, shared service or unresolved. Add a start and end date when a meter relationship changes. This is a records review. Questions that require opening equipment or verifying electrical connections belong with qualified personnel.

Two situations deserve special attention. A master bill and a submeter can describe some of the same electricity. Use the master for its verified scope and the submeter as a breakdown where it sits underneath that total. Separately, a shared service may span a storage building and an unrelated use. Keep it labeled as shared unless you have a supportable allocation method. Where an allocation is useful for internal review, publish its basis and keep allocated use distinct from measured use.

EPA's Portfolio Manager instructions provide a useful precedent. They ask operators to identify what meters measure, specify partial coverage and look for unusual gaps or overlaps in billing periods. The product's rules govern its own calculations. For an internal portfolio, I would also ask which consumption is missing, which entries represent the same load and what date each answer became true. [EPA ENERGY STAR, How to Get Utility Data into Portfolio Manager](https://www.energystar.gov/sites/default/files/2025-01/How%20to%20Get%20utility%20data%20into%20Portfolio%20Manager_December%202024.pdf)

## Build a comparison that can survive a corrected bill

Put service dates on the usage view and keep posting dates available for accounts payable. Use the utility's service-day count when supplied. For automated gap checks, first establish whether each feed treats its end date as the last included day or the next read boundary. Preserve the raw dates and document any conversion before comparing feeds. A one-day discrepancy can be a convention issue. An entire missing statement calls for a source check.

Record whether the utility marks each reading as actual, estimated or unspecified. Con Edison, for example, describes an estimated read as a projection used when an actual read is unavailable. Read labels and correction mechanics depend on the serving utility and account. A subsequent actual read can coexist with an earlier estimate on the source statements. Inspect the provider's documents to see what period was reconciled and which usage or charge lines changed before amending the operating history. [Con Edison, Your Guide to Rates](https://www.coned.com/en/accounts-billing/your-bill/your-guide-to-rates)

Build three review states into the report. A **comparable** row has a verified boundary, suitable dates and sufficient use evidence for the stated comparison. A **provisional** row can remain visible as context with a named reason, such as an estimated read or a calendar-month allocation. A **held** row has an unresolved gap, overlap or material boundary change that makes the requested comparison unreliable. Show how many sites qualify beside the total or rank so withheld rows never disappear into the baseline.

When a correction arrives, preserve the former record and mark the scope of the replacement. Recompute the affected service periods from the governing records, check the difference against the previous report and issue a dated revision to anyone using that report to make decisions. Route an amount change to accounts payable and a usage change to the report owner. A billing revision can affect either or both.

## Use daily averages to screen and comparable periods to investigate

For one verified meter over an unchanged scope, billed kilowatt-hours divided by service days can help screen bills of different lengths. Keep the original totals beside the averages. Both numbers carry useful information. A longer billing period can explain a larger energy quantity, and a shift in the daily average can prompt a closer look.

For a month-by-month ranking, calendar dates are a separate decision. Site bills may close on different dates. Where reliable interval readings cover the period, use those with the reconciled meter scope. If you prorate bills by days overlapping the month, mark the result as an allocation based on uniform daily use. That assumption can be weak around a heat wave, a change in operating hours or the commissioning of new space. Use it for the level of decision the evidence can support.

Across stores, group sites by operating characteristics and coverage before comparing use intensity. An enclosed climate-controlled building and a drive-up property with an office and perimeter lighting serve customers in different ways. Start with similar sites or the site's own prior period. If you divide by area, specify the area served by the measured loads and document whether it is gross floor area or some other defined measure. An office-only meter divided by the whole property's rentable area will produce an attractive number and a useless diagnosis. EPA's benchmarking guidance likewise suggests grouping buildings by characteristics such as function, location, size and metering. [EPA ENERGY STAR, Analyze Benchmarking Results](https://www.energystar.gov/buildings/benchmark/analyze-benchmarking-results)

Return to the fictional Cobalt Marsh review. The 400-kilowatt-hour daily averages are arithmetically correct. The expansion means the second average spans two physical operating scopes, so the site stays out of a like-for-like ranking for that cycle. The analyst can still report the bill and metered usage with the scope change visible. Accounts payable can work the adjustment from the source statement. Facilities can confirm the expansion date and begin a new comparison window, using the earlier scope only where the records support it.

## Assign the variance to someone who can answer it

The most expensive report is one that sends everyone looking in the wrong place. An unexplained charge belongs with the billing owner. An unknown account or load belongs with facilities and the utility account owner. A verified usage shift goes to the site or engineering lead with the service period, verified meter coverage and the documented operating changes to check. Give each exception an owner, a date and the evidence that will close it.

That last route is where operating judgment matters. If the evidence points to a real load change, ask what happened on the site before anyone proposes a setback, a lighting change or a capital project. Bring operating schedules, equipment work orders and approved environmental requirements into the review. Protect the service the customer rented while the technical owner determines whether there is an avoidable load.

Use the companion electric-bill reconciliation worksheet on two locations and their last two statements. Start with one climate-controlled site and one different configuration so the coverage problems are easy to surface. Then use the same checks on a matched pair. The first pass should tell you which numbers you can explain, which comparisons you can defend and who will resolve the rest. Once you can answer those questions on demand, the ranking has a job it can actually do.

<!-- BODY_END -->
