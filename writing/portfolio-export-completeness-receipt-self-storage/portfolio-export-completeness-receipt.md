# Portfolio Export Completeness Receipt

Use this receipt before an extract supports a portfolio comparison, exception queue, executive report, automated workflow, or AI-assisted decision.

## 1. Decision scope

- Decision or analysis purpose:
- Permitted downstream use:
- Data owner:
- Expected roster ID and version:
- Roster effective timestamp and timezone:
- Expected facility count:
- Expected facility IDs:
- Inclusion rules:
- Exclusion rules:

## 2. Extraction identity

- Source system:
- Report, query, view, or endpoint:
- Saved-view or filter identity/version:
- Visible filters:
- Requested period start:
- Requested period end:
- Period timezone rule:
- Source-period closure state:
- Export run ID:
- Export started at:
- Export completed at:
- Export actor or process:
- Pagination, cursor, or row-limit behavior:
- Source-side result count, if supplied:

## 3. Frozen file

- File name:
- File format:
- Byte size:
- SHA-256:
- Schema or data-dictionary identity:
- Observed row count:
- Observed facility count:
- Observed facility IDs:
- Minimum source timestamp:
- Maximum source timestamp:
- Required-field null count:
- Duplicate business-key count:

## 4. Population reconciliation

- Expected but not observed:
- Observed but not expected:
- Duplicate or unmapped facility identities:
- Facilities with zero qualifying activity but an explicit source record:
- Facilities whose value is not established:
- Known source or transport limitations:

## 5. Variance control

For each variance, record the facility or record set, condition, consequence, owner, due time, required evidence, and operating boundary while unresolved.

## 6. Release decision

- Disposition: eligible / limited use / hold / reject
- Reviewer:
- Reviewed at:
- Reason:
- Permitted use:
- Prohibited use:
- Correction or rerun ID:
- Supersedes export run ID:
- Receipt status: prepared / reviewed / released / superseded

## Non-negotiable rule

Do not convert an absent facility or missing period into zero. Record the value as `not evaluated` until the intended population and period are established.
