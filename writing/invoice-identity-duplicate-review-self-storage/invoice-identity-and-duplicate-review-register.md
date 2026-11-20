# Invoice Identity and Duplicate Review Register

Use the blank CSV to distinguish intake artifacts, invoice documents, candidate obligations and later financial events. The register is a diagnostic and routing aid. It does not approve, reject, post, pay or establish the validity of an invoice.

## Relationship states

| State | Use when | Required next step |
|---|---|---|
| Exact artifact duplicate | Content hash and material file properties match | Preserve receipt event; link to existing document |
| Probable obligation duplicate | Different artifacts materially align on governed identifiers and scope | Hold and review against governing records |
| Related revision | New document purports to correct or replace an earlier one | Preserve lineage; verify which version governs |
| Legitimate related charge | Similarity is explained by recurring, split, milestone or multi-facility billing | Record the distinguishing basis |
| Unresolved | Evidence cannot support classification | Assign owner, next check and due time |

## Review gate

- Confirm that raw values and normalized values are both retained.
- Compare approved vendor and facility identifiers, not names alone.
- Keep allocations below one obligation identity.
- Preserve revisions, credits, rebills and supporting artifacts as linked records.
- Separate detected, held, reviewed, released/linked/rejected, posted and reconciled states.
- Do not infer fraud, validity, approval, posting or payment from a duplicate signal.
- Point the final state to the governing financial record or documented no-post decision.

The worked CSV is explicitly fictional. It contains no customer, vendor, facility, invoice, payment or performance evidence.
