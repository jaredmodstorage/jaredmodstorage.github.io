# Portfolio Delinquency Definition and Reconciliation Contract

Use this tool to define and reconcile a portfolio delinquency measure. It is a measurement contract, not legal advice, an accounting determination, a customer-contact authorization, a notice schedule or authority to change access, fees, ledgers or account status.

## Definition contract

1. **Name the unit.** State whether the observation is a rental agreement, customer-facility relationship, occupancy episode or another governed entity. Record the stable identifier.
2. **Name the balance predicate.** Identify source fields, included components, pending states, currency, precision and comparison threshold.
3. **Name the clock.** Record the as-of timestamp, facility named time zone, local day boundary and date fields used.
4. **Name eligibility.** Version included agreement states and every exclusion or exception reason.
5. **Store the denominator.** Preserve the eligible population beside the count and amount.
6. **Preserve membership.** Retain included IDs, excluded IDs, provisional records, source snapshot and checksum.
7. **Bridge changes.** Compare old-only, both, new-only and unresolved membership before releasing a revised series.
8. **Hold the action boundary.** Require current authoritative records and governing policy before customer-specific action.

## Diagnostic table

| Check | Pass evidence | Hold condition |
|---|---|---|
| Unit consistency | Every facility uses the same entity type and stable identity rule | “Account” changes meaning across sources |
| Balance consistency | Field lineage and component treatment match the approved version | Pending credits, reversals or disputes are undefined |
| Time consistency | RFC 3339 timestamp, named zone and local boundary are retained | Unqualified local time or stale offset controls membership |
| Eligibility consistency | Included and excluded states have versioned reason codes | Missing source state is coerced to eligible or ineligible |
| Denominator integrity | Eligible population is stored with source coverage | Rate is published without a reproducible base |
| Cohort reproducibility | Membership and snapshot checksum reproduce the total | Only the aggregate survives |
| Change reconciliation | Old-only, both, new-only and unresolved rows explain the bridge | Definition change rewrites history silently |
| Action separation | Current record and authority are checked independently | Metric membership directly triggers customer action |

The blank CSV contains the complete contract fields. The completed CSV is explicitly fictional teaching material.

