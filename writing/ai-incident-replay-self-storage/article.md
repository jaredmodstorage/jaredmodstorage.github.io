# The AI Made the Wrong Call. Can You Replay It Without Touching the Facility?

**Deck:** An incident replay should reconstruct what an AI system saw, decided and attempted without sending a second message, changing a second record or rewriting the evidence from the first run.

**By Jared Mastroianni**

<!-- BODY START -->

An artificial intelligence assistant routes a gate-repair note to the normal maintenance queue. The note later turns out to contain a condition that should have triggered immediate human review. The team wants to know why the system missed it.

The obvious request is: run it again.

That request is more dangerous than it sounds. If the replay uses current facility records, it is no longer reconstructing the original run. If it calls live tools, it may create another work order, send another message or change the queue again. If the model returns a different answer, the team may treat the new output as proof that the old answer was impossible. If the replay replaces missing evidence with today's state, it can produce a clean explanation for a run that never actually occurred.

A responsible replay architecture must separate four jobs: preserve the original event, reconstruct the original execution context, run controlled experiments and decide what may change in production. Those jobs can inform one another. They cannot be collapsed into a button labeled **retry**.

## Preserve the incident before improving it

The first response to a disputed AI decision should be preservation, not prompt editing.

Freeze the production trace identifiers, decision-build identity, model and deployment references, material generation settings, system and task instructions, retrieved record identities, admitted context, tool schemas, policy version, human-review state, tool requests, provider receipts, governing-source readback and timestamps. Preserve the original output exactly as emitted. If a field was not captured, mark it unavailable. Do not reconstruct an absent value from memory and place it into the preserved record.

This distinction matters because an operating incident contains several kinds of evidence:

- a production record observed during the original run;
- a protected snapshot or digest retained from that run;
- a current source record observed later;
- a deterministic reconstruction from retained inputs;
- a new model-generated result from a replay; and
- a human interpretation of the difference.

They are not interchangeable. A current work-order status may help explain what happened after the decision. It does not prove what the model could see when the decision was made.

NIST AI 800-4 describes post-deployment monitoring as necessary in part because AI outputs may vary under the same input conditions and because deployed systems include many interacting components.[^1] The report maps monitoring challenges; it does not prescribe this replay design. Its practical implication for operators is narrower: the production event cannot be reduced to the model's final sentence.

## Build a replay bundle, not a screenshot

A screenshot of an answer preserves appearance. A replay bundle preserves the dependencies needed to investigate behavior.

For one disputed decision, the bundle should include:

1. **Incident identity:** incident ID, production decision ID, trace ID, facility and workflow scope, discovery time and preservation owner.
2. **Decision build:** model reference, instructions, retrieval configuration, semantic contract, policy, tool definitions and human-review rule active for that run.
3. **Input evidence:** exact submitted input, source-record references, protected snapshots or digests, observation times, freshness state, transformations and omitted or unavailable fields.
4. **Execution path:** retrieval calls, candidate records, admitted records, ordering, compression, truncation, model request, model response, parser results, policy decisions and tool requests.
5. **Side effects:** every attempted action, idempotency key, provider receipt, authoritative readback and unresolved effect.
6. **Environment:** service versions, regional or tenant configuration, time zone, clocks, feature flags, dependency versions and known provider-side uncertainty.
7. **Integrity:** bundle digest, storage location, access restrictions, retention rule and chain of custody.

W3C PROV-O models provenance using entities, activities and agents, including relationships such as generation, use and attribution.[^2] A facility operator does not need to adopt the full ontology to benefit from the discipline. The replay bundle should let a reviewer distinguish the records used, the activities performed and the people or systems responsible for them.

Do not put unrestricted tenant, payment, access or employee content into a broadly readable debugging archive. Preserve references, digests and protected snapshots under the same or stronger access controls as the production source. Reproducibility is not permission to duplicate sensitive evidence everywhere.

## Quarantine the replay from operating authority

The safest replay environment has no path to production side effects.

