# One Facility, Two Agents: The Command-Arbitration Layer for Self-Storage AI

**Deck:** An AI workflow can be individually well governed and still collide with another workflow acting on the same facility. Responsible architecture needs one place that decides which command, if any, may proceed.

**By Jared Mastroianni**

A maintenance agent proposes a temporary gate restriction so a technician can work safely. At nearly the same moment, a customer-service agent proposes extending access after a weather-related closure. Both workflows have a valid source. Both pass their own approval rules. Both target the same access schedule.

If each workflow can write directly to the operating system, the winner may be whichever request arrives last.

That is not a decision policy. It is a race.

Self-storage operators adding AI-assisted workflows need a command-arbitration layer between approved proposals and consequential facility systems. Its job is not to pick the most confident model. Its job is to prevent independently reasonable automations from producing an incoherent operating state.

The distinction becomes important as one portfolio adds more specialized agents. A maintenance workflow, leasing assistant, access workflow, collections process, messaging agent and reporting process may each have narrow permissions. Narrow permissions reduce risk inside one workflow. They do not resolve two workflows competing for the same resource, acting from different state versions or producing effects that cannot coexist.

## Concurrency becomes an authority problem

Software engineers recognize the technical form of this problem as concurrent modification. Facility operators should recognize the operating form: two sources of work are trying to exercise authority over the same subject at the same time.

The subject may be an access schedule, customer message, work order, refund case, vendor dispatch, rate proposal, unit availability record or public facility fact. A collision does not require identical commands. One workflow may attempt to change the gate schedule while another starts work that requires the gate to remain locked. One may queue a service-restored message while another keeps the incident open. One may propose a refund while another places the account in a different exception state.

Model confidence cannot settle those conflicts. A 94 percent confidence score for one classification and an 89 percent score for another say nothing about which actor has operational authority, which source is current or whether both effects are permitted together. A vote among agents has the same weakness. More proposals do not create decision rights.

NIST’s AI Risk Management Framework places governance, roles, accountability, monitoring and risk response around AI systems.[^1] It is voluntary, cross-sector guidance, is currently being revised and is not a self-storage command protocol. The useful implication here is organizational: conflict policy belongs to the operating system and its accountable owners, not to an improvised conversation among models.

## Keep four objects separate

An arbitration design starts by separating four objects that are often collapsed into one status.

An **observation** reports something received or measured: a work-order update, access alert, customer request or current system value. It may be incomplete or wrong.

A **proposal** is a generated or rules-based recommendation about what should happen. It remains a proposal even when a human has reviewed it.

An **authorized command** is a bounded instruction that has passed the applicable identity, authority, policy, state and conflict gates. Authorization binds to an exact command version and expires.

An **observed effect** is the result read from the source that governs the operating outcome. A provider receipt can show acceptance without proving that the facility state changed as intended.

The arbiter operates between proposal and command. It does not turn an observation into fact, approve its own policy or mark a command complete. It decides whether the exact proposed effect may enter execution now, must wait, has become stale, conflicts with other work or needs a qualified person.

## Put every proposed effect in a command envelope

Free-form agent messages are poor concurrency controls. Before arbitration, every proposed effect should be converted into a typed command envelope. At minimum, the envelope should carry:

- a unique proposal ID and trace ID;
- the proposing actor, workflow and build version;
- the exact facility, account, asset or other resource key;
- the command type, parameters and intended effect;
- the governing source and the state version the proposal relied on;
- the policy version, authority class and approval identity;
- the effective time, expiration and consequence tier;
- an idempotency key and intent hash;
- any resource lease, ownership claim or exclusion window;
- the expected provider receipt, governing readback and reconciliation owner; and
- the conflict class and handback route if execution is denied.

This is deliberately more precise than “Agent A wants to update access.” The resource key should identify the collision domain: for example, facility, gate, access-calendar interval and customer audience. If keys are too broad, unrelated work waits unnecessarily. If they are too narrow, two commands can miss each other even though their effects collide.

CloudEvents provides a standardized event envelope in which `source` plus `id` identifies a distinct event and repeated delivery can retain the same identity.[^2] That helps identify messages. It does not define business authority, command compatibility or exactly-once real-world effects. A command envelope can borrow the discipline of stable identity while adding the facility-specific controls an event format does not supply.

## Reject work built on a stale state

The first arbitration question is not which command came first. It is whether the proposal still describes the resource that exists now.

Record an expected state version when the workflow builds the proposal. Immediately before commitment, compare that version with the governing source. If the access calendar, incident, account or work order changed, the command fails its precondition. The system should not silently refresh the version and preserve the old recommendation. It should return the new state to the proposal stage because the evidence, policy result or human approval may no longer apply.

