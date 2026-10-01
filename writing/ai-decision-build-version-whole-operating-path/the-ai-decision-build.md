# The AI Decision Build: Version the Whole Operating Path, Not Just the Model

**Deck:** A model name cannot explain why a self-storage recommendation changed. Operators need one releasable manifest for the model, instructions, retrieval set, facility context, policy, tools, review rule, and evaluation evidence that produced the decision.

**By Jared Mastroianni**

Chief Operating Officer, modSTORAGE; CEO and Founder, Facily.ai

<!-- BODY START -->

A self-storage operator can keep the same artificial intelligence model in place and still deploy a materially different decision system.

Change the system instructions. Rebuild the retrieval index. Replace the facility-hours source. Adjust an exception threshold. Add a tool. Rename a status. Shorten the freshness window. Move a human approval from before an action to after it. The model identifier remains unchanged while the operating behavior moves underneath it.

That is why “Which model are we using?” is an incomplete control question. The model is one dependency in a longer operating path. The unit that needs to be versioned, evaluated, approved, observed, and retired is the **AI decision build**: the exact combination of components allowed to produce one class of recommendation for one operating scope.

This is not a software bill of materials with a model name added. It is a decision-specific release record. It connects technical configuration to operating authority. When a regional leader asks why a maintenance case moved into an urgent queue, the answer should identify the complete build that evaluated the case—not merely the provider printed at the top of a settings page.

## The same model can produce a different operating system

Consider a maintenance-triage assistant. Its model summarizes a new work order and recommends a route: normal queue, urgent review, or immediate handback to a person. That apparent simplicity depends on several moving parts:

- the versioned instruction that defines the task;
- the documents and records available for retrieval;
- the facility and equipment identities used to join those records;
- the vocabulary for priority, safety, completion, and uncertainty;
- the rule that converts model output into a queue;
- the tools the workflow may call;
- the evidence shown to the reviewer;
- the role permitted to approve the recommendation; and
- the telemetry and readback used to determine what happened next.

Any one of those can change the result without changing the model.

NIST's AI Risk Management Framework treats risk management as a lifecycle activity spanning the application context, data and input, model, task, and output. Its Govern function calls for AI-system inventories, explicit human-AI roles, and safe decommissioning rather than inventorying a model in isolation.[^1] NIST is revising AI RMF 1.0, so it should be treated as current voluntary guidance under revision, not as a self-storage standard or certification.

The operator consequence is direct: a deployment register organized only by model cannot establish which decision logic was active at a facility on a given date. It also cannot support a clean comparison between the build that passed evaluation and the build that actually ran.

## Give the decision build a stable identity

Every consequential AI-assisted workflow should emit a `decision_build_id`. That identifier resolves to an immutable manifest. The manifest can reference protected artifacts by URI and digest rather than copying customer data, prompts, or proprietary rules into a broad log.

At minimum, the manifest should bind sixteen control areas:

1. **Decision contract.** The exact recommendation or classification the build may produce, its intended user, and prohibited uses.
2. **Consequence class.** Whether an error can affect money, access, customer communication, safety escalation, public facts, employee accountability, or only a reversible internal display.
3. **Scope.** The permitted facilities, entities, workflows, channels, and effective period.
4. **Model dependency.** Provider, model identifier or deployment reference, material settings, and the evidence available for pinning or detecting provider-side change.
5. **Instruction set.** System instructions, prompt templates, examples, output constraints, and their digests.
6. **Retrieval set.** Corpus manifest, document versions, inclusion rules, index or embedding configuration, and cutoff time.
7. **Facility context.** Identity map, source authority, freshness rules, time zone, lifecycle state, and required local facts.
8. **Semantic contract.** Field definitions, state vocabulary, units, null behavior, and compatibility version.
9. **Policy and thresholds.** Eligibility rules, stop conditions, confidence interpretation, and exception routing.
10. **Tool surface.** Available tools, action schemas, permissions, idempotency rules, expiration, and side-effect class.
11. **Human review contract.** Reviewer role, evidence packet, approval point, handback rule, and separation of duties.
12. **Evaluation suite.** Test-set version, adjudication method, scenario coverage, acceptance thresholds, unresolved failures, and approved limitations.
13. **Privacy and logging profile.** Data minimization, restricted fields, content-capture rules, retention, and access.
14. **Release authority.** Named technical, operating, risk, and local approvals required for this consequence class.
15. **Activation and retirement.** Effective time, rollout cell, kill switch, rollback target, revocation trigger, and archive location.
16. **Observation contract.** Trace linkage, outcome states, readback source, correction route, and monitoring owner.