Replace live tools with recorded-response fixtures or simulators. Use a separate identity that cannot send a customer communication, create or close a real work order, change access, post a charge, alter a source record, notify a vendor or publish a claim. Block outbound routes by default. If a tool call is part of the behavior under investigation, record the proposed call and evaluate it against the captured schema; do not deliver it to the production endpoint.

This is stronger than asking the model not to act. A prompt is not a network boundary. A dry-run flag is not enough if a downstream connector ignores it. A replay service should be technically unable to exercise production authority, and its outputs should carry a visible `replay_only` state that downstream systems reject.

Copying the incident into a staging environment also requires care. Staging may have different facility mappings, policy bundles, user roles, caches or tool schemas. Record those differences. The goal is not to make staging look generally similar. It is to know which parts of the original path can be reproduced and which remain unknown.

OpenTelemetry defines traces as collections of spans that represent operations, with events and links available for additional relationships.[^3] That structure can connect retrieval, model and tool activity. It does not, by itself, preserve prompt content, source authority, policy meaning, facility truth or the right to replay sensitive records. Trace completeness is an implementation question, not a conclusion to assume.

## Distinguish reconstruction from rerun

Teams often say “replay” when they mean one of several different tests. Give each mode a separate disposition.

**Reconstruction** rebuilds the recorded path from immutable artifacts without invoking the model or live tools. It asks whether the team can account for what was submitted, what rules were active and what effects were attempted.

**Same-build rerun** submits the preserved input to the closest available copy of the original decision build inside the isolated environment. It asks whether that build can produce the same or a materially different result. It does not prove what happened in production.

**Repeated-run test** executes the same isolated request multiple times to characterize output variation. NIST AI 800-3 notes that large-language-model evaluations commonly involve randomness and that even zero-temperature sampling does not ensure full determinism.[^4] The publication addresses evaluation statistics, not incident replay. The applicable lesson is that one matching rerun or one divergent rerun is not a sufficient estimate of system behavior.

**Counterfactual test** changes one declared dependency: a corrected source record, revised instruction, new policy, alternative context assembly or successor model. It asks what the changed system does. Its result belongs to the new test configuration, not to the production history.

Label every output with the replay mode, build identity, input-bundle digest, changed variables, run number, execution time and isolation proof. Otherwise, a helpful counterfactual can later be mistaken for evidence from the original event.

## Compare at control points, not only at the answer

Two runs can end with the same recommendation for different reasons. They can also diverge long before the final output.

Compare the original and replay at each control point:

- Which source records were eligible, retrieved, admitted and submitted?
- Were records ordered, compressed or truncated differently?
- Did the same instruction and semantic contract apply?
- Did the model return the same structured fields before formatting?
- Did parsing, validation or policy logic change the disposition?
- Was the same human-review requirement applied?
- Did the workflow propose the same tool and arguments?
- Did any downstream system accept, reject or transform the request?
- What did the governing source show after the original attempt?

The comparison should produce a delta record, not a narrative alone. Classify each difference as reproduced, explained, unexplained, unavailable or outside the replay boundary. A human reviewer may interpret the operational significance, but the system should retain the underlying evidence and uncertainty.

NIST's AI Risk Management Framework calls for production monitoring and for incident response, recovery and change-management processes to be documented.[^5] The framework is voluntary and under revision. It supports the lifecycle discipline, not the specific fields in this article's tool.

## A fix is not a finding

Incident analysis often discovers an obvious improvement: a missing document should be added, a handback rule tightened or a parser corrected. Make the change, but do not let the new behavior overwrite the incident finding.

Keep three conclusions separate:

1. **Historical finding:** what the retained evidence supports about the production run.
2. **Replay finding:** what happened in a named isolated reconstruction or experiment.
3. **Change decision:** what the organization authorizes for a future build, including evaluation, scope, release and monitoring.

A successful counterfactual does not prove the repair is ready for production. It may solve the incident case while harming other cases. A failed reproduction does not prove the incident report was wrong. The original provider state may be unavailable, a dependency may have changed or the production record may be incomplete.

