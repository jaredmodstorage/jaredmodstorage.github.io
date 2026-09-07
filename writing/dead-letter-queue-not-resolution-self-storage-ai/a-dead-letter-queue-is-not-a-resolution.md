# A Dead-Letter Queue Is Not a Resolution: Recovering Failed AI Work in Self-Storage

**Deck:** A failed record is contained, not resolved. Safe recovery requires the operator to preserve its history, classify the failure, recheck current authority and reconcile any business effect.

**By Jared Mastroianni**

<!-- BODY START -->
A self-storage workflow receives a facility record, asks a model to classify it, and tries to pass the result to the next system. The consumer rejects the message. After several retries, the record lands in a dead-letter queue.

The dashboard turns green because the main queue is moving again.

That is a technical recovery, not an operating resolution. The failed record may still represent an unreviewed maintenance condition, an access change that never reached its governing system, a duplicate request, or an action whose outcome is unknown. Moving it out of the live path prevents one bad record from blocking other work. It does not determine what the business now owes.

This distinction matters more as AI enters multi-location operations. Model output adds versions, source selections, prompts, tool calls and uncertainty to a message path that already has facility identity, policy, permissions, provider behavior and human decisions. If a team treats every failure as “retry later,” it can repeat an obsolete recommendation, apply a corrected record twice, or act on evidence that no longer reflects the facility.

A dead-letter queue should be governed as a quarantine boundary. It holds failed work while the organization decides whether to repair, replace, supersede, deny or safely replay it. Resolution happens only when the underlying operating obligation has a named disposition and any resulting state has been read back from the appropriate source.

## Containment is a useful first move

Dead-letter queues are a standard messaging pattern. Amazon SQS describes them as destinations for messages that were not processed successfully and notes their value for isolating failures for diagnosis.[^1] Azure Service Bus likewise provides a dead-letter subqueue for messages that cannot be delivered or processed, with reason and description fields available for dead-lettered records.[^2]

Those are infrastructure behaviors. They do not define a self-storage operating policy.

The queue can tell a technical owner that a consumer rejected an event after five receives. It cannot decide whether the event still represents valid work, whether another path already completed the action, whether a human corrected the condition, or whether replay is still authorized. Even the phrase “poison message” can mislead an operating team. The record may be technically malformed while describing a legitimate obligation. The payload may be valid while the requested action is prohibited. The failure may have occurred after a provider accepted the request but before the caller received the response.

Containment therefore needs an explicit state name: `quarantined_pending_disposition`. Do not label the work closed, fixed or safely failed merely because it left the primary queue.

## Separate the message failure from the business state

Every quarantined record carries at least two questions:

1. Why could the workflow not continue?
2. What is now true in the facility or governing business system?

The first question is technical. The second is operational. They often require different evidence and different owners.

A schema error can be established from validation logs. It does not establish that the underlying door condition was addressed. A timeout can be established from a client trace. It does not establish that the provider rejected the action. A model-service outage can explain why no classification was produced. It does not establish that the input was harmless.

Build the recovery workflow around five failure classes:

- **Transient delivery failure:** the request is still valid and the dependency may recover, but retries must remain finite and bounded.
- **Deterministic data or schema failure:** the same bytes will fail again until the record, mapping, contract or consumer changes.
- **Authority or policy failure:** the workflow lacks permission, required approval, applicable policy or allowed consequence scope. A retry cannot grant authority.
- **Ambiguous side effect:** the caller lacks a reliable response, but the receiving system may have acted. Repeating the request could duplicate the effect.
- **Expired or superseded work:** the original record has been overtaken by a correction, later observation, manual decision, policy change or completed action.

Microsoft's retry guidance makes the same narrower technical distinction between transient faults and failures that should be canceled or treated as exceptions. It also warns that retrying a non-idempotent operation can produce the action more than once.[^3] The operator consequence is straightforward: failure class must be known before the replay control is enabled.

## Freeze the failed-work packet