The companion decision-build manifest turns those areas into a release gate. A blank critical field does not mean “document later.” It means the team cannot prove which system it is asking an operator to trust.

## Borrow the build idea without confusing software provenance with decision authority

Software supply-chain practice offers a useful structural analogy. SLSA 1.2 defines build provenance as verifiable information about where, when, and how a software artifact was produced. Its approved build-provenance format separates a build definition, resolved dependencies, run details, builder identity, and output subject.[^2]

An AI decision build can use the same discipline: name the output, freeze the external parameters, resolve dependencies to exact versions, identify the builder, and retain the evidence needed to verify the release. NIST SP 800-218A likewise recommends retaining verification information and provenance for AI models, components, derivatives, frameworks, and pipelines.[^3]

The analogy has a hard boundary. A valid software attestation does not establish that a facility fact was true, a model recommendation was appropriate, a manager had authority, or an action reached the intended real-world state. Build integrity answers whether the approved parts were assembled as claimed. Decision authority and operating truth require separate evidence.

## Hash artifacts; do not dump sensitive content into telemetry

Reproducibility does not require every reviewer to see every underlying record. It requires a stable way to resolve what was used, under the right access controls.

For prompts, policies, schemas, test sets, and corpus manifests, record a version-controlled URI plus a cryptographic digest. For third-party model services that do not expose immutable weights, record the exact service and deployment identifiers available, request parameters, provider release information, evaluation date, and observed change controls. If the provider cannot guarantee a pinned artifact, say so in the manifest and shorten the release window accordingly.

For live facility facts, do not pretend a dynamic record can be frozen by naming its application. Preserve the source record identifier, authoritative field, observation time, effective time, transformation version, and a protected evidence reference. That allows a reviewer to reconstruct what the decision build could see without copying tenant, payment, access, or employee data into an analytics system.

OpenTelemetry's current semantic-conventions line supports common naming across traces, logs, metrics, and events, but its generative-AI conventions have moved to a separate repository and parts of the surrounding configuration remain in development.[^4] That makes OpenTelemetry useful transport vocabulary, not a substitute for a governed manifest. Teams should pin the convention version they adopt and keep sensitive prompt or retrieval content opt-in and restricted.

## Compatibility belongs at the decision boundary

Version numbers become useful only when a change rule says what they mean.

A patch change may fix a display label without affecting the recommendation. A minor change may add a retrieved document type while preserving the decision contract. A major change may alter a threshold, facility population, state meaning, tool permission, or review point. The classification should follow operating consequence, not a developer's sense of code size.

Use three compatibility questions before promotion:

1. Can the new build answer the same operating question for the same population?
2. Can downstream reviewers and tools interpret the output under the same contract?
3. Can the prior evaluation evidence still support the permitted decision?

If any answer is no, the build is decision-incompatible. It needs a new evaluation, approval, and release record even if only one configuration line changed.

This is especially important for human review. A reviewer who previously saw the governing source, conflicting evidence, model rationale, and stop condition may receive a thinner packet after an interface revision. The human role still exists on the organization chart, but the control has changed. The evidence packet and the moment of review therefore belong inside the build version.

## Release one decision build through seven gates

The release path should be short enough to operate and strict enough to investigate.

**Freeze.** Resolve every dependency that can affect the recommendation. Generate the manifest and build digest before evaluation.

**Evaluate.** Run the exact frozen build against the approved suite. Preserve failures, abstentions, reviewer disagreements, and coverage gaps rather than reporting only an aggregate score.

**Authorize.** Obtain the approvals required by consequence class. Technical release authority cannot stand in for operating, privacy, safety, financial, or local authority.

