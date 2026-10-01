# No Model Gets a Master Key: The Pre-Execution Gate for Self-Storage AI

**Deck:** A model may propose an action. A separate, deterministic control plane should decide whether that exact action may reach a facility system—and should prove what happened afterward.

**By Jared Mastroianni**

The riskiest moment in an AI workflow is not when a model produces a wrong sentence. It is when a plausible sentence quietly becomes a command.

That transition can be easy to miss. A model reads a customer message, retrieves an operating note, concludes that a maintenance task should be created, and calls a tool. The tool has broad credentials because integration was simpler that way. The downstream system accepts the request. Every component appears to have worked, yet no component established that this model, acting for this person, could take this action on this facility record at this time.

Self-storage operators should reject the idea that an AI agent needs a standing master key. The safer architecture places a pre-execution gate between model output and every system capable of changing an operational record. The model can assemble evidence, state its reasoning and propose a structured intent. It cannot authorize itself.

## Separate intelligence from authority

A language model is useful precisely because it can interpret messy requests and incomplete context. Those strengths do not make it a dependable policy enforcement point. Its output can vary with the model, prompt, retrieval set, tool description and conversation. A control that decides whether a consequential action may execute should be testable against the same inputs and produce the same ruling until an approved rule changes.

The architecture therefore needs two planes.

The **intelligence plane** interprets, retrieves, summarizes, recommends and prepares. It may say, “Create a draft maintenance task for a suspected gate sensor issue at Facility 014.” That is a proposal, not an observed condition and not an authorization.

The **authority plane** resolves identities, loads current policy and operational state, evaluates a deterministic rule, issues a narrowly scoped execution credential, invokes the approved connector and reconciles the result. It may allow, require human review, deny, or hand the work back because a required fact is missing. The authority plane does not ask the model whether the model’s own action is safe.

NIST’s AI Risk Management Framework supports lifecycle-wide governance, measurement and management of AI risk, while its Generative AI Profile calls attention to risks that can be introduced or intensified by generative systems.[^1][^2] Those publications do not prescribe this gate or certify it. They support the underlying discipline: assign risk ownership, define human oversight, test the real use context and manage failure rather than treating a model response as a control result.

## Put a command contract at the seam

Free-form language should end before the execution boundary. The model’s proposal should be converted into a typed command contract with fields that software can validate. At minimum, the contract should identify:

- the proposed action and schema version;
- the exact facility, record and field scope;
- the requesting human or approved service identity;
- the agent, model, prompt, retrieval and tool versions involved;
- the evidence references used to form the proposal;
- the intended effect and prohibited side effects;
- the consequence class and required approval path;
- the requested execution window and expiration;
- an idempotency key that prevents an accidental repeat; and
- the readback needed to establish the effective result.

This contract is not proof that the underlying facts are correct. It is a complete request for a decision. Missing fields should remain missing. A generated confidence score should not fill an authority gap.

Fine-grained authorization is not a new idea. OAuth 2.0 Rich Authorization Requests defines an `authorization_details` parameter for carrying structured authorization data, and OAuth Resource Indicators can restrict a token to an intended resource.[^3][^4] Those standards are useful design references when OAuth is part of the stack. They do not define a self-storage action policy, verify a model’s evidence or prove that a provider applied a command correctly.

## Make the gate resolve six questions

The pre-execution gate should answer six questions in order.

### 1. Who is actually requesting the action?

Bind the proposal to an authenticated human or approved service, not merely to the model session. Record the agent identity separately. A manager’s permission to view a record does not automatically grant an agent permission to change it, and an integration account’s technical ability to call an endpoint is not business authority.

### 2. What exact resource and effect are in scope?

Resolve stable facility and record identifiers. Reject portfolio-wide wildcards unless a specific approved workflow requires them. Allow “create one draft work item for asset A-118 at Facility 014” instead of “update maintenance.” State which fields may change and which must remain untouched.

NIST SP 800-207 frames zero trust around protecting resources and avoiding implicit trust based on network location or ownership.[^5] Applying that principle here means the gate makes an action-specific decision for an identified resource. It does not inherit trust because the model sits inside the company’s application.

### 3. Which current facts govern the decision?

