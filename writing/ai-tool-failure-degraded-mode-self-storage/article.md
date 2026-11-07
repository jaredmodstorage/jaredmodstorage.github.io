---
title: "The AI Lost One Tool. Why Did the Workflow Still Say Complete?"
description: "A self-storage AI workflow needs an explicit runtime capability contract, a lower action ceiling when a required tool fails, and a handback that tells an operator exactly what remains unresolved."
author: "Jared Mastroianni"
date: 2026-10-29
historical_slot: "2026-10-28 evening AI architecture"
slug: "ai-tool-failure-degraded-mode-self-storage"
canonical_url: "https://jaredmodstorage.github.io/writing/ai-tool-failure-degraded-mode-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
featured_image: "056-ai-development-smart-access-control-pilot.png"
featured_image_alt: "Three self-storage professionals review a keypad-controlled gate during a smart-access pilot."
featured_image_caption: "A tool can be online while a workflow is incomplete. Runtime controls have to test every required capability before an AI-assisted action is released. AI-generated editorial image."
---

# The AI Lost One Tool. Why Did the Workflow Still Say Complete?

An AI workflow rarely fails as cleanly as a power switch. One tool works. Another times out. A third returns yesterday's snapshot. The model still has enough context to write a confident answer, and the orchestration layer still has enough green checks to display “complete.”

That is one of the most dangerous failure shapes in an operating system: not a total outage, but a plausible partial success.

In self-storage, a customer-access workflow may depend on several different facts. Is the account eligible for access? Is the credential active? Is the facility open for the applicable access window? Is there a documented exception or hold? Those facts may live in different systems. If the gate tool responds but the authoritative account-status tool does not, the workflow does not have most of the answer. It has the wrong answer shape.

The control I want is simple to state: **a workflow may not claim completion when a required capability was unavailable at runtime.** It must lower its action ceiling, preserve the receipts it did obtain, and hand the unresolved decision to the right person.

That rule is more useful than a generic instruction to “keep a human in the loop.” It tells us when the human is needed, what the system is allowed to do before handback, and what evidence should travel with the exception.

## A successful call is not a completed decision

Operators should separate four states that software often collapses:

1. **Transport success:** the request reached a service and received a response.
2. **Tool completion:** the tool performed the requested operation within its declared scope.
3. **Workflow completion:** every required capability contributed an acceptable result.
4. **Business-state verification:** the real facility or account state was read back after any consequential action.

A `200` response can prove transport success without proving tool completion. A tool can complete while returning only the first page of records. Every tool can return successfully while the workflow is still missing a required policy check. And an action can be accepted by an API without proving that the customer credential, ledger, message, or work order changed as intended.

This distinction fits the [NIST AI Risk Management Framework](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf), which treats validity, reliability, monitoring, accountability, and documented roles as continuing parts of risk management. It also fits the [NIST Generative AI Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), which emphasizes monitoring, incident response, change management, and defined human oversight. Those documents are voluntary, cross-sector guidance—not self-storage operating rules—but the architecture lesson is direct: a system needs evidence about how it behaved, not merely an answer it produced.

## Give the workflow a runtime capability contract

Most AI workflow diagrams show tools as permanent boxes. Production tools are not permanent. Their permissions change. A schema adds a field. A credential expires. A site mapping points to the wrong facility. A source is available but stale. A vendor endpoint returns an incomplete page without an error.

Before a run begins, the orchestrator should assemble a capability contract for that specific run. At minimum, it should record:

- the tool and operation identifier;
- tool version and expected schema;
- organization and facility binding;
- permission scope;
- whether the capability is required or optional;
- freshness and coverage requirements;
- accepted success and failure states;
- the permitted degraded mode;
- the maximum action allowed in that mode; and
- the human owner of a handback.

Treat that contract as a short-lived lease, not permanent configuration. Invalidate it when a tool version, schema, identity binding, permission, policy, model, or facility context changes. Then rerun the preflight instead of carrying yesterday's green check into today's decision.

This is where conventional access control and contingency thinking help. [NIST Special Publication 800-53 Release 5.2.0](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) is a federal information-system control catalog, not a mandate for storage operators. Still, its control families around access, audit, contingency planning, monitoring, and recovery offer a useful design analogy: authority, evidence, fallback behavior, and recovery should be specified before the incident.

## Name failure states precisely

“Tool error” is too broad to govern an operating action. A runtime receipt should distinguish at least these states:

- `not_invoked`: the workflow never attempted the required call;
- `rejected`: identity, permission, policy, or request validation blocked it;
- `timed_out`: no acceptable result arrived within the decision window;
- `partial`: the result covered less than the required population or fields;
- `stale`: the result was older than the workflow's freshness limit;
- `empty_valid`: the authoritative source completed and validly returned no records;
- `completed`: the tool met its declared operation, scope, and freshness contract; and
- `completed_unverified`: the tool accepted a change, but required business-state readback is still missing.

Those distinctions prevent two common mistakes. First, an empty result cannot be treated as a timeout. Second, a timeout cannot be treated as evidence that nothing exists.

Retries also need boundaries. Retry a transient transport failure within a defined limit. Do not retry a permission rejection as if persistence will create authority. Do not replay a consequential write unless the operation has an idempotency control or the current target state has been read first. And when a tool recovers, recompute the decision from current authoritative inputs; do not simply resume the sentence the model was writing before the outage.

