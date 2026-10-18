# Every Site Passed Inspection. Which Checklist Did They Use?

## A version-control method for comparing facility inspections without turning different questions into one portfolio score

By Jared Mastroianni

<!-- BODY START -->

The portfolio dashboard says eight of eight facilities completed the monthly inspection. That sounds clean until someone opens the records.

Three sites used the current 42-item checklist. Two used the prior version, which did not include the new gate-release observation. One manager completed a regional PDF with different pass criteria. Another copied last month's spreadsheet and changed the date. The eighth used the right form but skipped a conditional section because the system never asked whether the property had that equipment.

Every record can honestly say “complete.” The records do not mean the same thing.

This is not primarily a training problem or a spreadsheet problem. It is a version-control problem. A checklist is a small operating specification: it defines what must be observed, what evidence is required, which conditions trigger extra questions, what counts as a failure, and who may close the work. Change any of those elements and the portfolio may be asking a different question.

Before leadership compares completion rates, overdue counts, or failure trends, it needs to prove which checklist governed each facility and whether those versions are comparable.

## Treat the checklist as a controlled operating object

A filename such as `Monthly Inspection FINAL.pdf` is not a reliable identity. Neither is a form title displayed in an app. The controlled object needs a stable checklist-family identifier and a specific version identifier.

At minimum, the release record should name:

- checklist family and operating purpose;
- version number or effective date;
- approving owner and approval time;
- version or file hash where practical;
- facility, asset, area, and condition scope;
- required and conditional items;
- pass, critical-fail, evidence, and closure rules;
- effective time and superseded version; and
- the systems, folders, binders, or devices where the checklist is distributed.

This does not require a complicated software platform. It requires one answer to a basic question: if a manager shows you a completed inspection, can you identify the exact rules that were in force when the work was performed?

The W3C's Data on the Web Best Practices recommends a version indicator and version history so users can identify the version they are working with and understand how versions differ. That document addresses web data, not self-storage inspections. The useful operating principle is narrower: a changing dataset or form should not silently replace its own history.[^1]

## Separate form distribution from operational adoption

Publishing a new checklist does not prove that a facility used it.

A portfolio rollout has several distinct states:

1. **Approved:** the owner accepted the content and decision rules.
2. **Released:** the version was placed in the intended distribution channels.
3. **Received:** the responsible facility role could access it.
4. **Acknowledged:** the facility confirmed the version and effective date.
5. **Old version withdrawn:** obsolete copies were removed or visibly marked retired.
6. **Executed:** a real inspection record cites the released version.
7. **Evaluated:** the completed record passed the current completeness and evidence checks.
8. **Reconciled:** the facility's first required use and the portfolio register agree.

Those states prevent a familiar false finish. A central team uploads a revised form and marks the project complete. A manager's bookmark still opens the previous form. A printed binder remains in service. An offline tablet contains a cached copy. A recurring task links to an old template. None of those conditions is fixed by sending another email announcing the release.

For each facility, record the actual distribution surface and test the path the operator uses. Open the link from the task, scan the posted code, inspect the shared folder, or view the offline device. Then preserve evidence of the version shown. “Available at headquarters” is not the same as “available at the point of work.”

## Make applicability explicit before scoring completion

One portfolio checklist can still produce invalid comparisons if its questions do not apply evenly.

A drive-up property, an interior multistory building, and a site with climate-controlled equipment may require different sections. A property without an elevator should not fail an elevator item. A facility with a second entrance should not satisfy a two-gate check by completing one gate row. A temporary construction zone may add observations without permanently changing the base checklist.

The release therefore needs an applicability layer. For every facility, identify:

- the base version in force;
- required modules based on actual assets and areas;
- approved local additions;
- conditions that activate optional questions;
- items that are not applicable and the authority for that determination; and
- the next review trigger when the facility, equipment, or operating policy changes.

Do not let operators decide applicability by silently skipping rows. A skipped item, a not-applicable item, and an unanswered item are different states. The first may be a process failure, the second may be valid, and the third is unknown.

The same rule applies to portfolio denominators. If seven facilities were required to use the checklist and six produced valid records, the completion rate is six of seven. A property held because its applicability record is unresolved should remain visible as held. It should not disappear from the denominator or count as a completed inspection with zero findings.

## Classify the change before rolling it out

Not every edit has the same consequence.

A corrected typo that does not change meaning may be nonmaterial. A new photo requirement changes the evidence contract. A revised threshold changes the decision rule. Adding a new equipment section changes applicability. Removing an item changes the population of observations that can be compared with prior periods.

Classify each release as one of three practical categories:

- **Editorial:** wording or layout changed without changing meaning, scope, evidence, or decision outcome.
- **Operational:** required fields, applicability, evidence, ownership, sequence, or routing changed.
- **Decision-rule:** a pass, fail, escalation, release, or closure threshold changed.

The classification should be approved, not inferred from the size of the redline. One short sentence can materially change a closure rule. A ten-page layout revision can leave operating meaning untouched.

For an operational or decision-rule change, attach a concise difference record: items added, removed, renamed, reordered, or made conditional; evidence requirements changed; thresholds changed; and downstream reports affected. That record tells regional leaders what to teach and tells analysts where historical comparisons need a break or crosswalk.

