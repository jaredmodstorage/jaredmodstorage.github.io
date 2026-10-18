# The Facility Added 38 Units. Did Last Year's Occupancy Rate Change Too?

## A capacity denominator is a versioned operating record, not a field someone should overwrite

By Jared Mastroianni

<!-- BODY START -->

A self-storage facility completes an expansion and adds 38 units. The property-management system now shows the larger unit count. The portfolio dashboard refreshes. Occupancy drops.

Nothing happened to the occupied units. The denominator changed.

That can be the correct current result. It can also create a false historical trend if the new capacity is written over the old value and every prior period is recalculated as though the expansion had always existed. A manager reviewing last year's performance may see a lower occupancy rate that nobody reported last year. A regional comparison may reward one site and penalize another because their capacity changes were handled differently.

The operating problem is not the arithmetic. It is the identity and lifetime of the denominator.

For a multi-location portfolio, unit count and net rentable square footage should be governed as effective-dated capacity records. Each change needs a source, physical scope, definition, effective time, approval, downstream impact, and explicit treatment of prior periods. The old record should remain available for the periods in which it was true.

## Begin with the metric contract

“Occupancy” is incomplete without its basis. At minimum, a portfolio should distinguish:

- occupied units divided by eligible units;
- occupied rentable square feet divided by eligible rentable square feet;
- an end-of-period observation from an average over a period; and
- a whole-portfolio result from a same-store or otherwise bounded cohort.

Those figures can move differently. Converting one 10-by-20 unit into two 10-by-10 units may increase unit count without changing rentable square footage. Adding a new building may increase both. Taking units permanently out of service may reduce a governed capacity definition, while a short repair restriction may belong in availability rather than physical capacity. There is no safe default that covers every use.

Public filings illustrate why definitions matter. Public Storage's 2025 Form 10-K defines its same-store pool and says the composition helps evaluate ongoing performance while excluding fill-up effects from unstabilized facilities. It also warns that other REITs may calculate same-store facilities differently, limiting comparability. Extra Space Storage's 2025 Form 10-K reports net leasable square footage, net leased square footage, and square-foot occupancy together for its same-store portfolio. These are company-specific public disclosures, not universal self-storage rules. Their value here is the discipline: population, numerator, denominator, period, and limitation are made visible.

Write the internal contract before changing data. Name the metric, formula, unit of measure, cohort, observation timing, exclusion rules, rounding rule, and accountable owner. If a dashboard cannot show which contract generated the percentage, the percentage is not ready for cross-site comparison.

## Give capacity its own identity

Do not store “650 units” as a timeless attribute of the facility. Create a capacity record with an identifier and an effective interval.

A minimum record should include:

- stable facility ID;
- capacity-definition ID and version;
- effective-from time and, when superseded, effective-through time;
- unit count and rentable-square-foot values under that definition;
- physical scope, including buildings or floors included;
- source document, source system, and extraction or measurement method;
- reason for change;
- local verifier, portfolio reviewer, and approval state; and
- correction link when a prior record was wrong.

The W3C Provenance constraints explain a general versioning principle: when relevant attributes change over time, provenance can describe multiple entities, each with its own identifier, lifetime, and fixed attributes, linked through events. A self-storage capacity ledger does not need to implement the W3C model to use that lesson. Capacity version `CAP-07` can remain the record for one interval, while `CAP-08` becomes effective after the expansion. The physical facility is continuous; its governed description changes.

This also protects corrections. If the old square footage was wrong because of a transcription error, create a corrected version that identifies what was corrected and why. Do not disguise a correction as an expansion or silently edit the source value.

## Separate four events that teams often collapse

One construction project can create at least four different dates:

1. **Physical completion:** the space exists in its completed form.
2. **Operating acceptance:** the organization has accepted the space for the intended use.
3. **System activation:** units appear in the management or inventory system.
4. **Metric effectiveness:** the approved capacity definition includes them for a named report.

These dates may coincide, but they are not interchangeable. An import timestamp does not prove the units were rentable. A certificate, inspection, or contractor handoff may be relevant under local requirements and organizational policy, but this article does not determine which authorization is sufficient. The portfolio needs the evidence named by its approved process.

Record the metric-effective time explicitly. If 38 new units become eligible at noon on May 1, define whether an end-of-day report includes them and how a monthly average handles the partial period. If the system only supports dates, document the chosen boundary rather than allowing different analysts to infer different times.

## Decide what happens to history

A denominator change requires one of three declared treatments.

**Prospective treatment** preserves prior published observations under the capacity version that governed them and uses the new version from its effective date. This is usually the clearest representation of a real physical change.

**Controlled restatement** recalculates prior observations because the earlier capacity record was erroneous or because a governed reporting rule requires a consistent recast. A restatement needs a reason, affected period, prior and replacement results, approval, and a visible revision marker. It should not erase the original publication or pretend the replacement was the value previously reported.

**Not comparable** marks a period or facility when the change prevents a responsible like-for-like comparison. The report may still show the observations, but it should not manufacture a trend line across an unbridged definition change.

