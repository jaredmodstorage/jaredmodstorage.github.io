# The AI Recommended a Reset. What Evidence Would the Reset Erase?

*A responsible troubleshooting agent should preserve the evidence it is about to change—or make the resulting gap impossible to miss.*

By Jared Mastroianni

![A cross-functional operations and technology team reviews system evidence around a conference table.](assets/060-ai-development-ai-product-retrospective.png)

<!-- BODY START -->

An AI assistant sees repeated access failures at a facility and recommends restarting a controller. The recommendation may be reasonable. It may even restore service. But the reset can also change the very evidence needed to explain what happened: transient fault flags, an in-memory queue, local counters, open sessions, timestamps or the relationship between commands and device responses.

If the first action changes those signals, the operator may finish with a working device and a weaker incident record. “Healthy after restart” does not establish what was true before the restart. It does not prove the cause, confirm that the same condition will not return or justify treating reconstructed history as observation.

This is an architectural problem, not a reminder to take more screenshots. An AI system that can recommend or execute troubleshooting steps needs an **observe-before-act control**. Before an evidence-altering action is released, the system should identify the evidence at risk, preserve the permitted minimum, verify the preservation result and bind the action to a human-approved authority path. If urgent safety or continuity needs require immediate action, the control should allow the override while preserving an explicit evidence gap.

## A troubleshooting action can rewrite its own evidence

Most action controls ask whether a command is authorized, syntactically valid and directed at the right target. Those checks matter, but they do not answer a different question: **What will become unknowable after this command runs?**

A restart can end processes. A configuration push can replace the prior configuration. A retry can add new events to a queue. A cache clear can remove state. A diagnostic test can generate traffic that looks like the condition under investigation. Even opening an administrative interface can update access logs or “last viewed” fields.

The point is not that every change destroys evidence. The point is that the evidence effect must be classified before the action, not guessed afterward.