A team cannot investigate a failure if the evidence changes while it is being reviewed. Preserve an immutable failed-work packet when the message enters quarantine.

At minimum, retain:

- original message bytes or a protected reference and cryptographic hash;
- source, destination, message identifier and correlation chain;
- facility, asset, unit or workflow identity used at failure time;
- event type, schema version and transformation history;
- model, prompt, retrieval, rule, tool and workflow versions when applicable;
- policy version, authority scope and consequence class;
- occurrence, enqueue, receive, processing and quarantine times;
- attempt count, backoff history, error code and error text;
- exact processing stage and last completed checkpoint;
- provider receipts, tool responses and known side effects;
- sensitive-data class, access restriction and retention rule; and
- current owner, disposition deadline and permitted next states.

CloudEvents provides a vendor-neutral event envelope with required context attributes such as `id`, `source`, `specversion` and `type`.[^4] That is useful interoperability plumbing. Its own primer leaves processing semantics, error handling and domain meaning to the producer and consumer. A compliant envelope therefore does not establish that a failed event is complete, authorized, current or safe to replay.

The failed-work packet closes that gap for the operator's workflow. It preserves the original event and adds the decision evidence needed for recovery. If the payload contains customer or access information, the packet should point to protected evidence rather than spreading sensitive details through queue labels, alerts and exported spreadsheets.

## Do not send every dead letter to a human review queue

Human review is for a bounded decision, not for every technical exception.

A malformed JSON document may belong with the integration owner. An expired facility mapping may belong with the identity steward. A prohibited action should be denied by policy. A provider outage may belong in incident response. A record with an ambiguous side effect may require a qualified operator to choose between reconcile, compensate and escalate.

Putting all five into one review queue creates two problems. Technical defects consume decision capacity, and reviewers are asked to approve work before the evidence is ready.

Route quarantined records by both processing stage and consequence:

| Quarantine lane | What failed | Default owner | Permitted next move |
|---|---|---|---|
| Input admission | Identity, schema, required field or source eligibility | Data or integration owner | Repair source or mapping; rebuild candidate |
| Recommendation build | Retrieval, model, rule or transformation | AI workflow owner | Rebuild under a declared version; retain old output |
| Authorization | Policy, permission, role or consequence boundary | Decision authority or policy owner | Deny, obtain valid authority, or redesign scope |
| Execution | Tool or provider request | System owner plus operating owner | Reconcile first; retry only if duplicate effect is controlled |
| Readback | Result cannot be independently confirmed | Operating owner | Hold closure; inspect governing source and escalate mismatch |

The queue lane is not the final status. It is a routing control. A record can move from an execution lane to an incident path, or from input admission to `superseded`, without ever becoming a human approval case.

## Replay is a new release decision

Redrive tools make it easy to move messages back into processing. Amazon SQS, for example, supports redrive to a source or compatible destination queue and recommends starting at a low velocity so the destination is not overwhelmed.[^5] Its documentation also notes that redriven messages receive a new message identifier and enqueue time, and that redriven and newly produced messages can interleave.[^5]

That means replay is not restoration of the old moment. It is a new processing event in the current operating world.

Before replay, verify seven conditions:

1. **The failure cause is understood.** A changed symptom is not proof that the cause was corrected.
2. **The original intent is still valid.** The work has not expired, been canceled, completed manually or replaced by a later decision.
3. **Current facility state supports the action.** Recheck the governing sources required by the consequence.
4. **Versions remain compatible.** Identify the schema, mapping, model, prompt, policy and consumer versions that will process the record now.
5. **Prior side effects are known.** Reconcile the destination before repeating an ambiguous request.
6. **Duplicate execution is controlled.** Use an idempotency or deduplication design appropriate to the receiving system; do not invent protection the provider does not offer.
7. **The replay is bounded.** Name the batch, velocity, stop conditions, observer, rollback or compensation path and post-run readback.

Bulk redrive should be treated like a production release. Start with representative records across failure families and consequence classes. Stop if the same defect repeats, a new mismatch appears, the destination slows, or the governing state cannot be confirmed. A falling queue count is not sufficient evidence.

