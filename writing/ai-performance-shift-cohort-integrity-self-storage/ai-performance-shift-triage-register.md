# AI Performance Shift Triage and Cohort Integrity Register

Use one register for one monitored metric, comparison window and bounded decision scope. A moved metric opens an investigation; it does not establish model drift.

## 1. Name the observation

| Field | Required entry |
|---|---|
| Register ID | Stable identifier |
| Metric and permitted use | Exact measure and what it may influence |
| Baseline window | Start, end and reporting time zone |
| Current window | Start, end and reporting time zone |
| Baseline numerator / denominator | Counts, not only a percentage |
| Current numerator / denominator | Counts, not only a percentage |
| Uncertainty method | Interval, resampling method or `not_established` |
| Observed shift | Absolute and relative change, if appropriate |
| Initial state | `observed_shift` or `comparison_not_established` |

## 2. Freeze the comparison contract

| Identity | Baseline | Current | Same? | Evidence reference |
|---|---|---|---|---|
| Decision build | Model, prompt, retrieval, rules, threshold and post-processing versions |  | yes / no / unknown |  |
| Task contract | Question, output meaning and permitted consequence |  | yes / no / unknown |  |
| Facility cohort | Included facilities and membership rule |  | yes / no / unknown |  |
| Record cohort | Eligible record types and exclusions |  | yes / no / unknown |  |
| Source coverage | Required sources, received sources, freshness and missingness |  | yes / no / unknown |  |
| Outcome contract | Label, observation window, exclusions and correction rule |  | yes / no / unknown |  |
| Label maturity | Earliest valid evaluation date and unresolved count |  | yes / no / unknown |  |
| Decision environment | Policy, reviewer population, authority and known operating conditions |  | yes / no / unknown |  |

If a release-critical identity is `unknown`, do not diagnose model drift. Keep the state `comparison_not_established` and assign the missing evidence.

## 3. Produce three views

| View | Numerator | Denominator | Result | Limitation |
|---|---:|---:|---:|---|
| Reported portfolio |  |  |  | Includes all period-eligible records |
| Matched cohort |  |  |  | Same facilities, records, definitions, sources and maturity rule |
| Composition |  |  |  | Entries, exits or eligibility changes only |

## 4. Classify supported causes

Use `supported`, `candidate`, `not supported`, `not evaluated` or `unknown`.

| Cause class | State | Evidence needed before conclusion |
|---|---|---|
| Decision-build change |  | Versioned build and controlled replay |
| Portfolio or record-mix change |  | Membership diff and matched-cohort result |
| Observation or source-coverage change |  | Source receipt, freshness and missingness evidence |
| Label definition or maturity change |  | Versioned outcome contract and matured-label counts |
| Policy or reviewer change |  | Policy version, reviewer instructions and disposition comparison |
| Real operating-environment change |  | Qualified facility evidence independent of model output |

## 5. Bound replay and action

| Field | Required entry |
|---|---|
| Replay packet IDs | Immutable copies of the exact historical evidence packets |
| Builds compared | Exact baseline and current identifiers |
| Isolation boundary | Confirmation that replay cannot call live tools or customer channels |
| Replay result | Output, abstention, threshold and tool-use comparison |
| Unsupported conclusions | Causes the evidence does not establish |
| Interim operating state | `advisory`, `shadow`, `human_review_required`, `held` or approved bounded state |
| Stop condition | Condition that suspends use or prevents broader authority |
| Decision owner | Accountable human role |
| Next evidence and due time | Concrete owner, artifact and deadline |
| Closure state | `cohort_shift_supported`, `source_gap_open`, `labels_not_mature`, `model_change_candidate`, `operating_change_candidate`, `resolved` or another defined state |

## Close rule

Close only when the comparison contract is preserved, each supported cause is tied to evidence, unsupported causes remain explicitly unproven, the interim operating state is reconciled, and the decision owner signs the final disposition. Reopen after a material correction to the build, cohort, sources, labels, policy, review process or facility evidence.

