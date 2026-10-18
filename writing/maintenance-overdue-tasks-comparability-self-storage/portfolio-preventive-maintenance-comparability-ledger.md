# Portfolio Preventive-Maintenance Comparability Ledger

Use this tool to decide whether facility maintenance results are comparable before ranking sites, escalating managers, or allocating capital. It does not prescribe maintenance intervals or replace manufacturer, qualified-provider, code, insurer, engineering, or site-specific requirements.

## Five-pass review

### 1. Establish the asset denominator

- Reconcile each row to one installed asset instance and location.
- Preserve retired and replacement assets as separate records.
- Confirm operating state and denominator eligibility.
- Hold ambiguous, duplicate, or unverified asset identities.

### 2. Validate the governing basis

- Record the approved maintenance source and exact version or effective date.
- Identify whether the strategy is reactive, calendar-based, usage-based, condition-based, event-based, or combined.
- Never manufacture a calendar interval merely because the work-order system requires a date.

### 3. Reproduce the due state

- Retain the trigger, threshold, unit, current reading or condition evidence, last qualifying completion, and calculation timestamp.
- Keep the source-system value and the normalized reporting value traceable.
- Use `not_evaluable` when the required evidence is absent.

### 4. Resolve completion evidence and exceptions

- Distinguish ticket closure from qualifying maintenance completion.
- Record evidence as `verified`, `pending_review`, `insufficient`, or `unavailable`.
- Require exception owner, scope, restriction, start, expiration, and next action.

### 5. Release the comparison

- State the eligible denominator and all held or excluded rows.
- Declare the intended management use and material limitations.
- Assign a reconciliation owner and next-action date.
- Release only when another responsible person can reproduce each due-state result.

## Decision table

| Condition | Due state | Denominator | Required response |
|---|---|---|---|
| Governing basis, trigger, last qualifying completion, and current threshold are verified | Calculated from the approved rule | Eligible | Include with calculation timestamp |
| Current usage or condition reading is missing | Not evaluable | Held | Obtain or reconcile the required reading |
| Ticket closed but required completion evidence is insufficient | Not evaluable | Held | Verify the qualifying completion; do not infer current or overdue |
| Asset is under an approved, unexpired out-of-service exception | Separately reported | Excluded only under the recorded rule | Track restriction, expiration, and next action |
| Asset identity or installed instance is ambiguous | Not evaluable | Held | Reconcile asset identity before comparison |
| Exception has expired | Recalculate | Held until reviewed | Escalate to the designated authority |

## Release note template

> As of **[calculation timestamp]**, **[number]** of **[number]** eligible tasks are overdue under the approved bases and versions recorded in this ledger. **[number]** records are held because **[reasons]**; **[number]** are excluded under **[approved rules]**. This comparison is released for **[intended use]** by **[owner]** and must not be used for **[excluded uses]**. Next reconciliation: **[date]**.

## Companion files

- `portfolio-preventive-maintenance-template.csv` — blank 38-field implementation register.
- `portfolio-preventive-maintenance-fictional-example.csv` — four explicitly fictional teaching records.

