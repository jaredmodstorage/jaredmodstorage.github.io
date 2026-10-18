# Portfolio Capacity Denominator Change Ledger

Use this ledger when unit count, rentable square footage, eligibility, physical configuration, or a reporting definition changes at a self-storage facility. It preserves the denominator's identity, effective interval, source, impact, approval, and downstream reconciliation. It does not determine legal capacity, rentable status, construction completion, accounting treatment, appraisal measurement, or public-disclosure requirements.

## Gate 1 — Define the measurement

- [ ] Name the metric and formula.
- [ ] Identify unit-count, rentable-square-foot, or other approved capacity basis.
- [ ] Record cohort, period, observation timing, exclusion rules, rounding rule, and owner.
- [ ] Assign a stable capacity-definition ID and version.

## Gate 2 — Establish the physical event

- [ ] Record exact facility, buildings/floors, affected units, reason for change, and source event.
- [ ] Separate physical completion, operating acceptance, system activation, and metric-effectiveness times.
- [ ] Preserve source document, source system, extraction hash, and measurement method.
- [ ] Distinguish a real physical change from correction of an earlier record.

## Gate 3 — Preserve both versions

- [ ] Retain the prior record and effective-through time.
- [ ] Create the proposed record with effective-from time.
- [ ] Record unit and rentable-square-foot deltas independently.
- [ ] Link corrections to the record they replace; do not silently overwrite.

## Gate 4 — Preview the impact

- [ ] Freeze occupied units and occupied square feet at one comparison instant.
- [ ] Calculate occupancy under prior and proposed capacity versions.
- [ ] Label the difference as physical change, correction, definition change, or unresolved.
- [ ] Identify affected reports, cohorts, incentives, forecasts, and public facts.

## Gate 5 — Declare historical treatment

- [ ] Choose prospective, controlled restatement, or not comparable.
- [ ] Record reason, affected interval, approver, prior result, replacement result, and revision marker.
- [ ] Do not change historical observations merely to improve a trend.
- [ ] Hold comparison when cohort or effective-time rules are unresolved.

## Gate 6 — Reconcile consumers

- [ ] List each management, BI, budgeting, revenue, scorecard, reporting, warehouse, export, and public consumer.
- [ ] Record prior version, target version, recompute job, completion receipt, and parity check.
- [ ] Compare coverage, totals, periods, and an authorized sample of source records.
- [ ] Keep internal operating state separate from public disclosure state.

## Gate 7 — Release and monitor

- [ ] Local verifier, portfolio reviewer, and authorized approver are recorded.
- [ ] All required consumers reconcile or have named exceptions.
- [ ] Release time, next review, correction route, and exception owner are recorded.
- [ ] Original and revised observations remain traceable.

## State rule

`Observed change -> Proposed capacity version -> Impact preview -> Historical treatment approved -> Consumer recompute -> Reconciliation -> Released`

A new number in the property system is not a portfolio release.

Supporting files:

- `portfolio-capacity-denominator-change-ledger-template.csv`
- `portfolio-capacity-denominator-change-ledger-fictional-example.csv`
