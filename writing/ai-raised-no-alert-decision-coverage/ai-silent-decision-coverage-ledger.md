# AI Silent-Decision Coverage Ledger

Use this ledger for an operating cycle in which an AI-assisted workflow can produce alerts, recommendations, abstentions, or no visible output. It reconciles the expected population through execution and delivery, then records negative-decision sampling and safe sentinel checks.

## Reconciliation equation

Start from an authoritative expected population. Reconcile:

`expected = received + missing`

`received = identity_resolved + identity_unresolved`

`identity_resolved = eligible + not_eligible`

`eligible = evaluated + not_evaluated`

`evaluated = alert + evaluated_negative + below_threshold + abstained + other_disposition`

Then reconcile required alert deliveries separately. Never force an unresolved record into `evaluated_negative` to make the counts tie.

## No-alert classes

- `evaluated_negative`
- `below_threshold`
- `abstained`
- `suppressed`
- `not_eligible`
- `not_evaluated`
- `alert_not_delivered`
- `unresolved`

## Negative review

Document the sample method, population, sample size, risk strata, evidence source, reviewer authority, scorable count, confirmed negatives, missed conditions, source defects, policy disagreements, and unscorable cases. Do not represent a complaint-driven or convenience sample as portfolio performance.

## Sentinel check

Use only controlled, labeled, non-consequential tests. Record the expected result, observed path, versions, and containment. Never permit a sentinel to message a real customer, change access, dispatch a vendor, create a production charge, or alter a real facility record.

## Final decision

- `hold`: population unknown or material gap unresolved
- `limited`: verified subset released; named scopes excluded
- `observed`: population reconciled; sample or monitoring window open
- `reconciled`: counts tie, exceptions are bounded, required review is complete, and delivery is accounted for

This tool is an operating control, not a certification, model-validation report, facility-safety determination, legal opinion, or claim about a deployed product.
