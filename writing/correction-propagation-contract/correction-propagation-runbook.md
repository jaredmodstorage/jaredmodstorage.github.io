# Correction propagation runbook

Status: proposed operating tool by Jared Mastroianni. All examples and identifiers are fictional. This runbook is not a product description, deployment record, legal or safety instruction, accounting policy, certification, or evidence that any correction occurred.

Use this runbook when a qualified facility assertion may have been wrong and one or more consumers could still hold, display, derive from, or act on the predecessor.

## Stop conditions

Stop and route to the named consequence-qualified owner when any of the following is true:

- subject or facility identity is ambiguous;
- governing source or correction authority is unknown;
- effective time cannot be bounded;
- the predecessor changed after qualification;
- protected values would leave their approved access boundary;
- a replay could repeat a financial, access, customer-message, physical, legal, or safety effect;
- a known consumer has no accountable owner;
- two correction packets compete for the same predecessor;
- dependency closure is cyclic or materially incomplete;
- rollback or compensation is required but unauthorized.

Stopping is a controlled state. Record why, who owns the next decision, and when it must be reviewed.

## Phase 1 — qualify the assertion

- [ ] Assign a correction ID.
- [ ] Identify the exact subject and fact path.
- [ ] Preserve the superseded assertion ID and value or protected hash.
- [ ] Create a separate governing candidate assertion ID.
- [ ] Record discovery, effective, and recorded time separately.
- [ ] Record the evidence reference and correction reason.
- [ ] Verify the authority identity, scope, and current status.
- [ ] Classify confidentiality and consequence.
- [ ] State what the evidence does not prove.

Output: a qualified candidate, not an executed correction.

## Phase 2 — freeze dependency closure

Create `dependency_snapshot_id` from a dated consumer inventory and exact discovery method.

Inspect these seven classes:

1. governing source;
2. replicas, caches, indexes, and read models;
3. metrics, reports, exports, and other derivatives;
4. workflows, automations, queues, and pending actions;
5. AI retrieval, features, recommendations, evaluations, and memory;
6. messages, documents, listings, and public surfaces;
7. completed real-world actions.

For every consumer, record:

- consumer ID and owner;
- how it depends on the predecessor;
- whether it has already been used;
- consequence class;
- proposed disposition;
- execution precondition;
- readback method;
- rollback or compensation;
- deadline and residual owner.

Record unknown or unreachable consumers as gaps. Do not silently omit them.

## Phase 3 — assign one disposition

Choose exactly one primary disposition per consumer:

| Disposition | Use when | Minimum completion evidence |
| --- | --- | --- |
| Replace | Mutable consumer should hold the governing assertion | Conditional write receipt plus current readback |
| Recompute | Derived artifact must be regenerated | Inputs, transformation version, output ID, comparison |
| Retract | Artifact must remain preserved but become ineligible | Retraction state plus current-use query |
| Invalidate | Cache, index, retrieval object, or decision input must refresh | Invalidation receipt plus uncached or rebuilt readback |
| Replay | Bounded process must rerun against corrected input | Original event, correction, idempotency, suppressed effects, final state |
| Annotate | Immutable history must retain predecessor and correction | Original hash, correction link, current eligibility state |
| Notify | Recipient or external owner needs a correction packet | Exact send state and separate delivery/receipt tracking |
| Quarantine | Consumer cannot safely remain in decision use | Exclusion state and owner/readiness gate |
| No action | Consumer is intentionally retained | Reason, authority, consequence review, next review date |
| Cannot reverse | Real-world effect cannot be undone by data mutation | Escalation, owner disposition, compensation or accepted residual |

Secondary steps can be recorded, but one primary disposition keeps the packet testable.

## Phase 4 — authorize the exact packet

- [ ] Source owner approves the governing assertion.
- [ ] Consumer owners approve high- or critical-consequence dispositions.
- [ ] Financial, access, privacy, safety, legal, or customer-communication reviewers approve only the fields within their actual scope.
- [ ] Dependency snapshot has not changed materially.
- [ ] Preconditions still match the predecessor.
- [ ] Idempotency keys are stable.
- [ ] Replay side effects are listed and suppressed unless separately authorized.
- [ ] Rollback or compensation is executable.

Approval applies to one exact packet version. A later dependency or assertion change requires a rebase or superseding packet.

## Phase 5 — propagate in consequence order

Recommended sequence:

1. quarantine unsafe current use;
2. correct the governing source with a precondition;
3. update replicas and read models;
4. rebuild derivatives;
5. invalidate AI and search context;
6. repair pending workflow state;
7. issue approved notices;
8. address nonreversible effects.

Record execution state and receipt per consumer. Do not advance failed consumers because another consumer succeeded.

## Phase 6 — read back independently

The readback should not merely repeat the write API response.

Use the governing observation for each consumer:

- fresh source query;
- uncached HTTP request;
- exact replica version;
- report row and manifest hash;
- workflow state and pending-side-effect query;
- retrieval probe with source/version disclosure;
- immutable recommendation correction link;
- public page and structured-data fetch;
- exact sent-item and delivery-state ledger;
- physical or provider-state inspection by an authorized owner.

Label readback `matched`, `mismatched`, `pending`, `unavailable`, or `not_applicable`.

## Phase 7 — reconcile

Reconciliation requires:

- every required consumer has a disposition;
- every executed disposition has a receipt;
- every required output has independent readback;
- mismatches and failures have owners;
- tombstone or retention deadlines remain satisfied;
- historical artifacts preserve their original identities;
- nonreversible effects have an approved residual or compensation;
- current publication, message, workflow, and AI states are named separately;
- next review date is set.

Close as one of:

- `reconciled_no_residual`;
- `reconciled_with_accepted_residual`;
- `superseded_by_new_correction`;
- `withdrawn_candidate`.

Never use `write_succeeded`, `job_completed`, `request_sent`, `provider_accepted`, or `cache_cleared` as a synonym for reconciliation.

## Minimum evidence packet

- [ ] correction record and version;
- [ ] protected predecessor and candidate evidence;
- [ ] authority and approval record;
- [ ] dependency snapshot and known-gap statement;
- [ ] consumer-level register rows;
- [ ] transformation, snapshot, event, index, or message versions;
- [ ] execution receipts;
- [ ] independent readback results;
- [ ] rollback or compensation evidence;
- [ ] residual ledger and next review date;
- [ ] outcome statement separating correction, delivery, publication, indexing, coverage, and recognition.

## Operator exercise

Use fictional data only.

1. Create one facility-hours assertion and four consumers.
2. Correct the assertion while preserving predecessor and candidate IDs.
3. Assign four different dispositions.
4. Add a sent message that cannot be reversed.
5. Add a lagging event consumer whose tombstone window is about to expire.
6. Add an AI retrieval chunk and an immutable recommendation.
7. Design independent readback for each consumer.
8. Introduce a second authorized correction before reconciliation.
9. Decide which packet is superseded and prove that no consumer can regress to the first predecessor.

The exercise passes only when every consumer is accounted for and the residual is explicit.
