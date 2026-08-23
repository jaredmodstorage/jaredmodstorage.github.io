# Metric claim card

Use one card for one metric definition, decision use, population, and release context. Duplicate the card when any of those changes.

## Control

- Metric ID:
- Metric name:
- Definition version:
- Card version:
- Decision supported:
- Intended audience:
- Facility-set ID and version:
- Owner:
- Reviewer:
- Release state: `candidate` / `diagnostic` / `approved-internal` / `approved-external` / `held` / `retired`
- Effective from:
- Expires or review due:
- Correction owner and route:

## Expression

- Unit of analysis:
- Display unit:
- Formula:
- Displayed value:
- Numerator count or amount:
- Denominator count or amount:
- Weighting or aggregation method:
- Rounding rule:

## Numerator contract

- Qualifying record or event:
- Inclusion rule:
- Exclusion rule:
- Reversal or correction rule:
- Deduplication key and version:
- Unknown-state treatment:

## Denominator contract

- Eligible population in plain language:
- Inclusion rule:
- Exclusion rule:
- Entry event:
- Exit event:
- Snapshot or cohort rule:
- Maturity rule:
- Late-arrival policy:
- Unknown-state treatment:

## Time and scope

- Observation start:
- Observation end:
- As-of time:
- Named time zone:
- Included facility IDs:
- Excluded facility IDs and reasons:
- Lifecycle restrictions:
- Channel, product, unit, or customer restrictions:

## Source and transformation

- Authoritative source owner:
- Source system and record type:
- Authoritative fields:
- Extraction timestamp:
- Source snapshot or export hash:
- Query, semantic model, or code version:
- Transformations:
- Conflicting source and disposition:
- Reproduction route:

## Quality and uncertainty

- Missing record count:
- Unknown-state count:
- Source coverage:
- Sample size and sampling method, if any:
- Known uncertainty components:
- Sensitivity result under alternate denominator:
- Comparator identity and version:
- Comparability decision:
- Limitations shown with the metric:

## Review

- Can a reviewer reproduce numerator membership? `yes` / `no`
- Can a reviewer reproduce denominator membership? `yes` / `no`
- Does the metric show `numerator / denominator`? `yes` / `no`
- Are definition, facility set, query, and source versions recorded? `yes` / `no`
- Are exclusions, missing records, unknown states, and late events disclosed? `yes` / `no`
- Does the conclusion survive the approved sensitivity test? `yes` / `no` / `not run`
- Is this definition approved for this exact decision and audience? `yes` / `no`
- Final disposition and reason:

## Compact display

`[value] ([numerator] / [denominator]) · [window/cohort] · [facility set] · [maturity] · [exclusions] · [coverage] · [definition version] · [calculated at + time zone] · [owner] · [state]`

## Boundary

This card documents an authored operating control. Completion does not establish correctness, comparability, legal compliance, external eligibility, customer impact, publication, indexing, coverage, recognition, or certification. Resolve material uncertainty with the qualified source owner and decision owner.