## A fictional record that should not be replayed

North Hollow Storage is an entirely fictional operator. The facility, systems, records, people, times and outcomes below are invented for instruction and do not describe modSTORAGE, Facily.ai or any deployment.

In the fictional workflow, an inspection note enters an AI-assisted maintenance classifier. The record names a facility identifier retired during a prior migration. The classifier produces a recommendation to isolate a roll-up door from rental availability, but the authorization consumer rejects the message because it cannot resolve the facility identity. After the retry limit, the record is quarantined.

Two days later, an integration owner repairs the identifier crosswalk and proposes replaying every failed record. The original message now validates. That does not make replay correct.

The recovery owner finds a later manual inspection tied to the governing facility identifier. It documents that the door note belonged to a different unit and that the affected unit was already placed into the appropriate operating state through the approved manual workflow. The original AI recommendation is both mis-scoped and superseded.

The correct disposition is `resolved_without_replay`. The packet links the identity defect, the governing later inspection, the manual operating-state record and the crosswalk correction. The team also tests other messages that used the retired identifier. It does not rewrite the original event, delete the model output or pretend the workflow completed automatically.

This is why queue depth is a poor measure of resolution. North Hollow could empty the queue by replaying the record and create a new error. Keeping one record with a proved superseded disposition is better than producing a technically successful duplicate action.

## Close the obligation, not the queue entry

A failed-work record needs a small, explicit set of terminal states:

- `replayed_and_reconciled`;
- `resolved_without_replay`;
- `superseded_with_evidence`;
- `duplicate_with_governing_match`;
- `invalid_or_prohibited`;
- `compensated_and_reconciled`; or
- `escalated_to_named_owner` when closure belongs to another controlled process.

None of those states should be assigned from the message broker alone. Closure requires the disposition decision, the person or policy authorized to make it, the evidence used, and the governing readback where an operating effect was possible.

Measure the recovery system accordingly. Track age by consequence, oldest unresolved ambiguous side effect, repeated failure family, records missing a complete packet, replay recurrence rate, superseded-work rate and time from quarantine to operating disposition. Keep technical throughput and business closure as separate measures.

NIST's AI Risk Management Framework is voluntary guidance and is currently being revised. Its governance and management functions emphasize documented roles, ongoing monitoring and treatment of identified risks; the Generative AI Profile adds suggested actions around incident communication and response roles.[^6][^7] Those sources do not prescribe a dead-letter design or certify an implementation. They support the broader obligation to make responsibility, monitoring and response explicit when AI components participate in operational work.

The design principle is simpler than the infrastructure: a failed message must not disappear, and it must not regain authority merely because a retry button exists. Preserve what failed. Establish what happened. Decide what remains valid now. Re-enter only the work that is still authorized, then verify the result from the system that governs it.

A dead-letter queue can protect the live workflow. Only a controlled disposition can protect the operation.
<!-- BODY END -->

---

## References

[^1]: Amazon Web Services, “Using dead-letter queues in Amazon SQS,” accessed September 4, 2026.
[^2]: Microsoft, “Service Bus dead-letter queues,” accessed September 4, 2026.
[^3]: Microsoft Azure Architecture Center, “Retry pattern,” accessed September 4, 2026.
[^4]: Cloud Native Computing Foundation, “CloudEvents Specification v1.0.2,” accessed September 4, 2026.
[^5]: Amazon Web Services, “Learn how to configure a dead-letter queue redrive in Amazon SQS,” accessed September 4, 2026.
[^6]: National Institute of Standards and Technology, “AI Risk Management Framework,” accessed September 4, 2026.
[^7]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*, NIST AI 600-1, July 2024, accessed September 4, 2026.

## Assistance and claim disclosure

AI assistance supported research synthesis, drafting and editorial QA. The architecture, scenario and recovery register are editorial methods, not evidence of a product feature, deployed system, customer result or industry standard. All North Hollow Storage details are fictional.
