# Unit Type Attribute and Comparability Contract

Use one record per facility-local unit type and mapping version. The contract defines meaning and comparison eligibility; it does not replace the unit-instance inventory, rental agreement, customer-facing description, rate record or availability record.

## Contract rules

1. Assign a durable portfolio unit-type ID that is not generated from the current display label.
2. Preserve the exact local source code, preferred label and alternate labels.
3. Record physical, access, environmental-description and commercial attributes separately.
4. Give every numeric field an explicit unit and measurement/source method.
5. Distinguish `unknown`, `not mapped`, `not applicable`, `conflicted` and actual zero values.
6. Declare comparison eligibility by named purpose; do not assume one universal comparable group.
7. Record the required attributes, exclusions and denominator effect for each comparison.
8. Version mappings and material definitions with effective timestamps, approver and evidence.
9. Preserve historical mappings unless a controlled correction/restatement decision is recorded.
10. Verify required downstream consumers after release; a saved source record is not full reconciliation.

## Release gate

A mapping is ready only when the facility and local code are exact, the portfolio type exists, required attributes are sourced, conflicts are resolved or explicitly carried, comparison eligibility is declared, effective dates are valid, approval is recorded and required downstream readbacks match.

## Stop conditions

Hold the affected comparison or mapping when facility identity is ambiguous, a local code maps to multiple active types, a material attribute lacks a source, units are missing, an effective interval overlaps another active mapping, a customer-facing promise conflicts with the contract, or a required downstream consumer still shows the prior meaning.

## Claim boundary

The contract may establish how the portfolio classifies and compares records. It does not prove measured dimensions, climate performance, accessibility compliance, customer fit, availability, occupancy, rate, revenue, conversion, asset condition or facility performance without separate governing evidence.

The blank implementation template is `unit-type-attribute-and-comparability-template.csv`. The companion teaching data in `unit-type-attribute-and-comparability-fictional-example.csv` is entirely fictional.
