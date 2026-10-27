# The AI Joined Three Current Records. They Were Never Current at the Same Time.

*An operations agent can retrieve three accurate facility records and still assemble a false operating picture. Temporal coherence has to be designed, tested and visible before a composite answer can govern action.*

By Jared Mastroianni

<!-- BODY START -->

An AI assistant checks a self-storage facility before recommending whether a delinquent unit should remain overlocked. It reads the property-management system, the access platform and a customer-service case.

Every call succeeds. Every returned record is authentic.

The rental record says the balance is still due. The access platform says the gate credential is disabled. The service case says the customer reported a posted payment. The agent combines the three and tells the operator that the account remains unpaid, access is correctly blocked and the payment report still needs investigation.

There is one problem: those records describe three different moments.

The rental balance was captured before the payment posted. The access state was read during the overnight synchronization delay. The service case was updated after accounting confirmed the receipt. Each record was accurate in its own context. The combined answer was never true at any one time.

This is a temporal-coherence failure. It is easy to miss because the architecture can show green tool calls, legitimate sources and recent timestamps. The failure appears only when we ask a stricter question: **What facility state was this answer intended to represent, and were all material facts valid for that same boundary?**

## “Current” is not a timestamp

Operations systems use several kinds of time, and they should not be collapsed into one `updated_at` field.

- **Effective time:** when the represented business state began or ended. A payment may be effective as of a transaction time even if another system learns about it later.
- **Observation time:** when a person, sensor or source system observed the condition.
- **Record time:** when the source stored or changed the record.
- **Event time:** when an emitted event says the occurrence happened.
- **Retrieval time:** when the agent received the record.
- **Decision time:** the boundary the composite answer is supposed to represent.

Retrieval time is often the easiest to capture and the least useful by itself. Three systems queried at 10:05 may return records that became effective at 09:41, 09:58 and 10:04—or records whose effective times are unknown. Calling all three “current at 10:05” converts transport success into a claim about business state.

RFC 3339 defines a consistent Internet timestamp representation.[^1] That helps systems exchange unambiguous instants. It does not establish what a timestamp means, whether the source clock is reliable, whether a record was late, or whether two facts are eligible to be joined. Format is necessary plumbing, not temporal governance.

## Choose the as-of question before collecting facts

The agent needs an explicit **as-of boundary** for every composite operational answer. That boundary may be:

- the latest coherent state all required sources can support;
- the state at a named incident or customer interaction time;
- the state at a reporting cutoff; or
- the live state, but only when each source satisfies a defined freshness and effective-time rule.

Do not let the agent choose the boundary silently after seeing the data. That invites it to mix whatever records are available and write a fluent explanation around the gaps.

The request should define the target subject, action or decision, facility identity, required sources, as-of policy and maximum tolerated uncertainty. The answer should carry the chosen boundary forward. If a source cannot represent that boundary, the agent should say so.

This is especially important in self-storage because operational states often change in sequence across different systems. A rental may become active before a gate grant appears. A transfer may close in the property system while a former entitlement remains. A work order may show a technician note before the verified condition is resolved. A payment may post before a collection workflow releases its next step.

The most recent record from each system is not necessarily a coherent facility state.

## Give every fact a validity envelope

Before a fact can enter the agent’s reasoning context, wrap it in a small evidence envelope. At minimum, record:

- facility and subject identity;
- source system and source record ID;
- fact type and value;
- effective-from and effective-through times, when the source supports them;
- observation, event and record times, with meanings kept distinct;
- retrieval time;
- source version, sequence or revision identifier;
- correction or supersession relationship;
- allowed freshness at the intended use;
- time uncertainty and clock source, when material;
- authoritative-source status for this fact; and
- the strongest available readback.

Do not invent missing effective times from record time. If a source only tells you when its row changed, store that as record time and keep effective time unknown.

The W3C PROV-O recommendation provides concepts such as generation and invalidation times that can bound the existence of an entity.[^2] It does not prescribe a self-storage state model, but it reinforces a useful principle: a fact’s provenance includes when it came into existence and when it ceased to be usable, not merely which document contains it.

## Test the join, not just the ingredients

The composite answer should pass a temporal join gate. A practical gate asks four questions.

### Identity

Do all facts resolve to the same governed facility, account, unit, work item or entitlement? Similar names, shared phone numbers and vendor aliases are not enough.

### Validity

Was each fact effective at the chosen as-of boundary, or does the system have an approved rule for using an observation as a bounded proxy? A recently retrieved fact can still be historically invalid. An older record may be the correct record for a historical boundary.

### Completeness

Are all required sources represented? If one source is late or unreachable, the agent should not quietly answer from the remaining subset unless that reduced evidence set is explicitly permitted for the use.

### Order

Do versions, source sequences and event relationships form a possible history? A payment confirmation should not be evaluated against a balance snapshot taken before that payment while being described as a post-payment balance.

CloudEvents defines `time` as the timestamp of when an occurrence happened, while allowing a consistent alternate time when occurrence time cannot be determined.[^3] It also defines event identity through `source` and `id`. Those attributes help preserve occurrence and delivery evidence. They do not guarantee cross-system ordering, clock agreement or a coherent business snapshot. The operator still needs source-specific semantics and join rules.

## A database snapshot does not freeze the portfolio

Inside one database, transaction isolation can provide a consistent view. PostgreSQL documentation explains that multiversion concurrency control lets a statement see a database snapshot rather than inconsistent partial updates, and that repeatable-read behavior can keep a stable view within a transaction.[^4]

That is valuable—and easy to overgeneralize.

