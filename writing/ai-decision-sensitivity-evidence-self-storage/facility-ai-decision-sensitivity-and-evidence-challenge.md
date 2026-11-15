# Facility AI Decision-Sensitivity and Evidence Challenge

Use this tool to test whether a plausible evidence change would move an AI-assisted recommendation across a real operating boundary. It is an architecture worksheet, not a live action engine.

## Operating rules

1. Run the challenge in an isolated evaluation context with no production credentials or write tools.
2. Preserve the baseline input snapshot, model/configuration versions and output before changing anything.
3. Use only bounded, plausible alternate values. Mark every alternate value as synthetic.
4. Treat a boundary-crossing field as decision-critical for that recommendation.
5. Verify decision-critical fields from their named governing sources before release.
6. Never copy a synthetic challenge value into facility history.

## 1. Freeze the baseline

| Field | Required entry |
|---|---|
| Recommendation ID | Durable identifier for this baseline recommendation |
| Use case and purpose | Exact workflow and approved reason for using AI |
| Facility and object identity | Stable IDs for the facility and affected object |
| Source snapshot ID and digest | Reproducible evidence set, cutoff and cryptographic digest |
| System versions | Model, prompt, retrieval, feature, policy and boundary-evaluator versions |
| Baseline output | Recommendation text or structured class |
| Baseline action class | Display, propose, queue, prepare or execute |
| Authority ceiling | Highest state the workflow may reach without additional approval |

**Hold when:** the snapshot, identity, purpose, version or authority ceiling is missing.

## 2. Define the material boundaries

Record the deterministic rules that make a change material.

| Boundary | Examples of material movement |
|---|---|
| Timing | Routine review becomes immediate human review |
| Ownership | Facility review becomes regional, security or qualified-service review |
| Evidence | Ordinary source packet requires a current inspection or governing-source readback |
| Action | Display becomes queue placement; queue placement becomes prepared action |
| Communication | Internal note becomes a proposed customer or vendor message |

**Hold when:** the model itself decides whether its output crossed a consequential boundary.

## 3. Build the challenge set

| Challenge family | Bounded alternatives |
|---|---|
| Identity | Current stable ID, unresolved ID, governing linked record |
| Time | Current cutoff, prior approved calendar, expired evidence, unknown local time |
| State | Approved states plus `unknown` and `not evaluated` |
| Provenance | Observed, staff-entered, vendor-returned, calculated, summarized, inferred |
| Missingness | Absent, unavailable, unreadable, not applicable, explicitly negative |

For each field, document why the alternate value is plausible and which source or rule bounded it. Do not ask the model to invent an alternate history.

## 4. Compare outcomes

For every challenge run, capture:

- challenged field and original value;
- synthetic alternate value;
- challenge-set version;
- challenged output and digest;
- challenged action class;
- boundary-crossing result;
- explanation produced by the system, if any; and
- whether the explanation is supported by the recorded process.

The comparison should be machine-readable. A prose note alone is not sufficient evidence.

## 5. Verify decision-critical evidence

When a challenge crosses a boundary:

1. Name the governing source for the challenged field.
2. Retrieve the current value through an authorized read path.
3. Record source time, retrieval time and freshness rule.
4. Classify the outcome as verified, contradicted, unavailable or unresolved.
5. Create a new baseline if the governing source changes the evidence.
6. Preserve the original baseline and the synthetic challenge as separate test artifacts.

**Hold when:** the critical field is inferred, stale, unavailable, contradicted or outside the reviewer’s authority.

## 6. Release decision

| Release state | Required condition |
|---|---|
| Release for display | Evidence packet reproducible; no hidden action |
| Release for human review | Critical fields verified or visibly unresolved; named reviewer |
| Hold | Boundary crossing unresolved, recommendation expired or authority unclear |
| Retest | Model, prompt, retrieval, policy, source schema or boundary rule changed |
| Retire | Use case no longer approved or safe operating conditions cannot be maintained |

If a later action is authorized, record its separate action ID, approver, execution receipt and operating readback. A sensitivity test never supplies action authority.

## Review questions

- Could a plausible change to one field alter the owner, timing, evidence or permitted action?
- Did the challenge use a real bounded alternative rather than random text?
- Can the reviewer see both outputs and the exact evidence difference?
- Is every boundary-crossing field verified from its governing source?
- Are synthetic values blocked from production records and tools?
- Can the team reconstruct why the final recommendation was released, held, retested or retired?

This template requires adaptation and review by the organization’s operating, technical, security, privacy and legal owners as applicable.