HTTP’s `If-Match` precondition illustrates this control. RFC 9110 explains that a state-changing request can be conditioned on a current entity tag to prevent accidental overwrites when multiple actors operate in parallel.[^3] An entity tag is not a facility-control design, and many operating systems do not expose one. The broader pattern still holds: compare the approved version with the current governing version, and reject the write when they differ.

“Last write wins” can be acceptable for an inconsequential display preference. It is a weak default for access, money, customer communication, vendor work or a state that drives other automation. In those paths, a lost update can also erase evidence that another owner was already acting.

## Coordinate who may act without confusing a lease with authority

Some collision domains need temporary exclusive control. A workflow may acquire a short lease on a resource key before it prepares or executes a change. The lease names the holder, purpose, acquisition time, renewal time and expiration. It prevents two workers from believing they are the active executor.

Kubernetes uses Lease objects for coordination, including node heartbeats and leader election, and its documentation describes workloads using leases so one leader performs operations while peers remain inactive.[^4] That is an implementation reference, not evidence that Kubernetes should run a facility workflow. It also exposes an important limitation: a lease coordinates technical ownership; it does not grant business authority.

The arbiter therefore checks both. The actor needs a valid lease where exclusivity is required and a separate authorization that permits the effect. A messaging agent holding the technical lease for a customer-notice resource cannot override an incident owner’s hold merely because it acquired the lock first.

Use an increasing execution epoch or fencing value when a downstream system can retain work from an expired holder. Every accepted command carries the current epoch. A destination that later receives a command from an older epoch rejects it. Without that check, an agent paused by a network delay can wake after its lease expires and still apply stale work.

Lease loss should be treated as a handback condition. The workflow stops issuing effects, records which calls may be in flight and reconciles provider and governing state before another executor resumes.

## Make retries repeat intent, not effects

Distributed workflows retry. A request may succeed while its response is lost, leaving the caller uncertain. Blindly issuing the command again can create a duplicate message, dispatch, charge, credit or schedule change.

An idempotency key gives repeated attempts at the same intended command one stable identity. The arbiter stores the key with an intent hash, command parameters, resource version and first result. A retry with the same key and same intent can receive the prior result or safely continue the original operation. The same key with different parameters is a conflict, not a retry.

The AWS Builders’ Library describes this caller-provided request-identifier pattern, including the need to distinguish duplicate delivery from a new intent and to address late-arriving requests.[^5] The article documents an AWS design approach, not a universal guarantee. For facility operations, idempotency at the API boundary still does not prove that the business effect occurred once. A provider can accept one message request while downstream delivery remains unresolved, or accept one schedule request while the controller retains the old state.

That is why the command record stays open after technical acceptance.

## Resolve conflicts by policy, not model negotiation

The arbiter needs explicit dispositions for at least five collision classes.

**Duplicate intent** means the same authorized effect arrived again. Return the existing command state; do not create new work.

**Stale-state conflict** means the governing version changed after proposal or approval. Reject execution and rebuild the proposal from current evidence.

**Incompatible-effect conflict** means two commands cannot safely coexist, such as extending access during an active maintenance restriction. Hold both effects that have not executed and route the decision to the named authority.

**Scope-overlap conflict** means the effects may coexist only after their facility, asset, interval or audience is narrowed. Re-scope through an authorized rule or human decision; do not let an agent invent the boundary.

**Authority conflict** means two valid roles assert different decisions within an overlapping scope. The policy must name precedence, joint approval or escalation. Confidence, arrival time and system seniority are not substitutes.

Some conflicts can be decided mechanically because the policy is precise: an expired proposal is denied, an exact duplicate is suppressed, and a stale version is rejected. Consequential ambiguity should create a decision packet. The packet shows both proposals, governing state, source versions, policies, approvals, in-flight effects, deadlines and the smallest decision a qualified person must make.

NIST SP 800-53 includes separation-of-duties and audit-record controls among a broad catalog of security and privacy controls.[^6] It does not prescribe this arbiter or certify an implementation. The relevant design lesson is to keep proposal, authorization, execution and review responsibilities visible enough to inspect rather than allowing one opaque agent to create and resolve its own conflict.

## A fictional access collision

Harbor Pine Storage is entirely fictional. Every facility, person, record, system, command, event and outcome in this example is invented to test the architecture.

At 1:40 p.m., a fictional maintenance workflow receives a technician’s proposed service window for Gate 2. It generates a command to restrict tenant access from 2:00 to 3:00 p.m. The proposal uses access-calendar version 412, receives the fictional maintenance owner’s approval and acquires lease epoch 88 for the Gate 2 calendar.

