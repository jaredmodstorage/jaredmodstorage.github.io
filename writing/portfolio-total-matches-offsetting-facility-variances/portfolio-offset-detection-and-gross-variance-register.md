# Portfolio Offset Detection and Gross Variance Register

Use this register to determine whether a matching portfolio total contains offsetting facility-level errors. Create one row per facility plus one portfolio-summary row. Do not copy restricted customer data into the register; link to controlled evidence.

## Metric contract

- Reconciliation ID:
- Metric ID, name and version:
- Unit of measure:
- Reporting period and time-zone rule:
- Included and excluded states:
- Facility population and effective dates:
- Source and target systems:
- Facility-identity rule:
- Transformation and mapping versions:
- Late, reversed, deleted and transferred-record treatment:

## Facility calculation

For each facility:

- `signed_variance = observed_value - expected_value`
- `absolute_variance = abs(signed_variance)`

For the portfolio:

- `portfolio_net_variance = sum(signed_variance)`
- `portfolio_gross_variance = sum(absolute_variance)`
- if gross variance is greater than zero, `offset_ratio = 1 - (abs(net variance) / gross variance)`

Do not calculate an offset ratio when gross variance is zero.

## Required row controls

- Confirm comparison status before interpreting a variance.
- Assign evidence-backed reason codes; “offset by another site” is not a root cause.
- Keep detection, explanation, authorization, correction, validation and historical treatment as separate states.
- Do not link positive and negative rows without record-level or mapping evidence.
- Preserve the original frozen extracts and configuration versions.
- Record unsupported or unavailable evidence as a limitation, not a pass.

## Release states

- **Not comparable:** metric contract, population or period differs.
- **Comparable—open:** calculation is valid but one or more facility rows remain unresolved.
- **Comparable—bounded exception:** remaining facility rows have approved owners, evidence requirements and due times.
- **Reconciled:** facility rows and portfolio result meet the documented release rule.

This tool is an adaptable operating control. It is not an accounting opinion, audit standard, cybersecurity assessment, product certification or legal requirement.