NIST Special Publication 800-53 uses configuration-change controls that include reviewing proposed changes, approving or disapproving them, documenting decisions, implementing approved changes, retaining records, and monitoring change-controlled activities. It is security and privacy control guidance, not a self-storage checklist standard. Its relevance here is structural: controlled changes need an owner, a decision, an implementation record, and monitoring rather than an undocumented overwrite.[^2]

## Preserve the version used with the completed record

Do not store only the current checklist definition and expect it to explain old inspections.

Each completed record should retain the checklist-family ID, executed version, execution time, facility ID, applicable modules, completion owner, verifier where required, evidence references, and evaluation state. If the platform cannot retain the historical form, export an immutable copy or preserve a controlled snapshot with its hash.

That record makes three questions answerable later:

- What was the operator required to inspect?
- Which decision rules evaluated the answers?
- Can this result be compared with the current or prior period?

Never rewrite a past inspection to display the new form as if that version governed the original work. If a correction is necessary, append the correction, reason, reviewer, and time. Preserve the original state and identify which downstream summaries must be recalculated.

## Compare only the common, governed population

Portfolio reporting should not force unlike versions into one score.

Suppose version 3 has 30 required items and version 4 has 36, including a new six-item access module. A site that passed 30 of 30 under version 3 did not complete 36 of 36. It also did not necessarily fail the six new items. Those observations were not collected.

The defensible choices are to:

- report each version separately;
- compare only items with a documented semantic crosswalk;
- restate the historical series only when source evidence supports the transformation; or
- mark the period noncomparable and begin a new baseline.

A crosswalk should identify the old item, new item, relationship, allowed use, reviewer, and known loss of meaning. “Same label” is not enough. A renamed question may carry a new threshold. Two old questions may have been merged into one. A binary pass/fail may have become a measurement.

When a leadership report says “inspection completion improved,” it should disclose the facility set, period, checklist versions, applicable-item denominator, held records, exclusions, and crosswalk rule. If version coverage is incomplete, the report is incomplete.

## Design an offline and exception path

Facility work does not stop because a form service is unavailable. The fallback still needs control.

Provide one approved offline version with its own identifier, effective period, storage location, and return procedure. Require the operator to record the facility, start time, reason for offline use, and version. When service returns, reconcile the offline record into the system without converting the upload time into the inspection time.

If a facility must temporarily use a superseded version, record the approving owner, reason, missing requirements, compensating steps, expiration, and corrective plan. A temporary exception should not become the unobserved portfolio standard.

## A fictional seven-facility rollout

The following scenario is entirely fictional. Northstar Lock & Store, its seven facilities, people, forms, systems, dates, records, and results were invented only to demonstrate the method.

Northstar releases Monthly Property Review version 4.2, effective October 15. The revision adds a conditional roof-drain module, changes the gate-photo requirement, and makes an unresolved exit-route obstruction a critical failure. The release owner classifies it as both operational and decision-rule change.

The portfolio register shows five facilities acknowledged version 4.2. A sixth still opens version 4.1 from a recurring task. The seventh has the right form, but its applicability record omits the roof-drain module even though the fictional asset list says the property has that system.

Northstar does not report seven completed rollouts. The sixth facility's task link is corrected, the old copy is withdrawn, and the first 4.2 execution is verified. The seventh facility's applicability record is repaired before the inspection; no answer is invented for work that has not occurred.

At month-end, four facilities have valid 4.2 records, two have valid 4.1 records completed before the effective date, and one has an approved offline 4.2 record awaiting reconciliation. The report shows the versions separately. A crosswalk permits comparison of 27 unchanged items, while the gate-photo and critical-failure results begin a new series.

Nothing in the scenario claims a real inspection, customer, facility, deployment, safety result, compliance outcome, cost saving, or performance improvement.

## Completion is a versioned claim

The companion Facility Checklist Version and Coverage Register joins the release record to each facility's applicability, distribution, execution, exception, and reconciliation evidence.

Start with one recurring portfolio checklist. Identify every version still reachable, name the current version, map facility applicability, withdraw obsolete copies, and verify the first required use at each site. Then repair reporting so completion is counted only when the facility used an authorized version and satisfied the applicable evidence and decision rules.

A checklist is useful because it makes work repeatable. It becomes dangerous when the portfolio assumes that the same title guarantees the same work.

The operating standard is simple: before comparing inspections, prove the question set, the version, the applicable population, and the decision rule that produced each result.

<!-- BODY END -->

## Sources

[^1]: World Wide Web Consortium, [Data on the Web Best Practices](https://www.w3.org/TR/dwbp/), especially Best Practices 7 and 8 on version indicators and version history; accessed October 14, 2026.
[^2]: National Institute of Standards and Technology, [NIST SP 800-53 Rev. 5, Update 1](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), especially CM-3 Configuration Change Control; accessed October 14, 2026.

Additional implementation context: Occupational Safety and Health Administration, [Program Evaluation and Improvement](https://www.osha.gov/safety-management/program-evaluation), current Recommended Practices guidance; accessed October 14, 2026. OSHA recommends verifying that programs are implemented and operating as intended and reviewing the data used to evaluate them. It does not prescribe this checklist-version method or establish a self-storage inspection requirement.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

This article was prepared with AI-assisted research, drafting, and editorial QA under Jared Mastroianni's byline. It presents a product-neutral operating method and no customer, deployment, provider, performance, compliance, revenue, occupancy, award, or recognition result. The scenario and dataset are fictional teaching material. Operators must apply their current policies, contracts, system instructions, and applicable law.