At 1:43 p.m., a fictional customer-recovery workflow uses the same calendar version 412 to propose extended access until 10:00 p.m. for customers affected by an earlier closure. Its approval covers customer recovery but not active maintenance windows.

At 1:44 p.m., the maintenance command commits. The access system returns a provider receipt, and a fresh governing readback produces calendar version 413 with the restriction present.

The recovery command reaches the arbiter next. Its expected version is stale, its interval overlaps the active restriction and its authority does not permit overriding maintenance. The arbiter does not compare model scores or allow the second write to replace the first. It rejects the stale precondition, records the incompatible-effect conflict and creates a handback packet for the fictional incident owner.

The incident owner may choose a non-overlapping extension after the service window, keep standard hours or issue a different authorized plan. Whatever the choice, it becomes a new proposal against version 413. The earlier approval cannot be recycled because its evidence and operating context changed.

This scenario does not claim that any real facility uses this architecture or that the controls prevent every failure. It demonstrates the state transitions and evidence an implementation should be able to show.

## Observe the decision path and close on readback

Tracing makes arbitration explainable across services. OpenTelemetry’s trace API defines trace and span identifiers, links and timestamped events that can connect distributed operations.[^7] Those records can link proposals, arbitration decisions, provider calls and readbacks. Telemetry does not enforce authority, prevent a collision or prove a physical result.

The operational trace should record the proposal identity, expected version, current version, resource key, lease epoch, conflict checks, policy result, authorization, idempotency result, execution attempt, provider receipt, governing readback and final reconciliation state. Sampling rules should preserve consequential and conflict traces according to an approved retention policy; an unrecorded conflict is difficult to audit later.

Close the command only when the declared evidence is present. “Authorized,” “sent,” “accepted,” “applied,” “read back” and “reconciled” are separate states. If the provider times out, first determine whether the effect occurred under the existing idempotency key. If readback disagrees with the intended result, stop dependent automation and route recovery. If another command changed the resource after successful execution, record that later transition instead of rewriting history.

## Start with one collision domain

Do not begin by building a universal agent parliament. Choose one consequential resource that two workflows can touch. Map its exact key, governing source, version signal, authorized roles, incompatible effects, lease rule, idempotency contract, expiration, readback and handback owner. Run tests for simultaneous proposals, delayed requests, duplicate delivery, expired leases, stale approvals, partial provider success and a failed readback.

The operator standard is straightforward: one facility state should not be decided independently in two automation lanes. Specialized agents can propose useful work. They can even hold narrow permissions. Before any consequential command executes, one governed arbitration path must establish that the proposal is current, authorized, compatible, singular in intent and observable through reconciliation.

Otherwise, a portfolio has not created coordinated intelligence. It has created faster disagreement.

---

**Proposed slug:** `one-facility-two-agents-command-arbitration-self-storage-ai`

**Publication state:** Publication-ready local draft only. No publisher handoff, submission, publication, canonical URL, search submission, crawling, indexing, coverage or recognition has been established.

**Disclosure:** Jared Mastroianni serves as Chief Operating Officer of modSTORAGE and as CEO and Founder of Facily.ai. This article presents a proposed architecture and an entirely fictional scenario. It does not describe a released Facily.ai or Facily OS capability, a customer deployment, measured performance, legal advice, a security certification or an industry standard.

[^1]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*, NIST AI 100-1, January 2023; current official framework page noting that AI RMF 1.0 is being revised; accessed August 30, 2026: https://www.nist.gov/itl/ai-risk-management-framework
[^2]: Cloud Native Computing Foundation, *CloudEvents Specification*, version 1.0.2; accessed August 30, 2026: https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md
[^3]: Internet Engineering Task Force, *HTTP Semantics*, RFC 9110, June 2022, Sections 9.2.2 and 13.1.1; accessed August 30, 2026: https://www.rfc-editor.org/rfc/rfc9110.html
[^4]: Kubernetes Documentation, *Leases*, current official page; accessed August 30, 2026: https://kubernetes.io/docs/concepts/architecture/leases/
[^5]: Malcolm Featonby, Amazon Web Services, *Making retries safe with idempotent APIs*, Amazon Builders’ Library; accessed August 30, 2026: https://aws.amazon.com/builders-library/making-retries-safe-with-idempotent-APIs/
[^6]: National Institute of Standards and Technology, *Security and Privacy Controls for Information Systems and Organizations*, NIST SP 800-53 Rev. 5, current page for Release 5.2.0; accessed August 30, 2026: https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final
[^7]: OpenTelemetry, *Tracing API*, current specification; accessed August 30, 2026: https://opentelemetry.io/docs/specs/otel/trace/api/
