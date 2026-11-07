---
title: "The AI Marked It ‘Closed.’ Which Kind of Closed Did It Mean?"
author: "Jared Mastroianni"
historical_slot: "2026-10-29 evening AI architecture"
slug: "ai-semantic-state-collision-self-storage"
canonical: "https://jaredmodstorage.github.io/writing/ai-semantic-state-collision-self-storage/"
destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
description: "A practical architecture for preventing one overloaded status word from turning into an unsafe self-storage operating decision."
featured_image: "assets/054-ai-development-computer-vision-pilot-inspection.png"
featured_image_alt: "Three colleagues review a camera and operating workflow during an AI governance discussion."
---

# The AI Marked It “Closed.” Which Kind of Closed Did It Mean?

An AI assistant is asked a simple question: “Is the gate closed?”

It finds four records. The gate contact says `closed`. The office-hours record says `closed`. A gate repair work order says `closed`. An incident case tied to the same entrance says `closed`.

All four statements may be accurate. Only one describes the physical position of the gate leaf. None, by itself, answers the question the operator probably cares about: Can an authorized customer enter the property safely right now?

That distinction is where responsible AI architecture becomes operational work. A model can read every available record correctly and still produce the wrong answer because the word *closed* is carrying several unrelated meanings. The failure is not necessarily hallucination. It may be a semantic collision: the same label is being used for different subjects, different state types, different authorities, and different consequences.

In self-storage, that is not a language problem we can solve with a better prompt. It is a data-contract and decision-authority problem.

## A status word is not an operating state

Operational software often presents short labels because people need to scan quickly: open, closed, active, inactive, complete, blocked, released. Those labels work inside a familiar screen because the surrounding context supplies the missing meaning. A manager looking at a work-order queue knows that *closed* means the administrative record is no longer active. A person standing at the keypad may use *closed* to mean the gate leaf is across the lane. The same person, looking at the office schedule, means the office is outside staffed hours.

AI systems flatten those contexts when they retrieve and combine records. If the architecture passes the model a bag of labels, the model is forced to reconstruct meaning from nearby text, naming conventions, and probabilities. That may be acceptable for summarization. It is a poor basis for releasing an operational action.

The safer unit is not `status = closed`. It is a typed statement:

> At 6:42 p.m., gate contact G-02 reported the physical leaf position as closed, according to controller C-17, under source version 8841. This observation does not establish access availability, controller health, customer authorization, lane clearance, or operating release.

That statement is longer because the system had always been relying on hidden context. The architecture’s job is to make the context explicit before the AI is allowed to use the state.

## Define the subject before the state

Every operational state needs a subject. “Closed” should be impossible to store or exchange without saying what is closed.

For a gate episode, the relevant subjects might include:

- the physical gate leaf;
- the access controller;
- the customer-access schedule;
- a particular customer credential;
- the vehicle lane;
- the office-hours schedule;
- the repair work order; and
- the incident case.

These subjects are related, but they are not interchangeable. A closed repair work order does not prove the gate is physically closed. A closed gate leaf does not prove the controller is healthy. A healthy controller does not prove a particular credential is authorized. An open access schedule does not prove the lane is clear.

The first architecture rule is therefore simple: bind every state to a canonical `subject_type` and `subject_id` before it enters an AI retrieval layer. If a source cannot identify the subject, the record may still be displayed for human review, but it should not be promoted into an action-bearing fact.

## Give each state its own namespace

The second rule is to stop treating familiar words as universal codes. A namespace makes the domain part of the value:

| Ambiguous label | Typed state example | What it means |
|---|---|---|
| `closed` | `gate_leaf.position = closed` | The contact reports the physical leaf at its closed position. |
| `closed` | `office.service_window = closed` | The office is outside the staffed service interval. |
| `closed` | `work_order.lifecycle = closed` | The maintenance record reached its administrative terminal state. |
| `closed` | `incident_case.lifecycle = closed` | The incident review was administratively concluded. |
| `closed` | `facility.access_availability = closed` | The operating authority has disabled customer entry. |

The words remain readable, but the state type does the real work. It constrains which transitions are valid, which source has authority, and which consequences may follow.

