# Portfolio Source Watermark and Batch Release Register

Use one batch contract and one row per required facility-source pair. Do not infer a watermark from a filename or receipt time.

## Batch contract

| Field | Entry |
|---|---|
| Run ID / purpose | |
| Comparison instant and UTC rule | |
| Facility population version | |
| Required sources | |
| Arrival window / correction policy | |
| Release owner / second verifier | |

## Facility-source row

| Control | Required evidence | Hold condition |
|---|---|---|
| Identity | Facility ID, source, extract name | Wrong or ambiguous source/facility |
| Time | Watermark, basis, extraction and receipt timestamps | Watermark missing or outside contract |
| Integrity | Object ID, filename, digest, record count | Bytes or declared scope uncertain |
| Supersession | Prior object, reason, approver | Replacement relationship unclear |
| Validation | Schema, population and reasonableness checks | Required check failed or not run |
| Exception | Owner, due time, limitation, consumer disclosure | Effect or authority unresolved |
| Release | State, decision time, second verifier | Independent readback incomplete |

## Batch release checklist

- [ ] Every required facility-source pair has one row.
- [ ] Every watermark satisfies the same comparison rule.
- [ ] Timestamps include an unambiguous UTC relationship.
- [ ] Digests identify the exact files or objects reviewed.
- [ ] Replacements identify the inputs they supersede.
- [ ] Exceptions are visible to downstream consumers.
- [ ] The second verifier reproduced the decision.

**States:** Ready · Limited · Hold · Superseded.

This tool is a reporting release control, not accounting, legal, security or compliance advice.