**Shadow.** When appropriate and permitted, run the candidate without granting it action authority. Compare queue effects and handbacks against the approved baseline. Do not convert unexecuted alternatives into claimed outcomes.

**Activate.** Release to a named facility cell, user group, and time window. Emit the `decision_build_id` with every recommendation and derived task.

**Observe.** Monitor the whole decision path: input admission, recommendation, reviewer disposition, tool request, provider acceptance, source readback, exception, and correction. NIST's 2026 report on deployed-AI monitoring identifies fragmented logging, drift detection, human-AI feedback loops, and scaling human monitoring as continuing challenges; it maps the problem rather than prescribing this architecture.[^5]

**Retire.** Remove current-use eligibility, stop new recommendations, preserve historical evidence, identify in-flight work, and verify the successor or handback path. Deleting a model alias is not retirement if cached recommendations and open tasks remain active.

## A fictional two-facility release test

The following scenario and all values are fictional. They do not describe a modSTORAGE or Facily.ai deployment, customer, product capability, or result.

A two-facility test evaluates whether new maintenance notes should enter an urgent human-review queue. Build `ADB-17` uses model deployment `M4`, instruction digest `P12`, retrieval manifest `R8`, semantic contract `S5`, policy `Q3`, and review packet `H2`. It has no authority to dispatch a vendor, change access, message a customer, close work, or change a source record.

The candidate `ADB-18` keeps `M4` but updates the retrieval manifest to `R9`, the policy to `Q4`, and the review packet to `H3`. `R9` includes a revised equipment-criticality table. `Q4` treats missing equipment identity as a handback instead of normal priority. `H3` shows the conflicting identifiers to the reviewer.

Calling both candidates “model M4” would hide every material change. The build manifest makes the comparison honest. Evaluation covers identifier conflicts, stale inspections, missing facility mappings, duplicate notes, and unsupported safety language. The release record shows which cases abstained, which moved queues, which required local review, and which remained ineligible.

If `ADB-18` is activated, every recommendation carries that build ID. If the criticality table is later withdrawn, the operator can find recommendations derived from `R9`, suspend their current-use eligibility, and route open cases for review. The system does not claim that a source correction automatically reversed a human decision or field action.

## Start with one consequential recommendation

Do not begin with an enterprise registry program. Choose one AI-assisted recommendation that can move work, attention, money, access, communication, or accountability. Ask the engineering lead and operating owner to complete the manifest together.

Then select three historical cases that behaved differently and try to reconstruct the exact build behind each one. If the team can name only the model, it has found the control gap. Freeze the remaining dependencies, define the consequence-based version rule, attach the build ID to new recommendations, and require the manifest at the next release review.

The model is not the operating system. The decision build is the smallest configuration an operator can evaluate as a whole—and the smallest one a responsible team should be willing to release.

<!-- BODY END -->

## Author disclosure

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. This article presents an authored operating-architecture method. It is not a product-release statement, deployment report, performance study, legal opinion, or independent standard.

## Endnotes

[^1]: National Institute of Standards and Technology, [Artificial Intelligence Risk Management Framework (AI RMF 1.0)](https://doi.org/10.6028/NIST.AI.100-1), January 2023; current NIST landing page notes that version 1.0 is being revised.
[^2]: Supply-chain Levels for Software Artifacts, [SLSA v1.2 Build Provenance](https://slsa.dev/spec/v1.2/build-provenance), approved specification, accessed August 27, 2026.
[^3]: National Institute of Standards and Technology, [SP 800-218A: Secure Software Development Practices for Generative AI and Dual-Use Foundation Models](https://doi.org/10.6028/NIST.SP.800-218A), July 2024.
[^4]: OpenTelemetry, [Semantic Conventions 1.44.0](https://opentelemetry.io/docs/specs/semconv/) and linked generative-AI semantic-conventions repository, accessed August 27, 2026.
[^5]: National Institute of Standards and Technology, [NIST AI 800-4: Challenges to the Monitoring of Deployed AI Systems](https://doi.org/10.6028/NIST.AI.800-4), March 2026.
