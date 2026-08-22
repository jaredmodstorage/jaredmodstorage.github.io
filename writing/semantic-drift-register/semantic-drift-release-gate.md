# Semantic Drift Release Gate

**Authored by Jared Mastroianni**

Use this gate when a facility field, metric, state, identifier, event attribute, model score, or derived value may have changed meaning. It is a proposed operating tool, not a deployed control, certification, legal instruction, financial control opinion, or industry standard.

The fastest safe starting point is one term, one predecessor contract, one candidate contract, and one named decision.

## 1. Open the change record

Assign a stable record ID. Do not edit the predecessor contract in place.

- [ ] Stable term ID is named separately from its display label.
- [ ] Candidate contract has a new immutable version and effective interval.
- [ ] Predecessor contract ID, version, and exact digest are preserved.
- [ ] Candidate contract digest and transformation identity are recorded.
- [ ] Author, producer, source owner, approval owner, and migration owner are distinct where their authorities differ.
- [ ] Evidence boundary says what the field does not prove.

Output: one row in [semantic-drift-register-template.csv](semantic-drift-register-template.csv) and one candidate contract conforming structurally to [semantic-contract.schema.json](semantic-contract.schema.json).

## 2. Diff the meaning

Compare every dimension. Mark `changed`, `unchanged`, or `unknown` and attach evidence.

| Dimension | Minimum question |
| --- | --- |
| Identity | Does the value describe the same stable facility, resource, subject, and namespace? |
| Population | Are numerator, denominator, inclusions, exclusions, and eligibility identical? |
| Value | Are datatype, unit, scale, direction, precision, tolerance, and allowed values identical? |
| Time | Are event, observation, effective, posting, cutoff, timezone, and lateness rules identical? |
| Authority | Does the same qualified source field and owner govern the claim? |
| Null | Do blank, zero, false, unknown, unavailable, not applicable, withheld, error, and prohibited remain distinct? |
| State | Are states, transitions, evidence gates, and terminal meanings identical? |
| Transformation | Are calculation, input versions, joins, rounding, calibration, and thresholds identical? |
| Decision use | Is the field still limited to the same display, advice, routing, approval, or action use? |
| Boundary | Does the field continue to exclude the same conclusions? |

Any unresolved dimension makes compatibility `unknown`. A consequential change in any dimension is presumptively `breaking` until named consumers demonstrate otherwise.

## 3. Inventory consumers

Search beyond registered services.

- [ ] APIs and event subscribers
- [ ] dashboards, reports, exports, and spreadsheets
- [ ] alerts, rules, automations, and action gates
- [ ] metrics, historical series, and executive summaries
- [ ] model features, evaluation sets, thresholds, and queues
- [ ] retrieval corpora, prompts, generated summaries, and citations
- [ ] public content, customer-message drafts, and operator procedures
- [ ] caches, replicas, warehouses, archives, and backfills

For every consumer, record the current contract version, intended use, decision consequence, owner, compatibility result, migration state, readback target, and rollback behavior.

An undocumented consumer is not compatible by default. It is an unresolved dependency.

## 4. Classify the change

- **Additive:** existing meaning remains intact and every affected consumer safely handles the addition.
- **Non-breaking:** representation changes, meaning does not, and named consumer tests pass.
- **Breaking:** a consumer assumption can change.
- **Unknown:** evidence, ownership, or dependency coverage is incomplete.

Apply the strictest affected-consumer classification. Do not let a patch version, successful parse, unchanged datatype, or producer claim override the semantic diff.

## 5. Execute bounded dual-read

For breaking and unknown changes:

- [ ] Run predecessor and candidate against the same named fictional or approved private fixtures.
- [ ] Preserve both contract IDs, transformation IDs, event times, observation times, and evaluation times.
- [ ] Record every disagreement without overwriting either value.
- [ ] Assign each disagreement a reason such as intended population change, time-boundary difference, late source, identity conflict, transformation defect, or unresolved.
- [ ] Route each mismatch to the qualified owner.
- [ ] Keep consequential downstream action disabled until the required disposition is complete.

Dual-read is evidence collection, not acceptance.

## 6. Test history, thresholds, and exceptional states

- [ ] Historical replay preserves original series and labels any restatement.
- [ ] Null, zero, false, unknown, unavailable, not applicable, withheld, error, and prohibited fixtures are distinct.
- [ ] Timezone, daylight-saving, late-event, future-effective, and out-of-order cases pass where relevant.
- [ ] Identity aliases, collisions, retired IDs, and cross-facility conflicts fail visibly.
- [ ] Enum additions and removals preserve unknown values rather than coercing them to a terminal state.
- [ ] Thresholds are reapproved for the candidate meaning; old thresholds are not inherited silently.
- [ ] Retrieval uses one approved contract version or surfaces conflicts explicitly.
- [ ] Generated or derived text cannot recirculate as source authority.
- [ ] The appropriate cases in [semantic-drift-readiness-suite.csv](semantic-drift-readiness-suite.csv) pass.

Passing structural validation establishes structural conformance only. It does not establish truth, authority, compatibility, completeness, operational fitness, model validity, safety, or measured performance.

## 7. Approve a complete migration packet

Approval must bind to exact versions and evidence:

- [ ] predecessor and candidate contract IDs and digests;
- [ ] semantic diff and compatibility disposition per consumer;
- [ ] dual-read interval and mismatch ledger;
- [ ] historical-series and backfill decision;
- [ ] model, threshold, or queue decision when AI paths are involved;
- [ ] affected consumer inventory and migration sequence;
- [ ] effective interval, communications, and training need;
- [ ] approver identity, authority, timestamp, and expiry;
- [ ] executable rollback version and trigger.

If the packet changes materially after approval, mint a new candidate version or approval. Do not attach the old approval to new meaning.

## 8. Release and read back

- [ ] Release contract, transformation, consumer configuration, labels, and documentation as one governed change set.
- [ ] Record source commit, deployment identity, release time, and actual candidate hashes separately.
- [ ] Read back the named governing outputs, not only the deployment command or provider response.
- [ ] Verify which consumer version is active and whether exceptions remain.
- [ ] Keep predecessor artifacts and inputs runnable until the migration exit criteria are met.
- [ ] If a required check fails, stop downstream consequence, restore the predecessor contract, and verify its governing output.

## 9. Close without collapsing states

Record each state separately:

- candidate prepared;
- structurally validated;
- semantically reviewed;
- migration approved;
- deployed;
- consumer readback verified;
- operating reconciliation complete;
- published;
- crawled;
- indexed;
- ranked;
- covered;
- recognized.

No earlier state proves a later one.

## Operator exercise

Choose a real internal field only if you have authority to review its private sources. Otherwise use `SDR-FIC-001` from the fictional register.

1. Write the field's meaning without using its label.
2. Name its population, unit, clock, authority, null meaning, transformation, and decision use.
3. Find the predecessor contract or reconstruct the earliest evidence-bounded definition.
4. Mark every changed or unknown dimension.
5. Name one downstream decision that would change if the old meaning were assumed.
6. Design a two-version fixture and expected mismatch.
7. State the minimum evidence needed for approval and the exact rollback.

If the exercise cannot identify the owner, predecessor, consumer, or rollback, classify the candidate `unknown` and keep consequential use held.
