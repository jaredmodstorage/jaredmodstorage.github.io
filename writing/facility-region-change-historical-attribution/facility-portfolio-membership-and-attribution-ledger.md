# Facility Portfolio Membership and Attribution Ledger

Use this tool to preserve when a facility belonged to a portfolio, region or cluster and to document which membership view a report used. It is an operating-control template, not a substitute for accounting, legal, tax, employment or contractual review.

## Membership section

Create a new row when a membership starts, ends, is corrected or is superseded. Do not overwrite the prior row.

| Field group | Required evidence | Release question |
|---|---|---|
| Identity | Stable facility, portfolio, region and cluster identifiers | Can the relationship be resolved without matching on a display name? |
| Responsibility | Accountable owner role and assignment reason | Who was responsible, and under what approved assignment? |
| Effective period | `valid_from` and `valid_to` with named time zone | Was the relationship true for the period being reported? |
| Record time | `recorded_at` and source record | When did the system learn the assignment? |
| Continuity | Prior and next membership identifiers | Is there an unintended gap or overlap? |
| Correction | Corrected record, reason, approval and supersession time | Is the original assertion preserved and the correction traceable? |
| Consumers | Named downstream uses and affected report IDs | Which routes, queues or reports require review? |

## Report-attribution section

Every released comparison should carry a report record.

| Attribution view | Meaning | Appropriate use |
|---|---|---|
| `as_operated` | Facility-period follows the membership effective during that period | Historical accountability and operating review |
| `current_structure_restatement` | Historical facts are grouped under the current organization | Planning for leaders responsible today, with a visible restatement label |
| `constant_population` | The same governed facility set is held across periods | Like-for-like trend analysis |
| `transition_diagnostic` | Transfer effects and unresolved membership exceptions remain visible | Review before release; not a stable comparison |

## Minimum release test

- One stable membership record resolves each included facility-period.
- Attribution view, organization version and facility-population identifier are present.
- Gaps, overlaps, unknowns and late-entered assignments have explicit dispositions.
- The report identifies its source extracts and generation time.
- Any replacement report links to the prior report and explains the restatement.
- An authorized reviewer records the release decision.

The companion blank CSV contains 43 fields. The separate worked CSV is explicitly fictional and shows a region transfer, a corrected effective date and two different report views.
