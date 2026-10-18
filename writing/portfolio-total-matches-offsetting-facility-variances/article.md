# The Portfolio Total Matches. Which Facilities Are Canceling Each Other Out?

**Deck:** A zero portfolio variance can conceal missing records at one facility and duplicates at another. Reconcile the signed difference, the gross difference and every facility row before calling the result complete.

**By Jared Mastroianni**

<!-- BODY START -->

A portfolio report shows 1,240 open access exceptions. The source extract also shows 1,240. The total ties, the dashboard is green and the reconciliation closes.

But the facilities do not agree. One site has six extra cases in the dashboard, another is missing four and a third is missing two. At the portfolio level, positive six plus negative six equals zero. Operationally, the error is still twelve cases wide.

This is the offset problem: a correct total can be assembled from incorrect facility rows. If the reconciliation tests only the sum, errors in allocation, duplication, omission or facility identity can cancel each other out. The portfolio looks clean while managers work from the wrong local picture.

Multi-location operators need two answers, not one:

1. Does the portfolio total agree?
2. Does every facility contribute the right amount to that total?

The first answer is a net check. The second requires a gross check and a row-level disposition.

## A net-zero difference is not zero error

For each facility, define a signed variance:

**facility variance = observed value − expected value**

A positive result means the observed portfolio layer contains more than the comparison source for that facility. A negative result means it contains less. “Expected” does not mean a target or budget unless the metric is explicitly designed that way. In a record-reconciliation use case, it should mean the source value against which the target is being tested.

Then calculate two portfolio measures:

**portfolio net variance = sum of all signed facility variances**

**portfolio gross variance = sum of the absolute value of every facility variance**

If the facility variances are +6, −4 and −2, the net variance is zero. The gross variance is 12. The first number says the overstatements and understatements balance mathematically. The second says twelve units of facility-level disagreement still require explanation.

That distinction changes the control. A net variance of zero may be necessary for a complete reconciliation, but it is not sufficient. Completion also requires a gross variance of zero—or a documented, approved disposition for every nonzero facility row.

## Start with a metric contract

Offset detection works only when the compared values mean the same thing. Before extracting data, define a metric contract:

- metric name and version;
- unit of measure;
- reporting period and time-zone rule;
- event or record states included and excluded;
- facility population and effective dates;
- source and target systems;
- facility identifier used in each system;
- transformation and mapping versions; and
- treatment of late, reversed, deleted or transferred records.

Without that contract, a variance can be manufactured by definition. One system may count cases created during the period; another may count cases still open at period end. One may assign a transferred record to the originating facility; another may assign it to the current owner. A total comparison between those populations is not a reconciliation, even if the numbers happen to match.

GAO’s data-reliability guide frames reliability in relation to accuracy, completeness and applicability for the intended purpose.[^1] That guide is written for government audit work, not self-storage reporting. Its useful operating lesson is narrower: data should be assessed against the specific decision being made. A total can be numerically accurate and still be inapplicable to a facility-level staffing or service decision because its attribution is wrong.

## Freeze the comparison before investigating

When a portfolio discrepancy appears, do not repeatedly refresh both sides until they happen to agree. Capture the two extracts, their timestamps, filters, metric version, mapping version and facility population. Assign one reconciliation ID to the comparison.

This creates a stable question. Otherwise, a facility can move from negative two to zero simply because new records arrived during the investigation, while the original discrepancy disappears from view. The team may believe it corrected a problem that was never actually explained.

The frozen comparison should identify the evidence used, not copy restricted customer data into the register. Use controlled references to extracts, queries, tickets or logs. Preserve retention, privacy and access rules that already apply to those records.

The W3C PROV family describes provenance through entities, activities and people involved in producing data, supporting assessments of quality, reliability and trustworthiness.[^2] PROV is a general web standard, not a required self-storage data model. The practical translation is straightforward: preserve which data was used, what transformation produced the result and who or what performed the work.

## Reconcile at the lowest useful operating grain

Facility is usually the minimum useful grain for a multi-location operating report, but it may not be the final one. If a facility row is nonzero, the investigation may need to continue to building, unit, case, work order, transaction or event.

The rule is simple: reconcile at the level where an error could change an operating decision.

If site-level staffing is based on open customer-access exceptions, facility attribution matters. If a maintenance vendor is dispatched by asset, the asset assignment matters. If a regional manager is accountable for a period, effective-dated regional membership matters. Portfolio agreement cannot substitute for the identity needed to act.

Do not assume that one positive and one negative row describe a transfer between those sites. They might, but the pattern also fits a duplicate at one facility plus an unrelated omission at another. Link rows only when a shared record identifier, transfer event, mapping rule or other evidence supports the relationship.

## Use reason codes that describe evidence, not guesses

Every nonzero facility row should receive a reason state. Useful categories include:

- **timing difference:** the same valid record crossed the systems in different windows;
- **duplicate:** the target contains more than one representation of one source event;
- **omission:** an eligible source record did not reach the target;
- **facility mapping:** the record exists but is attributed to the wrong facility identity;
- **population mismatch:** facility membership or effective dates differ;
- **definition mismatch:** inclusion, exclusion or state logic differs;
- **authorized adjustment:** a documented rule intentionally changes the value;
- **source correction pending:** the expected side is known to be wrong but has not been corrected through its owner;
- **unresolved:** evidence is not yet sufficient.