This is also where schema validation helps. The official [JSON Schema Draft 2020-12 validation vocabulary](https://json-schema.org/draft/2020-12/json-schema-validation) defines structural controls including `type`, `enum`, `const`, and `required`. Those controls can reject a state record that lacks a subject, uses an unapproved value, or omits a required authority field. The limitation matters: schema validation can prove that a document has the expected shape. It cannot prove that the sensor is truthful, the source is current, the operator had authority, or the proposed action is safe.

## Separate observation, assertion, inference, and proposal

A semantic contract also needs to say what kind of statement it contains. I use four classes:

1. **Observation:** a source reports a condition, such as a contact sensor reporting the gate leaf closed.
2. **Assertion:** an authorized person or system declares an operating state, such as the manager placing customer access on hold.
3. **Inference:** a system derives a conclusion from other records, such as inferring that the office is likely unstaffed from a schedule and time zone.
4. **Proposal:** an AI recommends an action or a new state, such as proposing that access remain disabled pending inspection.

The classes must never silently collapse. An inference is not an observation. A proposal is not authorization. An administrative status is not a physical condition.

The [NIST AI Risk Management Framework 1.0](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-1.pdf) calls for risk management throughout the AI lifecycle and organizes work around governing, mapping, measuring, and managing risk. It also treats context, human oversight, and interpretation of AI output as part of that work. The framework is voluntary and general; it does not prescribe a self-storage state model. The operator still has to define the subjects, authority classes, decision boundaries, and handback rules that make those principles real at the facility.

## Preserve the event envelope, not just the latest value

A typed state can still become unsafe if its origin and timing disappear. Every state transition should retain at least:

- event ID;
- source system and source record ID;
- subject type and ID;
- state namespace and canonical value;
- observation, assertion, inference, or proposal class;
- observed time and effective time;
- source version and superseded record;
- authority class;
- valid-until time, when applicable; and
- expected operational consequence.

The [CloudEvents 1.0.2 specification](https://github.com/cloudevents/spec/blob/v1.0.2/cloudevents/spec.md) provides a useful, vendor-neutral event envelope with attributes such as `id`, `source`, `type`, `subject`, and `time`. It is a transport and interoperability specification, not a self-storage business ontology. It does not decide whether a state is true, which actor may authorize access, or whether delivery was exactly once. Its value here is narrower: an operational event should arrive with enough identity and provenance to be interpreted and traced.

Do not overwrite `gate_leaf.position = open` with `closed` and retain only the latest row. Append the transition. Link it to the prior version. Preserve the event that caused the change. If a correction is required, record the correction as another event rather than rewriting history. The AI should be able to explain which evidence it used and which later event superseded it.

## Make impossible transitions visible

A typed state model should define allowed transitions. A work order may move from open to assigned to in progress to completed to closed. A gate leaf may move from open to moving-closed to closed. An access-availability state may move from enabled to restricted to disabled, but only under defined authority.

Those transition graphs prevent a source label from jumping across domains. They also expose contradictions. If the access controller reports the gate leaf as both open and closed under the same version and effective interval, the architecture should not ask the model to pick the more plausible value. It should create a semantic-collision exception.

The exception needs an owner, a deadline, and an action boundary. Until the conflict is resolved, the AI may summarize the competing records and identify the missing evidence. It must not convert uncertainty into facility fact.

## Join the facts required by the operating question

“Is the gate closed?” is usually an incomplete question. The system should identify the intended decision before selecting evidence.

If the operator is checking the physical leaf position, the gate-contact observation may be enough to answer—with source and timestamp attached. If the operator is asking whether a customer can enter, the decision requires a join across several subjects:

- Is the customer-access schedule open for this facility and time zone?
- Is the controller online and processing current rules?
- Is the credential authorized and not on hold?
- Is the gate lane released from maintenance or incident control?
- Is the physical device in an operable state?
- Has an authorized person imposed a temporary restriction?

No single `closed` label answers that set. The result should be a decision object with its own evidence list, preconditions, authority requirement, and expiration. If any required input is ambiguous, stale, missing, or contradicted, the correct output is a handback—not a guess.

## A fictional collision at Granite Reed Storage

The following scenario and every record in it are fictional. They do not describe a customer, deployment, facility, product, or measured result.

At 6:45 p.m., an AI assistant at fictional Granite Reed Storage is asked whether customers can use the main gate. Retrieval returns four current-looking records:

- `gate_leaf.position = closed`, observed by contact G-02 at 6:42 p.m.;
- `office.service_window = closed`, effective at 6:00 p.m.;
- `work_order.lifecycle = closed`, set by a maintenance coordinator at 4:18 p.m.; and
- `incident_case.lifecycle = closed`, set by a regional reviewer at 5:07 p.m.

An untyped system might summarize: “The gate is closed, the repair is complete, and the incident is resolved.” Every clause sounds reasonable. The conclusion is still unsafe. The contact says where the leaf is, not whether it can move. The work-order state says the administrative record is closed, not that the operating release was verified. The incident state says the case is closed, not that the lane is available. The office schedule is irrelevant to authorized after-hours access unless policy explicitly makes it a precondition.

The typed system returns a different answer:

> Customer access cannot be determined from the retrieved states. The gate leaf was observed closed at 6:42 p.m. The work order and incident case are administratively closed. No current controller-health readback, lane-release assertion, or access-availability decision was found. Hand back to the on-call operator before representing the gate as available.

That answer is less convenient. It is also honest about what the evidence can support.

## Monitor collisions after deployment

Semantic safety is not finished when the schema ships. Source systems change labels. Vendors add statuses. Teams reuse a familiar word for a new workflow. A mapping that was valid last quarter can become misleading without breaking an API.

[NIST AI 800-4, *Challenges to the Monitoring of Deployed AI Systems*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.800-4.pdf), notes that post-deployment monitoring is needed to assess real-world reliability, track unforeseen outputs and drift, and identify consequences in new or changing contexts. The report also says that monitoring terminology, validated methods, and best practices are still nascent. It is a monitoring landscape and challenges report, not a prescriptive semantic-control standard.

For an operating portfolio, monitor at least five collision signals:

1. a new raw label that has no approved namespace mapping;
2. one raw label mapped to more than one state type without an explicit source rule;
3. contradictory states for the same subject and effective interval;
4. a downstream action based on an inference or proposal as though it were an authorized assertion; and
5. a decision produced without every required precondition and action-time readback.

Track the exceptions by source, facility, state type, action consequence, resolution owner, and age. A rising collision count is not merely a data-quality metric. It is evidence that the operating vocabulary and the actual workflows are drifting apart.

## Use the Semantic State Collision Test before action

The companion tool converts this architecture into a reviewable contract. For every action-bearing state, the operator or system owner must be able to answer:

- What exact subject does this state describe?
- Which namespace gives the label its meaning?
- Is the statement an observation, assertion, inference, or proposal?
- Which source and version produced it?
- When was it observed, when did it become effective, and when does it expire?
- Which transitions are allowed, and who may authorize them?
- What does the state permit the AI to conclude?
- What must the AI never infer from it?
- Which additional states must be joined before action?
- What action-time readback is required?
- Who receives the handback when any answer is missing or conflicting?

The point is not to build a bigger glossary. It is to keep one convenient word from crossing an authority boundary it was never designed to cross.

## The model should not have to guess what operations mean

An AI system can be fluent, careful, and technically correct while still joining the wrong meanings. When that happens, improving the prose of the prompt may make the answer sound better without making the operating decision safer.

The durable fix is architectural: typed subjects, state namespaces, explicit statement classes, append-only transitions, source and time provenance, allowed-transition rules, action preconditions, and human handback. Then the model can do what it is good at—finding, comparing, and explaining information—without being asked to invent the missing operating contract.

At a self-storage facility, *closed* should never be the end of the question. It should be the beginning of a more precise one: What is closed, according to whom, as of when, and what does that state actually authorize us to do?

---

**Practical operator tool:** See `semantic-state-collision-test-and-action-contract.md`, the blank CSV template, and the explicitly fictional Granite Reed Storage example included with this package.

**Author:** Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

**Image disclosure:** The featured image is an AI-generated editorial illustration. It is not documentary evidence of a meeting, facility, deployment, product capability, or result.