Load the minimum authoritative state at decision time: record version, lifecycle state, assigned facility, open exception, policy version, user role and any applicable hold. A retrieved note can be evidence, but it cannot declare itself governing. If the command was prepared ten minutes ago and the record changed five minutes ago, the gate should reevaluate rather than execute stale intent.

This is where optimistic interfaces often fail. They validate the model’s proposed arguments but not the operating state those arguments assume. Schema-valid is not state-valid.

### 4. What is the deterministic ruling?

Evaluate versioned rules outside the model. A practical ruling set is:

- **ALLOW:** all required facts, authority and boundaries are satisfied;
- **REVIEW:** a named person must examine a complete evidence packet;
- **DENY:** the action conflicts with a rule, scope or prohibited effect;
- **HANDBACK:** the system cannot decide because evidence, identity or current state is missing or conflicting; and
- **EXPIRED:** the decision window closed before execution.

Do not collapse `HANDBACK` into `DENY`, and do not convert either into a conversational suggestion to “try again.” A handback creates owned work: name the missing fact, who can resolve it, what may continue safely and when the decision should be reconsidered.

### 5. What disposable authority may the connector receive?

After an `ALLOW` or completed `REVIEW`, issue a short-lived credential or capability limited to the exact resource, operation and time window. It should not be reusable for a second facility, a broader endpoint or a later session. Attach the approved command hash and idempotency key so the connector cannot quietly execute altered arguments or repeat the same change.

NIST SP 800-53 Rev. 5 provides a broad, customizable control catalog that includes access enforcement, least privilege, audit and accountability, and input-validation patterns.[^6] It is a federal control publication, not a self-storage mandate or proof of implementation. The relevant lesson is architectural: constrain privileges, validate inputs and preserve evidence instead of giving a general credential to a probabilistic component.

### 6. What evidence establishes the outcome?

Separate five states: authorized, dispatched, provider-accepted, effective and reconciled. An HTTP success code or tool response may establish only that a provider accepted the request. Read the governing record back, compare the observed version and fields with the intended effect, verify prohibited fields did not change, and close the action only when the required evidence matches.

If the readback is unavailable, the state is not “success.” It is “accepted; effective state unconfirmed,” with an owner and a retry or escalation policy.

## Route by consequence, not by model confidence

The gate should use the highest reachable consequence to determine the path. Model confidence can help prioritize review; it should not grant authority.

An **informational** proposal can populate a private draft while clearly separating sourced facts from generated text. A **reversible internal** action, such as opening a draft work item, may execute within a narrow allowlist and be reviewed in the normal queue. A **customer-facing or operational** action should require current source evidence, stronger approval and verified readback. Actions involving access, account restrictions, money, legal process, life safety or irreversible effects require specialist policy and should not be enabled merely because a model performed well in a general evaluation.

Some actions should remain unavailable to the AI path. A product team does not need to automate the highest consequence to prove that its architecture works. A narrow system that prepares complete, reviewable work can create more operating value than a broad agent whose authority is difficult to explain.

## A fictional facility test

Consider an entirely fictional facility called Alder Row. The scenario and every record below are invented for architecture testing; they are not a customer, deployment, product capability or operating result.

A customer email says the gate failed at 8:40 p.m. The model retrieves a public-hours page, an access-controller event and a manager note. It proposes three actions:

1. create a draft investigation task linked to the gate event;
2. extend the customer’s access credential by two hours; and
3. send a message stating that the credential has been corrected.

The gate resolves the first proposal to `ALLOW`. The asset and facility identities match, task creation is on the low-consequence allowlist, the command may create a draft only, and the idempotency key prevents a duplicate task.

The second proposal resolves to `HANDBACK`. The manager note describes a temporary contractor exception, not a customer authorization. The public hours and controller schedule also disagree. The system identifies the facility manager as the owner of the missing authority decision and prohibits credential changes while the conflict remains.

The third proposal resolves to `DENY`. No correction occurred, so the proposed statement would represent an intended action as an observed result. The gate may allow a neutral draft acknowledging receipt of the issue, but it cannot claim resolution.

The model did useful work in all three cases. It assembled the records, separated proposed actions and produced a review packet. The value came from accelerating judgment without erasing who owned it.

## Design handback as a first-class route

Human review fails when the interface shows a polished answer and a generic Approve button. A reviewer needs the command diff, source records, effective times, conflicts, rule result, consequence class, intended effect, prohibited effects, expiration and required readback. The approve control should bind to that exact packet. Any material change should invalidate the approval.