An agent reading a property-management database, an access vendor API and a case-management platform is not automatically inside one transaction. A snapshot identifier from one system does not freeze the others. Even if all three systems use strong internal consistency, their replication delays, event pipelines, effective-time models and query moments can differ.

The architecture therefore needs either a shared governed event/history layer capable of answering the same as-of boundary, or an explicit reconciliation method that proves the selected records are mutually eligible. “All APIs returned 200” is not that proof.

## Separate freshness from coherence

Freshness asks how old a record is relative to a requirement. Coherence asks whether the selected records can describe one possible operating state.

The two are related but not interchangeable.

Three records retrieved within five seconds can be incoherent if one source lags by twenty minutes. Three records created hours apart can be coherent for a historical cutoff if each was valid at that cutoff.

Set freshness rules by fact and use, not by application. Gate access, delinquency state, payment state and a maintenance observation may require different tolerances. A dashboard summary may tolerate more delay than an action that changes access or communicates with a customer.

NIST’s AI Risk Management Framework calls for target application scope and human-oversight processes to be defined and documented, and for systems to be tested before deployment and regularly in operation.[^5] It does not prescribe the temporal envelope in this article. Its lifecycle approach supports the operating discipline: define the use, measure the failure mode and route unresolved risk to accountable people.

## Preserve a truthful failure state

When the join gate fails, the agent needs more than a generic error.

Use explicit outcomes:

- **coherent:** required facts support the same as-of boundary;
- **coherent with bounded lag:** an approved rule permits the known delay and its consequence;
- **partial:** required sources are missing;
- **temporally conflicting:** facts cannot describe one valid state;
- **time semantics unknown:** timestamps exist but their meanings are not governed;
- **identity conflict:** records may refer to different subjects; or
- **human review required:** consequence or uncertainty exceeds automated authority.

The answer should name the failed source or rule, the last coherent boundary available, the consequence of using stale or conflicting data, and the owner of the next decision. It should not smooth disagreement into a single confident sentence.

## A fictional Maple Quay example

The following facility, people, systems, identifiers, timestamps and results are fictional.

At fictional Maple Quay Self Storage, an AI assistant prepares a recommendation at 10:05:30 Eastern time for fictional unit MQ-214.

The property system returns balance record `PMS-881`: $186 due, effective at 09:55, retrieved at 10:05:04. The payment system returns receipt `PAY-1442`: $186 posted at 10:01, recorded at 10:02 and retrieved at 10:05:09. The access system returns `ACS-771`: overlock active, observed at 09:58, retrieved at 10:05:13. A customer-service case contains a fictional accounting note recorded at 10:04 stating that the receipt matched the account.

All records are recent. They are not one current state.

The agent’s policy requires payment and balance evidence valid at the decision boundary, plus an access readback no older than two minutes for an access-changing recommendation. The 09:55 balance predates the payment. The 09:58 access observation is outside the approved interval. The agent classifies the join as `temporally_conflicting`, holds the recommendation and requests a post-payment balance readback plus a fresh access-state query.

At 10:06:20, the fictional property system returns zero due with a revision tied to `PAY-1442`. At 10:06:27, the access system still reports the overlock active. The agent can now present a coherent 10:06:27 state and route the access release to the authorized workflow. It does not claim that the earlier evidence was false; it explains that those facts belonged to different times.

This scenario is a design example, not a deployment or performance claim.

## Use the AI Temporal Coherence and As-Of Integrity Test

The accompanying test makes the architecture inspectable. Run it for one composite answer or action at a time.

First, name the decision boundary, governed identities, required sources and per-fact freshness rules. Then capture every fact’s effective, observation, event, record and retrieval times without substituting one for another.

Next, test three cases:

### Fast retrieval, stale source

All tools respond quickly, but one source returns a record outside the allowed effective or observation interval.

### Late event, correct historical fact

A source records an event after the cutoff even though the event was effective before it. Confirm whether the policy uses effective time, record time or both.

### Impossible composite

Provide individually valid facts whose versions or validity intervals cannot overlap. Confirm that the agent refuses to summarize them as one state.

A pass requires more than visible timestamps. The system must preserve their meanings, apply the approved join rule, expose the selected as-of boundary, identify missing or conflicting evidence and hand back cases that exceed automated authority.

## Make time part of the claim

An operations agent should not say “the facility is in this state” when its evidence only supports “these systems returned these records at these retrieval times.”

Bind every composite answer to a governed subject and an explicit as-of boundary. Preserve each fact’s validity envelope. Test cross-system joins for identity, validity, completeness and order. Keep freshness separate from coherence. When the evidence cannot describe one possible state, say so and stop the action path.

The goal is not perfect simultaneity. It is an answer whose time boundary is honest, whose ingredients were eligible for that boundary and whose limitations remain visible to the operator who must decide what happens next.

<!-- BODY END -->

## Sources

[^1]: IETF, [RFC 3339: Date and Time on the Internet—Timestamps](https://datatracker.ietf.org/doc/html/rfc3339), accessed October 27, 2026.
[^2]: W3C, [PROV-O: The PROV Ontology](https://www.w3.org/TR/prov-o/), W3C Recommendation, accessed October 27, 2026.
[^3]: CloudEvents, [CloudEvents Specification v1.0.2](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md), accessed October 27, 2026.
[^4]: PostgreSQL Global Development Group, [PostgreSQL 18: Concurrency Control](https://www.postgresql.org/docs/18/mvcc.html), accessed October 27, 2026.
[^5]: NIST, [Artificial Intelligence Risk Management Framework 1.0 Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), accessed October 27, 2026.

## Disclosure

This article was prepared with AI assistance under Jared Mastroianni’s editorial direction. Maple Quay Self Storage and all related people, systems, identifiers, timestamps, records and outcomes are fictional and illustrative.
