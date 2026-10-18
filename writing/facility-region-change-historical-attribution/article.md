# The Facility Changed Regions. Did You Rewrite Last Quarter?

**Deck:** A current org chart is not a historical record. Multi-location operators need effective-dated facility membership, explicit attribution views and report receipts that preserve who was responsible when.

**By Jared Mastroianni**

<!-- BODY START -->

A self-storage facility moves from the East region to the Central region on October 1. The regional manager changes. The weekly scorecard refreshes. Then someone reruns September.

Suddenly, the facility’s September occupancy, delinquency, maintenance backlog and lead response appear under Central. East’s historical results improve or worsen without a September operating event. Central inherits results from a period it did not manage. Nobody edited a transaction. The dashboard simply joined old facts to today’s org chart.

That is not a cosmetic reporting problem. It changes the record of who operated what, which comparison is valid and where a leader should investigate a result.

The fix is to stop treating portfolio membership as a label on the facility record. Region, cluster, management company and accountable owner are relationships with effective dates. A trustworthy portfolio system preserves those relationships as records, then tells the reader which attribution view a report uses.

## The current org chart answers only one question

A facility master often contains one current region field. That is useful for routing today’s work. It is inadequate for reconstructing the past.

When a report asks, “How did the East region perform in September?” it needs the facilities that belonged to East during September under the report’s stated attribution rule. If the query instead takes every September transaction and joins it to the facility’s region today, it answers a different question: “What would September look like if we grouped historical transactions under the current structure?”

Both views can be useful. Neither should impersonate the other.

The Financial Accounting Standards Board’s conceptual framework describes comparability as the ability to identify similarities and differences among items. It also distinguishes comparability from mere uniformity: unlike things should not be made to look alike.[^1] That is financial-reporting guidance, not a self-storage regional-reporting rule. The design lesson still applies. A consistent-looking portfolio table is not meaningfully comparable if the facility population or accountability relationship changed underneath it.

## Store membership as an effective-dated relationship

Create a membership record for each period in which a facility belongs to a region, cluster or other operating group. At minimum, preserve:

- a stable facility identifier;
- the portfolio, region and cluster identifiers;
- the accountable operating role;
- the effective start and end;
- the source and approval for the assignment;
- when the record was entered;
- links to the preceding and succeeding memberships; and
- any correction or supersession relationship.

Do not overwrite `region=East` with `region=Central`. Close the East membership at the approved effective boundary and open the Central membership. The facility has not become two facilities. It has two time-bounded membership records.

This separation also handles late entry. Suppose the October 1 transfer is approved on September 25 but entered on October 4. The effective date describes when the organizational relationship was intended to apply. The recorded time describes when the system learned it. Preserving both lets an operator explain why a report run on October 2 differs from one run on October 5 without pretending that the earlier report had access to a record that did not yet exist.

The W3C PROV recommendation provides a general model for connecting entities, activities, agents, derivations, revisions and attribution.[^2] It does not prescribe a self-storage data model. It does support a useful principle: a report should retain enough provenance to identify the source records, transformation and responsible roles that produced it.

## Name the attribution view before calculating the metric

Every regional or portfolio report should declare its view. Three common views serve different decisions.

**As-operated view.** Attribute each facility-period to the region or operator responsible during that period. Use this view for historical accountability, manager coaching, operational trend review and questions about what a team actually controlled.

**Current-structure view.** Group historical facility results under today’s structure. This can help a current regional leader see the historical behavior of the facilities now in the territory. Label it clearly. It is a restated management view, not the historical org structure.

**Constant-population view.** Hold the facility set constant across comparison periods. This is useful when acquisitions, dispositions, transfers or temporary closures would otherwise make a trend look like operating improvement or decline. The report must state the population rule and exclusions.

Do not bury these choices in query logic. Put the attribution view, organization version, facility-population identifier and membership-rule version on the report itself.

## Keep performance time separate from responsibility time

One metric can contain several relevant dates:

- the period when the operating activity occurred;
- the membership period used to assign responsibility;
- the time the source record arrived;
- the time a correction became known; and
- the report’s as-of time.

Collapsing those into one date produces hard-to-diagnose errors. A late payment posted on October 3 but effective September 30 can change a September delinquency calculation. A region transfer effective October 1 should not change who owned the September result. A report rerun after both events should incorporate the supported payment correction while preserving September’s organizational attribution.

That requires two independent decisions: which operating facts belong in the metric, and which membership record governs the attribution. Do not let a change to one silently rewrite the other.