Do not choose the treatment because one produces a better chart. Choose it from the nature of the event and the reporting contract. An added building is not the same as correcting a mistyped square-foot value. A unit combination is not the same as temporarily blocking rentals during work.

## Preview the denominator effect before release

Before the new capacity version reaches production reporting, calculate the impact using a frozen numerator snapshot.

Show at least:

- prior and proposed unit capacity;
- prior and proposed rentable-square-foot capacity;
- occupied units and occupied square feet at the comparison instant;
- occupancy under both definitions;
- affected cohort and reports; and
- whether the difference reflects physical change, correction, or definition change.

The W3C RDF Data Cube recommendation describes statistical observations as measured values located by dimensions such as time and area, with metadata describing what was measured, how it was measured, units, and status. It also notes that an explicit data structure helps detect incoherent combinations of differently structured source data. In practical terms, “84.3%” should travel with facility, period, measure, unit, cohort, capacity version, and status—not as an orphan percentage.

Run the old and proposed versions side by side for a bounded review. That is not permission to keep two live definitions indefinitely. The review should have an owner, an end condition, and a release decision.

## A fictional example: Cedar Quay Storage

The following facility, counts, measurements, people, systems, dates, reports, and outcomes are entirely fictional.

Fictional Cedar Quay Storage operates 612 units containing 59,400 rentable square feet under capacity version `CQS-CAP-07`. A completed expansion adds 38 units and 3,800 rentable square feet. The proposed record `CQS-CAP-08` contains 650 units and 63,200 rentable square feet.

At the fictional comparison instant, 548 units and 53,100 rentable square feet are occupied. Under the prior capacity, unit occupancy is 89.5 percent and square-foot occupancy is 89.4 percent. Under the proposed capacity, the same occupied inventory produces 84.3 percent unit occupancy and 84.0 percent square-foot occupancy. The drop is a denominator effect, not a move-out event.

The portfolio team sets the new record prospectively from the approved metric-effective time. It does not rewrite April's dashboard. May is marked with a capacity-change annotation, and the same-store comparison remains held until the portfolio owner applies the existing cohort rule. The management system, BI model, budgeting workbook, regional scorecard, and scheduled board report are reconciled to the same capacity version.

No real facility or result is represented. The figures demonstrate the control; they are not a benchmark or recommended threshold.

## Reconcile every downstream consumer

A correct master record can still leave the portfolio inconsistent. Search for every place the denominator is copied, cached, derived, or manually maintained:

- property-management and unit-inventory systems;
- business-intelligence models and semantic layers;
- budgeting and forecasting workbooks;
- revenue-management inputs;
- regional scorecards and incentive reports;
- board, lender, owner, or investor packages;
- scheduled exports and data warehouses; and
- public facility pages when they state capacity facts.

For each consumer, record the prior version, target version, refresh or recompute job, completion evidence, and reconciliation result. A successful pipeline run proves execution, not parity. Compare facility coverage, totals, effective periods, and a sample of underlying units or spaces.

Keep disclosure scope separate. An internal operating capacity record does not automatically authorize a public statement. A public filing or website update has its own owner, materiality review, and publication state.

## The operator tool: Portfolio Capacity Denominator Change Ledger

The companion ledger makes the change reviewable. It binds one physical event to:

- the prior and proposed capacity versions;
- unit-count and square-foot effects;
- the numerator snapshot used for impact review;
- the prospective, restated, or not-comparable treatment;
- same-store and reporting-cohort implications;
- source and approval evidence;
- every downstream consumer and recompute state; and
- exceptions, corrections, and final reconciliation.

Use the blank CSV for live work. The separate fictional example shows proposed, approved, and reconciled states without presenting fictional data as an actual deployment.

## The management rule

Never overwrite capacity simply because the newest number is correct today.

A facility can change while its history remains true. Preserve each denominator for the interval it governed, make corrections visible, and carry the capacity version into every occupancy observation. When the portfolio compares locations, it should be comparing declared measurements—not percentages that happen to share a label.

<!-- BODY END -->

## Sources

1. Public Storage, 2025 Form 10-K, filed with the U.S. Securities and Exchange Commission in 2026. https://www.sec.gov/Archives/edgar/data/1393311/000162828026007696/psa-20251231.htm
2. Extra Space Storage Inc., 2025 Form 10-K, filed with the U.S. Securities and Exchange Commission in 2026. https://www.sec.gov/Archives/edgar/data/1031235/000119312526124051/self-20251231.htm
3. World Wide Web Consortium, *The RDF Data Cube Vocabulary*, W3C Recommendation. https://www.w3.org/TR/vocab-data-cube/
4. World Wide Web Consortium, *Constraints of the PROV Data Model*, W3C Recommendation. https://www.w3.org/TR/prov-constraints/

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

Cedar Quay Storage and every related facility, count, measurement, person, source, system, date, capacity version, report, decision, and outcome are explicitly fictional. The governed image is an AI-generated editorial illustration, not documentary evidence of a real meeting, facility, portfolio, dataset, system, implementation, customer, or result. This article presents a proposed operating method, not accounting, securities, legal, appraisal, measurement, or site-specific compliance advice.