Telemetry should preserve these states in a trace that links the workflow, tool receipt, facility identity, decision, action, and readback. The [OpenTelemetry guidance on recording errors](https://opentelemetry.io/docs/specs/semconv/general/recording-errors/) supports consistent error classification at the operation level. Its semantic-convention page is marked “Development,” and telemetry standards do not determine whether a storage decision is operationally complete. A green span is evidence about a software operation, not proof that a customer should receive access.

## Lower the action ceiling instead of improvising

The worst degraded mode is silent substitution. A required account-status tool fails, so the model uses a cached summary, an earlier conversation, or general policy language and continues. The output may sound reasonable because the substitute is semantically related. It is still not the required authority.

Each failure state should map to an explicit action ceiling. For example:

| Runtime condition | Maximum safe workflow behavior | Prohibited behavior |
| --- | --- | --- |
| Required source current and complete | Prepare the governed action; execute only within assigned authority | Expanding scope beyond the approved operation |
| Optional source unavailable | Continue only in the declared degraded mode with visible limitation | Hiding the missing input |
| Required source stale, partial, rejected, or timed out | Preserve evidence, create handback, and stop at draft or diagnostic support | Customer-facing decision, access change, charge, refund, lockout, or irreversible work order |
| Consequential write accepted but not read back | Mark `completed_unverified` and hold closure | Reporting the business state as changed |
| Facility or account identity conflict | Stop the run and require identity resolution | Guessing the intended target |

The system may still be useful while action is restricted. It can summarize the evidence it received, identify the missing capability, draft operator questions, or assemble a diagnostic packet. It cannot promote assistance into authority simply because the operator is busy.

## A fictional access example

Consider **Moraine Gate Storage**, a fictional facility used only to show the control. No real customer, deployment, vendor result, or performance claim is described.

An AI-assisted access-support workflow receives a call about a tenant who cannot enter. Its runtime contract requires four capabilities: current account eligibility, gate-credential status, the facility's applicable access window, and the approved exception policy.

The credential tool reports that the code is active. The facility-hours source is current. The policy source loads. The account-status tool times out.

The wrong workflow says: “The credential is active, so access should work,” then sends troubleshooting instructions or changes the credential.

The governed workflow records three successful receipts and one `timed_out` required capability. Its action ceiling drops to diagnostic support. It may tell the operator that the credential service reports an active code and that account eligibility is unresolved. It may prepare a handback with the tenant and facility identifiers, timestamps, source ages, trace ID, attempted operation, successful receipts, missing capability, prohibited actions, and the next authorized check. It may not infer eligibility, change access, or tell the customer that access is approved.

When the account tool returns, the workflow must read the current account state and recompute. Recovery does not retroactively make the earlier run complete.

## Make the handback small enough to use

A handback should not be a raw trace dump. The operator needs a compact decision packet:

- **What was requested?** State the customer or facility outcome in plain language.
- **What is known?** List authoritative receipts with source, scope, and time.
- **What is missing or conflicting?** Name the required capability and exact failure state.
- **What did the system not do?** State the held actions explicitly.
- **What can the operator do next?** Provide the authorized read, call, inspection, or escalation.
- **What evidence closes the handback?** Identify the required readback or supervisor decision.

Assign the handback to a role, not “operations.” Give it a due time based on consequence. A customer waiting at a gate needs a different response window than a portfolio-analysis job. If the owner changes, transfer the packet and record acceptance; do not leave the exception in an unowned queue.

## Test the failure shape before launch

A demo in which every tool answers does not test the architecture. Before release, inject the failures the workflow will eventually encounter:

- required-tool timeout;
- expired permission;
- wrong facility binding;
- partial pagination;
- stale cached result;
- schema mismatch;
- valid empty result;
- duplicate retry;
- write accepted without readback; and
- tool recovery after handback.

For each test, verify the declared action ceiling, visible limitation, prohibited-action hold, owner assignment, and recomputation behavior. The most important metric is not how often the model finishes a response. Track how often a run lacked a required capability, how often it entered degraded mode, how long handbacks remained open, whether recovered runs were recomputed, and whether any silent substitution occurred. The acceptable target for silent substitution is zero.

## Completion should mean what the operator thinks it means

An operator reading “complete” reasonably believes the required work was done. If the platform means “the model stopped generating tokens” or “the orchestration graph reached its final node,” the label is misleading.

Responsible AI architecture is often described through principles. Operators need state definitions. A required tool was available or it was not. Its result met freshness and coverage requirements or it did not. The workflow had authority to act or it handed back. A consequential change was read back or it remained unverified.

That discipline does not make an AI system timid. It makes the system dependable under the conditions that matter most: when production is only partly working and the output still sounds completely sure.

---

## Practical operator tool

Use the accompanying **AI Runtime Capability and Degraded-Mode Release Matrix** before enabling or changing an AI-assisted workflow. The package includes a blank CSV and an explicitly fictional completed example.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Disclosure

This article was developed with AI-assisted research and editorial support under human direction and review. The architecture, examples, and operating recommendations remain the author's responsibility. The Moraine Gate Storage scenario and all data in its completed tool are explicitly fictional.