## Reconcile the transition, not just the totals

On the effective day of a region transfer, run a bounded transition check.

First, confirm there is no gap or overlap between the prior and new membership records unless the approved model expressly permits one. A facility should not disappear from every region for three days because one record ended before the next began. It also should not count in two regional totals because both records include the transfer date.

Second, inventory the downstream consumers that use region or manager assignment. The dashboard is only one. Work-order routing, emergency contacts, approval queues, vendor escalation, access review, budget ownership and notification lists may each carry their own copy.

Third, compare the facility population before and after the change. Reconcile counts and named facility identifiers, not only aggregate totals. A portfolio total can remain unchanged while one facility is duplicated and another is missing.

Fourth, preserve the report versions affected by the change. If a previously released report is materially restated, link the new version to the prior one and state why. Do not replace the old file and leave readers unable to explain the difference.

GAO’s data-reliability guide defines reliability in terms of accuracy, completeness and applicability for the intended purpose, and recommends a risk-based assessment using documentation, knowledgeable people, testing and source tracing.[^3] The guide governs government audit work, not private self-storage reporting. Its purpose test is especially useful here: the same regional dataset may be suitable for current routing but not suitable for historical accountability.

## Separate organizational correction from operational correction

A manager may discover that a facility was assigned to the wrong region for two weeks. Correct the membership record through an approved correction path. Do not rewrite the history without preserving the prior assertion, correction reason, approving authority and reports affected.

Then decide which reports require restatement. A current routing list may need immediate correction. A weekly management scorecard may need a labeled replacement. A compensation or formal financial process may have its own governance and review requirements. The membership ledger should identify affected consumers; it should not declare every downstream decision automatically corrected.

This matters for people as much as data. An unexplained restatement can make one regional manager appear to have improved and another to have declined. A controlled correction lets leadership distinguish an operating result from an attribution error.

## A fictional example

The following scenario is entirely fictional and illustrates the method; it is not a modSTORAGE facility, deployment or performance result.

Juniper Crossing Storage belongs to the fictional North region through September 30. An approved transfer places it in the fictional Central region effective October 1. The assignment is entered October 4.

The September regional scorecard uses `as_operated` attribution. Juniper Crossing remains in North because North held the membership during the metric period. A current-structure planning view groups the same facility’s historical trend under Central, but the report is labeled `current_structure_restatement` and carries a different report identifier.

On October 6, the team discovers that the Central membership was entered with an October 2 effective date. The corrected record preserves the superseded assertion, links to the approval, closes the one-day gap and identifies the October 4 and October 5 routing extracts as affected. The September scorecard is not restated because its membership period did not change.

The example does not prove that a particular transfer policy is correct. It shows how the record makes the policy visible and the consequences traceable.

## Use the ledger as a release gate

Before releasing a regional comparison, require the report owner to answer:

1. Which attribution view does this report use?
2. Which organization version and facility population support it?
3. Are membership gaps, overlaps or unknowns unresolved?
4. Were late-entered assignments evaluated against the report’s as-of time?
5. Can each facility-period resolve to one governed membership record?
6. If the report replaced an earlier version, is the restatement linked and explained?

If those answers are missing, the report may still be useful as a diagnostic draft. It is not ready to be treated as a stable portfolio comparison.

Multi-location operators do not need to freeze the org chart. Facilities will change regions, leaders and operating structures. The control is simpler: preserve the relationship that was true for each period, make the selected reporting view explicit, and leave a receipt when the interpretation changes.

A region transfer should change future responsibility. It should not silently rewrite the past.

<!-- BODY END -->

## Sources

[^1]: Financial Accounting Standards Board, [*Statement of Financial Accounting Concepts No. 8, Chapter 3: Qualitative Characteristics of Useful Financial Information, as amended*](https://storage.fasb.org/Concepts_Statement_8_Chapter_3_As_Amended.pdf), accessed October 16, 2026.
[^2]: World Wide Web Consortium, [*PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013; accessed October 16, 2026.
[^3]: U.S. Government Accountability Office, [*Assessing Data Reliability*](https://www.gao.gov/products/gao-20-283g), GAO-20-283G, December 16, 2019; accessed October 16, 2026.

## Disclosure

This article was developed with AI assistance under Jared Mastroianni’s direction and editorial control. The fictional scenario and dataset are labeled. No customer, facility, employee, deployment, performance result, accounting treatment or legal requirement is represented as real. Final policy, reporting and correction decisions belong to the operator’s authorized owners and applicable professional advisers.