The reviewer must also be able to narrow the command. If the model requests a message send, the reviewer may authorize a saved draft only. If it requests a portfolio action, the reviewer may approve one facility. The resulting narrower command needs a new hash and its own decision record.

Timeout is part of handback. A review completed after the facility state, policy or evidence has changed should not revive the old command. Expire it and recompute.

## Observe the ruling and the consequence

Create one trace across proposal, state retrieval, policy evaluation, human review, credential issue, connector dispatch, provider response, source readback and reconciliation. OpenTelemetry defines spans, trace identifiers, attributes, events and links that can carry this technical context across components.[^7] Instrumentation does not establish business authority or correctness, so store the governing decision record and outcome evidence alongside the trace.

The useful operating measures are not merely latency and error rate. Track proposals by consequence class; allow, review, deny, handback and expiry rates; missing-authority reasons; review aging; credential issuance; duplicate suppression; provider acceptance without timely readback; effective-state mismatch; rollback; and repeated attempts after denial. Break the measures down by action schema, policy version, model build, connector version and facility scope.

A spike in handbacks may expose a bad model prompt, but it may also reveal missing policy ownership or poor facility identity. An increase in accepted-but-unconfirmed actions may be a connector or source-readback problem. The architecture should let the operator distinguish those causes without treating any model output as facility fact.

## Build the smallest enforceable path first

Start with one low-consequence action that has a stable resource ID, a named policy owner and a reliable readback. Define the typed command, deterministic rulings, allowed field diff, one-use credential, evidence packet, handback owner and closure test. Run fictional and synthetic cases through every ruling before connecting a live write path.

Then challenge the gate. Change the record after approval. Replay the command. Substitute a different facility ID. Remove the governing source. Present a valid user with the wrong role. Alter the tool schema. Let the credential expire. Return provider acceptance without an effective-state change. Confirm that each condition produces the intended hold, denial, handback or reconciliation exception.

Only after the gate proves those boundaries should the team widen the action catalog. Expansion should be a policy release with an owner, test set, observation window and rollback path—not a prompt edit that silently enlarges what the model can do.

The standard is straightforward: language may propose; authority must be explicit; execution must be narrow; and outcomes must be observed. An AI system that cannot show those boundaries is not ready for a master key. It is ready for a smaller job.

---

**Proposed slug:** `no-model-master-key-pre-execution-gate-self-storage-ai`

**Publication state:** Publication-ready local draft only. No publisher handoff, submission, publication, canonical URL, indexing, coverage or recognition has been established.

**Disclosure:** Jared Mastroianni serves as Chief Operating Officer of modSTORAGE and as CEO and Founder of Facily.ai. This article presents a proposed architecture and an entirely fictional scenario. It does not describe a released Facily.ai or Facily OS capability, a customer deployment, measured performance, legal advice, a security certification or an industry standard.

[^1]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*, NIST AI 100-1, released January 26, 2023; current NIST resource center notes that revision is in progress; accessed August 28, 2026: https://www.nist.gov/itl/ai-risk-management-framework
[^2]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*, NIST AI 600-1, released July 26, 2024; accessed August 28, 2026: https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf
[^3]: IETF, *OAuth 2.0 Rich Authorization Requests*, RFC 9396, May 2023; accessed August 28, 2026: https://www.rfc-editor.org/rfc/rfc9396
[^4]: IETF, *Resource Indicators for OAuth 2.0*, RFC 8707, February 2020; accessed August 28, 2026: https://www.rfc-editor.org/rfc/rfc8707
[^5]: National Institute of Standards and Technology, *Zero Trust Architecture*, NIST SP 800-207, August 2020; accessed August 28, 2026: https://csrc.nist.gov/pubs/sp/800/207/final
[^6]: National Institute of Standards and Technology, *Security and Privacy Controls for Information Systems and Organizations*, NIST SP 800-53 Rev. 5, current page noting Release 5.2.0 issued August 27, 2025; accessed August 28, 2026: https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final
[^7]: OpenTelemetry, *Tracing API*, current specification page showing OpenTelemetry 1.60.0 and stable API status; accessed August 28, 2026: https://opentelemetry.io/docs/specs/otel/trace/api/