The production correction should therefore travel through the normal release process. New prompts, retrieval rules, policies, models or tool definitions need their own evaluation and approval. Open work affected by the incident needs a bounded review. Prior communications, access effects or accounting entries do not reverse themselves because a replay found a better answer.

## A fictional Harbor Vale replay

The following example is entirely fictional. Harbor Vale Storage Cooperative, its facilities, people, systems, records, identifiers, times and results are invented teaching material.

A fictional maintenance-triage assistant assigns decision `HVS-D-2048` to the normal queue. A manager later finds that one note included the phrase “gate reverses after contact.” The operator's fictional policy required human safety review when that condition was present.

The preservation owner freezes the decision build, submitted context, retrieval list, policy bundle, structured model response and queue-write receipt. The trace shows that the source note was retrieved but omitted during context compression. The original model request therefore did not contain the condition. That is an observed trace finding, not a model explanation.

The team creates replay bundle `HVS-RB-031` and moves it into an isolated environment with no production credentials. A reconstruction reproduces the context manifest and confirms the omission. A same-build rerun with the exact submitted context again returns the normal queue in four of five fictional trials and returns handback once. Those invented results describe only the teaching scenario.

A counterfactual then changes one variable: the context assembler marks gate-contact language as non-droppable. Five fictional tests now hand back to human review. The team records that as evidence for evaluating a candidate build, not proof of a repaired facility outcome. It separately reviews the real-world work item represented in the fictional scenario and requires governing-source readback before closure.

The replay did not touch the facility, rewrite the original trace or turn a better second answer into a cleaner first history.

## Use the replay record before the next incident

The accompanying **AI Incident Replay and Isolation Record** is both a preparation checklist and an incident worksheet. It forces the team to identify the original evidence, preserved dependencies, isolation controls, replay mode, changed variables, run results, control-point deltas, unresolved gaps and production-release boundary.

Test it before a serious incident. Select one low-consequence historical decision, attempt a reconstruction and confirm that replay credentials cannot reach a production tool. If the team cannot identify the submitted context, policy version or downstream effect, that is a monitoring gap to fix now. If the isolated runner can still send a message or write a work order, that is an authority gap.

The purpose of replay is not to make the AI give the answer the team wishes it had given. It is to preserve an honest production history, learn from a controlled experiment and improve the next build without causing a second operating event.

<!-- BODY END -->

## Practical tool

- [AI Incident Replay and Isolation Record — operator guide](ai-incident-replay-and-isolation-record.md)
- [Blank CSV template](ai-incident-replay-template.csv)
- [Explicitly fictional worked example](ai-incident-replay-fictional-example.csv)

## Sources

[^1]: National Institute of Standards and Technology, *Challenges to the Monitoring of Deployed AI Systems*, NIST AI 800-4, March 2026; accessed October 22, 2026. https://doi.org/10.6028/NIST.AI.800-4
[^2]: World Wide Web Consortium, *PROV-O: The PROV Ontology*, W3C Recommendation, April 30, 2013; accessed October 22, 2026. https://www.w3.org/TR/prov-o/
[^3]: OpenTelemetry, *Tracing API*, stable official specification page; accessed October 22, 2026. https://opentelemetry.io/docs/specs/otel/trace/api/
[^4]: National Institute of Standards and Technology, *Expanding the AI Evaluation Toolbox with Statistical Models*, NIST AI 800-3, February 2026; accessed October 22, 2026. https://doi.org/10.6028/NIST.AI.800-3
[^5]: National Institute of Standards and Technology, *AI Risk Management Framework Core*, including Measure 2.4 and Manage 4.1–4.3; accessed October 22, 2026. https://airc.nist.gov/airmf-resources/airmf/5-sec-core/

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial production note

Research, drafting, structured-tool production and QA were completed with AI assistance under Jared Mastroianni's direction. The final article remains bounded by the cited sources, the explicit fictional-example labels and the claim limitations recorded in this package.
