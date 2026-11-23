# Published Offer Contract and Reconciliation Grid

Use this tool to distinguish an intentional offer difference from an unexplained pricing conflict. Create one offer-definition record for each effective version, one observation record for every channel checked, and one correction record for every affected destination.

**Important:** This is an operating-control template, not legal, tax or accounting advice. Define fee and disclosure requirements with qualified counsel for each jurisdiction. Never overwrite a prior version to make the history look consistent.

## 1. Offer-definition record

| Field | Required record |
|---|---|
| Offer identity | Stable offer version ID; portfolio; facility ID; unit-group ID; product attributes |
| Authority | Governing source by attribute; accountable owner; approval reference; precedence rule |
| Effective interval | Start; end; time zone; scheduled or immediate activation |
| Price components | Standard rate; published rate; promotion type/value; mandatory fees; conditional fees; tax treatment |
| Eligibility | Customer class; channel; inventory scope; promotion conditions; exclusions |
| Transaction terms | Quote validity; reservation hold; cancellation or expiration rule; agreement treatment |
| Evidence | Source record IDs; version; approval artifact; creation and observation timestamps |

## 2. Channel reconciliation

| Question | Pass condition | Exception examples |
|---|---|---|
| Same product? | Facility, unit group and material attributes match | Wrong unit mapping; marketing label substituted for product ID |
| Same audience? | Eligibility and channel scope match | New-customer offer compared with existing-customer charge |
| Same time? | Observation falls inside the governing effective interval | Stale cache; missing time zone; future offer published early |
| Same components? | Base rate, promotion and defined fees are compared like for like | First-period total compared with base rate; required fee omitted |
| Same transaction state? | Published, quoted, reserved, leased or charged state is explicit | Valid reservation hold treated as a current web mismatch |
| Traceable? | Source record, owner, approval and transformation path are present | Manual override with no authority; unexplained feed value |

## 3. Exception and correction record

- Classify: expected variance, timing lag, stale cache, eligibility gap, mapping error, unauthorized override, incomplete disclosure, inventory mismatch or unresolved source conflict.
- Record the original observation without editing it.
- Assign impact, owner, target time and the customer population potentially affected.
- Correct each destination through its approved path.
- Capture distribution acknowledgement and live readback separately.
- Review quotes, reservations, leases or charges created during the affected interval.
- Close only when the governing record, distributed surface and required transaction review agree.

## Recommended operating cadence

1. Reconcile all channels after a consequential offer, promotion, fee or mapping change.
2. Sample public, call-center and property surfaces on a routine schedule.
3. Review high-impact unresolved exceptions daily; age lower-impact items against a defined service level.
4. Publish completeness, effective-version match, open-impact and readback metrics with their definitions.
5. Retain prior versions and correction receipts so the offer can be reconstructed as of any customer observation.

The blank CSV is ready for portfolio use. The separate example CSV is explicitly fictional and should never be imported as production data.