NIST’s forensic guidance was written for computer-security incident response and some IT troubleshooting, not for self-storage operations. Still, its core discipline is useful: identify relevant sources, understand volatility, acquire data deliberately and document the process. [NIST SP 800-86](https://csrc.nist.gov/pubs/sp/800/86/final) also warns that forensic practices must fit organizational policy and applicable legal requirements. That boundary matters here. An operator should not collect broadly just because data might be useful.

## Classify the action by its effect on evidence

An agent should assign every proposed troubleshooting step to one of five classes:

1. **Read-only observation.** Query a current status, retrieve an already-governed report or inspect an approved configuration view without intending to change the target state.
2. **Preservation action.** Export an approved diagnostic bundle, record a versioned configuration or capture selected fields needed for the case.
3. **State-changing diagnostic.** Run a test, poll or temporary configuration that may affect counters, queues, sessions or downstream events.
4. **Corrective action.** Restart, clear, replace, revoke, reconfigure or otherwise change the operating state to restore service or remove a fault.
5. **Emergency protective action.** Act immediately under the facility’s emergency or safety procedure when delay would create an unacceptable risk.

These classes should drive different release rules. Read-only does not mean risk-free; a query can expose sensitive data or create a log event. But a corrective or emergency action deserves an explicit evidence-impact review because it can close the window for observing the earlier state.

The classification also prevents a common shortcut: calling a reset “diagnostic” because the team hopes to learn from the result. If the reset changes the target, it is a state-changing or corrective action. Its diagnostic value does not make it observational.

## Build an evidence-at-risk map before release

Before the agent proposes a consequential step, it should create a bounded map of the sources that may change. The map does not need every possible log. It needs the sources that are relevant, authorized and time-sensitive.

For each item, record:

- the source system and exact facility or device identity;
- whether the state is volatile, short-lived or persistent;
- the expected retention window or capture deadline, when known;
- the approved fields and the fields that must be excluded or masked;
- the capture method and governing authority;
- the artifact identity, timestamp, version and integrity value;
- the person or service responsible for validating the capture; and
- the question the evidence can and cannot answer.

The map should distinguish a source from a conclusion. A controller status page can show a status value at a time. It does not, by itself, prove why the status occurred. An access-platform event may show a command was recorded. It may not prove a gate moved, a customer entered or the command reached a particular field device.

[RFC 3227](https://www.rfc-editor.org/rfc/rfc3227.html), an older IETF best-current-practice document for security evidence, recommends collecting more volatile information before less volatile information and documenting collection steps. Its security and evidentiary context is narrower than routine facility troubleshooting, and some of its techniques are not appropriate for an operator. The transferable lesson is sequencing: preserve authorized, relevant, perishable evidence before an action changes it.

## Put a preservation barrier in front of the action

The observe-before-act control should be a release barrier, not a paragraph in the AI’s explanation. The action remains held until the system can answer six questions:

1. **What exact action is proposed?** Bind an immutable action ID to the facility, target, command, parameters and expected effect.
2. **What evidence could change?** Link each at-risk source to the proposed action and its volatility class.
3. **What is permitted to be captured?** Apply purpose, privacy, retention and access rules before collection.
4. **Was preservation verified?** Require a receipt, artifact ID, timestamp and validation result—not “capture requested.”
5. **Who may release the action?** Revalidate the current human or policy authority at execution time.
6. **What happens if preservation fails?** Hold, narrow, hand back or use a documented emergency override. Never silently treat failure as success.

This barrier should sit between recommendation and execution. A language model may draft the proposed step and explain the tradeoff, but a deterministic control should evaluate the required fields, current policy, preservation receipts and authority. The final provider response and a post-action readback should remain separate from the model’s prediction.

[NIST’s Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf) recommends documenting provenance, limitations, human oversight roles and retention practices for AI risk management. It is voluntary, cross-sector guidance; it does not prescribe a self-storage reset workflow. The design implication is narrower: an AI-assisted action record should preserve its sources, versions, limitations and accountable human path rather than presenting generated rationale as proof.

## Safety comes first, but the evidence gap stays visible

Evidence preservation must never delay an emergency protective action required by the governing procedure. If there is smoke, a life-safety alarm, an unsafe electrical condition or another immediate threat, people and the approved emergency response come first.

The architecture still has work to do. It should record:

- the authority used for the override;
- the condition that made delay unacceptable;
- which preservation steps were skipped;
- what state-changing action occurred and when;
- which later conclusions are now limited; and
- who owns the follow-up.

An override is not a bypass that makes the missing evidence disappear. It is a different, visible decision path. The post-incident record should say, in plain language, that the prior state was not captured before action because the protective response took priority.

[NIST SP 800-61 Rev. 3](https://csrc.nist.gov/pubs/sp/800/61/r3/final) frames incident response as part of broader cybersecurity risk management and emphasizes preparation, roles and continuous improvement. It is not a facility emergency plan. Its useful architectural lesson is that response procedures and responsibilities should exist before the stressful moment, then improve through after-action review.

## Preserve the minimum, not the maximum

“Save everything” is not a responsible preservation policy. Facility systems may contain personal data, access events, payment-related references, employee activity, security configuration or vendor-sensitive details. The preservation gate should capture only the fields needed for the defined troubleshooting purpose and only under valid authority.

The system should support field allowlists, masking, role-based access, retention deadlines and deletion or legal-hold rules. It should reject unsupported collection requests and record excluded categories. Hashes can help show that an artifact is unchanged after capture; they do not prove the source was accurate, the capture was complete or the interpretation is correct.

The same limit applies to AI context. The model does not need a raw diagnostic archive in its prompt. A controlled service can extract approved facts, attach provenance and expose only the minimum necessary context. Sensitive artifacts should stay in the governed evidence store, not in durable model memory.

## Bind every artifact to a clock and a version

Troubleshooting often fails because teams compare states without knowing when they were true. An evidence artifact should include the source clock, capture clock, timezone, known clock offset, source version, configuration version and the action ID it precedes.

If distributed traces are available, correlation identifiers can connect a recommendation, preservation request, provider call and readback. They still do not prove physical movement or customer activity. A trace shows recorded computational relationships, subject to instrumentation gaps and sampling.

The record should therefore use four labels:

- **observed before action**;
- **observed after action**;
- **inferred from identified evidence**; and
- **unknown or unresolved**.

Those labels prevent the model from filling a missing pre-action state with a plausible story generated from the post-action result.

## A fictional facility example

Consider this explicitly fictional scenario. Cedar Thread Storage, facility CTS-04, uses a fictional access controller named Gate 2. The systems, data and events below do not describe a real customer, vendor, deployment or product.

At 7:18 p.m., a fictional monitoring service records repeated command failures. An AI assistant proposes `ACTION-FIC-204`: restart the controller service. The action is classified as corrective and potentially evidence-altering. The gate identifies three relevant sources: approved fault fields in the current status view, a short-lived command queue and a persistent event export.

The approved fault fields and persistent export are captured and verified. The queue cannot be preserved through the authorized interface before its stated fictional expiry. There is no safety emergency, so the action remains held and returns to the on-call operator. The operator decides whether to obtain authorized technical support, accept the documented gap under policy or pursue a narrower step.

If the operator later releases the restart, the provider acceptance and post-restart status are recorded separately. A green status after restart may support “service reported healthy at 7:34 p.m.” It does not support “the queue was corrupt” or “the restart fixed the root cause.” Those conclusions remain unresolved unless separate evidence supports them.

## Test the control by trying to make it fail

An observe-before-act control should be tested with deliberate failure cases:

- the preservation service times out while the action service is healthy;
- the artifact exists but its hash or source version is missing;
- the facility identity changes between capture and execution;
- the action parameters change after approval;
- a sensitive field appears outside the allowlist;
- the human authority expires before execution;
- the provider accepts the command but no independent readback arrives;
- an emergency override is invoked without a named policy or follow-up owner; and
- the model tries to describe an unknown pre-action state as observed fact.

The expected behavior is not always “block.” It may be hold, narrow, re-capture, request human review, execute an authorized emergency action or proceed with an explicit inference limit. What matters is that the state transition is governed and auditable.

## The practical rule: observe, preserve, act, read back

The most dangerous troubleshooting sequence is simple: act first, explain later. A responsible AI system should do the reverse when conditions allow.

Observe the current state without overstating what the source proves. Preserve the permitted evidence that the action could change. Act only through current authority. Read back the actual result from an independent source. Then keep the limits visible.

The goal is not to turn every facility issue into a forensic investigation. It is to stop an AI assistant from erasing the basis for its own explanation—and then replacing the missing history with confidence.

<!-- BODY END -->

## Editorial disclosure

This article was prepared with editorial and research assistance. The fictional facility, systems, identifiers, timestamps and events are teaching examples only and do not represent an actual customer, incident, deployment or product capability.

## About the author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.
