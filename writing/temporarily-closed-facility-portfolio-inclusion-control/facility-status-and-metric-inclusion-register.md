# Facility Status and Metric Inclusion Register

Use one record for each metric or automation affected by a facility-state event. The event may be shared across records; the inclusion decision may not. This tool is a proposed operating method, not a universal accounting rule or a substitute for legal, contractual, safety or financial review.

## 1. Identify the facility and event

- Use a stable facility ID rather than a display name alone.
- Record the exact affected physical or commercial scope.
- Separate prior state, new state, effective time, next review time and actual end time.
- Name the authority that established the condition and link its evidence.
- Use `unknown` when a fact has not been established. Do not translate unknown into closed, inactive or excluded.

## 2. Bind the decision to one purpose

- Give the metric or automation its own ID and plain-language purpose.
- State the unit of analysis: facility, unit, occupied unit, agreement, lead, task, dollar or another governed unit.
- Record the inclusion-rule version, eligible states and treatment of partial operation.
- Choose `included`, `excluded`, `partial` or `held`.
- Explain numerator, denominator and comparison-cohort treatment separately.
- List downstream dashboards, exports, automations or decisions that consume the result.

## 3. Approve, read back and reconcile

- Record the approver and exact decision time.
- Read back the actual population after implementation.
- Reconcile expected and observed treatment.
- Carry every variance with an owner and due time.
- Close only when the metric population and downstream consumers agree with the approved rule, or the remaining variance is explicitly bounded and owned.

## Minimum review table

| Question | Hold condition |
| --- | --- |
| Is the facility identity stable? | No governed facility ID or conflicting identity |
| Is the operating condition established? | Missing scope, authority, evidence or effective time |
| Is the metric purpose explicit? | A generic dashboard name substitutes for a business question |
| Is the eligibility rule versioned? | Treatment depends on an unwritten convention |
| Is partial operation addressed? | The rule supports only active/inactive |
| Are numerator and denominator both declared? | Only the final percentage or total is reviewed |
| Is cohort treatment visible? | Historical comparison changes without disclosure |
| Are downstream consumers known? | The status field may change unknown reports or automations |
| Was the result read back? | A save banner or accepted request is the only evidence |
| Are variances owned? | Differences are left in notes without owner or due time |

## Files

- `facility-status-and-metric-inclusion-register-template.csv` — blank implementation register.
- `facility-status-and-metric-inclusion-register-fictional-example.csv` — four entirely fictional teaching records for Stonehaven Loop Storage. No company, facility, customer, deployment, incident, result or provider behavior is represented.

## State model

`event_recorded` → `metric_rule_identified` → `decision_approved` → `implemented` → `read_back` → `reconciled`

Use `held` at any stage when identity, condition, rule, authority or evidence is missing. Reopening creates a new effective-dated event; it does not erase the prior interval.
