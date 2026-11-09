# Customer Communication Preference and Suppression Propagation Register

Use this tool to move a communication restriction from the place where it was received to every in-scope sender before another message is released. It is an operating-control template, not legal advice, a consent determination, or a substitute for current counsel-reviewed policy.

## Release gate

No communication candidate proceeds when an in-scope suppression is unresolved, the audience predates the governing state, or a required destination lacks verified enforcement.

## Seven control sections

| Section | Required evidence | Hold condition |
| --- | --- | --- |
| Source event | Event ID, contact point, channel, received time, source reference, exact requested action | Source or contact point cannot be resolved |
| Classification | Sender, purpose, scope, rule version, classifier, effective time | Meaning or scope requires qualified review |
| Identity | Customer candidates, facility records, match state, reviewer | Match is unresolved and the protective rule is unknown |
| Destination | System, provider, record key, expected enforcement state, owner | An in-scope sender is missing from the graph |
| Propagation | Attempt ID, submitted time, provider state, target state, readback time and evidence | Accepted update lacks target readback |
| Audience | Batch ID, source time, release time, suppression version, hash, exclusions | Audience predates the restriction or exceeds its age limit |
| Exception | Fallback, owner, deadline, expiration, restoration evidence, disposition | Fallback expired or no owner exists |

## Destination state vocabulary

Use `not_started`, `submitted`, `accepted_unverified`, `applied_verified`, `rejected`, `conflict`, `not_applicable`, or `unknown`. Only `applied_verified` proves that the named destination displayed or enforced the expected state at the recorded time. `Not applicable` requires an authorized scope decision.

## Ten-minute portfolio review

1. Select new requests, unverified destinations, stale audiences, conflicts, and expired fallbacks.
2. Reopen the source event and confirm the exact contact point, sender, channel, purpose, and received time.
3. Apply the current qualified classification rule; do not infer scope from message tone.
4. Resolve customer-record candidates without forcing a merge.
5. Compare every in-scope destination with its target readback.
6. Quarantine any audience built before the governing state or against an older suppression version.
7. Assign each exception to one owner with a due time and restoration condition.
8. Release only after all required destinations are `applied_verified` or validly `not_applicable`.

## Companion files

- `customer-communication-suppression-register.csv` — blank 40-field template
- `customer-communication-suppression-fictional-example.csv` — explicitly fictional worked example

The fictional rows are training data only. Adapt field names, retention, classification, authority, escalation, and release logic to the actual organization, providers, contracts, applicable law, and approved policy.