“Offset by another site” is not a reason code. It describes what happened to the portfolio arithmetic, not why either facility row is wrong.

The 2025 GAO Green Book emphasizes reliable reporting, relevant quality information, control activities at appropriate organizational levels and documented responses to risk.[^3] Its mandatory scope is federal agencies, so it should not be presented as a private self-storage requirement. Adapted as an operating principle, it supports a layered control: portfolio totals for oversight, facility rows for accountability and evidence-backed correction at the source of the problem.

## Separate detection, correction and historical treatment

Finding a variance does not authorize an analyst to overwrite it. The register should carry distinct states:

- **detected:** the frozen comparison produced a nonzero facility row;
- **explained:** evidence supports a reason code;
- **correction authorized:** the owner of the affected source, mapping or transformation approved a change;
- **corrected:** the approved change was applied;
- **validated:** a new controlled comparison confirms the intended facility result; and
- **historical treatment decided:** prior reports were restated, annotated, left as originally issued or assigned for further review.

These states matter because the wrong fix can make today’s total look better while corrupting history. If the issue is a facility mapping effective on October 1, rewriting September without authority may move prior activity into an entity that did not own it at the time. If the source record itself is wrong, patching only the dashboard can allow the error to return at the next refresh.

The Federal Data Strategy calls for stewardship, governance, transparent documentation and protection of data quality and integrity.[^4] It applies to federal data, not private self-storage portfolios. Its bounded lesson here is that corrections need ownership and documentation; a silent spreadsheet override is not a durable data-control process.

## Track the offset ratio without turning it into a verdict

One useful diagnostic is the offset ratio:

**offset ratio = 1 − (absolute net variance ÷ gross variance)**

Use it only when gross variance is greater than zero. In the +6, −4, −2 example, the net variance is zero and the gross variance is 12, so the offset ratio is 100%. Every unit of gross disagreement is hidden by offsetting direction at the portfolio level.

If the net variance is two and the gross variance is ten, the offset ratio is 80%. Most of the underlying disagreement is masked, but two units remain visible in the total.

This ratio is a triage signal, not a quality score. A high ratio does not prove fraud, manipulation or a particular root cause. A low ratio does not make the data reliable. It simply tells reviewers how much facility-level disagreement disappears when signed variances are netted.

## A fictional five-facility example

In the explicitly fictional Harborline Storage portfolio, a source extract and dashboard each show 1,240 open access-exception cases for the same period and metric version. The portfolio net variance is zero.

Facility review shows Harborline North at +6, East at −4, River at −2, and the other two sites at zero. The gross variance is 12 and the offset ratio is 100%.

The review does not conclude that North’s extra six are the same records missing from East and River. Evidence shows four duplicated dashboard records at North, two records mapped from River to North after an outdated facility crosswalk ran, and four omitted East records caused by a failed batch. The team corrects each governed source or transformation through its owner, reruns the same metric contract, and validates all five facility rows at zero. Historical treatment is recorded separately.

The portfolio, facilities, systems, records, values, causes and outcome in this example are invented. They do not describe modSTORAGE, a customer, a deployment, an integration or an observed result.

## The operating release rule

The accompanying **Portfolio Offset Detection and Gross Variance Register** keeps the metric contract, frozen extracts, facility rows, signed and absolute variances, offset calculation, evidence, reason, authority, correction and validation in one governed structure.

A portfolio result can be released as reconciled only when:

- the compared metric contract is the same on both sides;
- the facility population and effective dates are confirmed;
- the portfolio net variance is zero or has an approved disposition;
- every nonzero facility row has evidence, an owner and a due time;
- gross variance is zero or every remaining amount is an approved bounded exception;
- corrections occur through authorized source, mapping or transformation owners;
- validation uses a new controlled comparison; and
- historical treatment is explicit.

The point is not to make every dashboard perfect before anyone can use it. The point is to make its limits visible. A portfolio total may be accurate for one purpose and unsafe for another. Managers should know whether they are looking at reconciled facility data, a netted portfolio estimate or an unresolved comparison.

When the total matches, the next question should not be “Can we close the report?” It should be: **What is the gross variance, and which facility rows are making each other disappear?**

<!-- BODY END -->

## Sources

[^1]: U.S. Government Accountability Office, *Assessing Data Reliability (GAO-20-283G)*, December 16, 2019, https://www.gao.gov/products/gao-20-283g
[^2]: World Wide Web Consortium, *PROV-Overview*, April 30, 2013, https://www.w3.org/TR/prov-overview/
[^3]: U.S. Government Accountability Office, *Standards for Internal Control in the Federal Government (GAO-25-107721)*, May 15, 2025, https://www.gao.gov/products/gao-25-107721
[^4]: Federal Data Strategy, *2020 Action Plan*, 2020, https://strategy.data.gov/assets/docs/2020-federal-data-strategy-action-plan.pdf

## Disclosure

This article was prepared with AI assistance under Jared Mastroianni’s editorial direction and subjected to source, originality, claim-boundary and publication-state review. The Harborline Storage portfolio and dataset are explicitly fictional.
