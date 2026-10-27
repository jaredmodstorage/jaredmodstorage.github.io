# AI Action Revocation Propagation Test

Use this test for one consequential agent action type and one complete execution path at a time. It is an architecture and operations diagnostic, not a certification or substitute for security, privacy, legal, safety, provider or policy review.

## 1. Define the action and authority

- [ ] Action type and bounded parameters are named.
- [ ] Facility, target object and target system are identified.
- [ ] Roles allowed to approve, revoke, reinstate and recover are documented separately.
- [ ] The authoritative action record and versioning rule are named.
- [ ] Expiration and scope rules for approval are recorded.

## 2. Define the commit boundary

- [ ] The target-specific point of external commitment is written in observable terms.
- [ ] The receipt or readback that proves the boundary was crossed is named.
- [ ] `accepted`, `created`, `posted`, `sent`, `enabled`, `closed` and similar target states are not treated as synonyms unless the governing contract proves they are.
- [ ] The pre-commit revocation behavior and post-commit recovery behavior are different.

## 3. Map every execution copy

Record the interface, orchestrator, scheduler, queue, worker, connector, target and any human or physical downstream process. For each, name:

- action and correlation identifiers;
- local state or projection;
- how revocation reaches it;
- how it rejects stale versions;
- its acknowledgment evidence; and
- timeout, retry and restart behavior.

## 4. Run three controlled cases

### Case A — revoked while queued

- [ ] Revoke after enqueue and before worker claim.
- [ ] Confirm the authoritative version advanced.
- [ ] Confirm queued work is removed, tombstoned or rejected on claim.
- [ ] Confirm no target receipt exists using the strongest available readback.

### Case B — revoked while executing, before commit

- [ ] Revoke after worker claim.
- [ ] Confirm the worker receives the stop signal or fails its next authority check.
- [ ] Confirm the connector rechecks authority immediately before the boundary.
- [ ] Confirm stale action version and scope cannot execute.
- [ ] Confirm no target effect using target evidence, not local silence alone.

### Case C — revoked at or after commit

- [ ] Force or simulate the boundary race.
- [ ] Record the ordering source and uncertainty.
- [ ] If committed, preserve the original receipt and set `recovery required`.
- [ ] Route recovery to a named authorized person.
- [ ] Record a compensating action as a separate action with its own approval and receipt.

## 5. Verify observability and handback

- [ ] One timeline joins approval, queue, worker, connector, revocation and target events.
- [ ] Operator view distinguishes `revocation requested`, `revoked before commit`, `committed`, `recovery required`, `recovered` and `unknown`.
- [ ] Missing evidence produces `unknown`, not an inferred success.
- [ ] The handback packet includes traces, state versions, target receipts, approved recovery options and named ownership.
- [ ] Alerts fire when revocation acknowledgments or target readbacks are late or absent.

## 6. Pass rule

A pre-commit test passes only when the revocation is durable, stale work cannot regain authority, every material execution path is resolved, the absence of the target effect is supported by the strongest available readback, and the operator can see the final disposition. A post-commit test passes only when the original effect remains visible, recovery is separately authorized and evidenced, and no interface mislabels the action as never executed.

The accompanying CSV files provide a blank implementation record and an explicitly fictional worked example.
