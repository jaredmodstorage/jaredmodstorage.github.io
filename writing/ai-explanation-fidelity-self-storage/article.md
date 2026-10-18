# The AI Explained Its Decision. Did the Explanation Come From the Decision Path?

**Deck:** A fluent rationale can help a self-storage operator understand a recommendation—or quietly invent a reason the system never used. Explanation fidelity has to be an architectural control, not a writing preference.

**By Jared Mastroianni**

<!-- BODY_WORD_COUNT_START -->

A facility manager opens an AI-assisted review queue and sees a gate event labeled “possible unauthorized access.” Beneath the label is a confident explanation: the credential failed three times after the facility closed, then succeeded from an unfamiliar vehicle.

The explanation is clear. It is also dangerous if the system did not actually establish those facts.

Perhaps the classifier used only credential status and event time. Perhaps the language model retrieved a stale hours record, confused three log rows from different credentials, or added the vehicle detail from a nearby camera note. The resulting paragraph may sound like the reason for the decision while being only a plausible story written after the decision.

That distinction matters in self-storage. An explanation can influence whether a manager calls a customer, changes access, dispatches a vendor, escalates a safety concern, or dismisses an alert. A human reviewer cannot provide meaningful oversight if the interface gives the reviewer an invented account of what the system considered.

Responsible architecture should therefore treat an explanation as a governed artifact. It must identify the decision it explains, the evidence it is allowed to describe, the process it can faithfully represent, the audience it serves, its limits, and the action authority it does not possess.

## An explanation is not the decision record

Operators often use several different objects as though they were interchangeable:

- the source records available to the system;
- the features or evidence actually used in a computation;
- the model output;
- the policy rule that converts an output into a queue state;
- the generated explanation shown to a person; and
- the human or system action that follows.

They are related, but they are not the same.

The source set may contain facts the model never used. A feature contribution may describe an association without proving cause. A policy may route a score to review even when the model itself produces no prose. A language model may then translate structured reason codes into plain language. Finally, a reviewer may take an action for a different, independently verified reason.

If those layers collapse into one paragraph, the organization loses the ability to answer basic questions. Did the system observe the claim? Did the decision depend on it? Was it added only to make the output understandable? Did a policy rule—not the model—control the result? Did a person verify it before acting?

NIST's *Four Principles of Explainable Artificial Intelligence* separates the existence of an explanation from its meaning, its accuracy to the system's process, and the system's knowledge limits.[^1] The publication is general guidance, not a self-storage standard, but its distinction is operationally useful: a readable explanation is not necessarily a faithful one.

## Build from typed evidence, not free-form recollection

The safest explanation pipeline begins before any sentence is generated. Create a decision receipt containing typed fields that can be tested independently:

1. **Decision identity.** One immutable case ID, facility ID, subject ID, decision type and event time.
2. **Source boundary.** The exact source references, versions, retrieval time and freshness state available to the workflow.
3. **Used-input record.** The fields, features, rules or retrieved passages actually admitted to the decision path—not every item present in the context window.
4. **Output identity.** Model, prompt, policy and explanation-template versions, plus the raw output or stable reference.
5. **Routing result.** The deterministic policy result that turned the output into `display`, `review`, `hold`, `abstain` or another defined state.
6. **Explanation claims.** Each user-visible claim mapped to a source reference, a used-input field, a policy reason code, or an explicit inference label.
7. **Knowledge limits.** Missing, conflicting, stale or out-of-scope evidence and the effect of those limits on the explanation.

This structure prevents a common shortcut: asking a language model to inspect an entire transcript and “explain why.” The model may produce a coherent answer, but coherence does not prove that the answer reflects the actual processing path.

NIST's Generative AI Profile specifically identifies the risk of generated logic or citations that appear to justify an answer and mislead people into inappropriate trust.[^2] That warning does not mean every generated explanation is false. It means the architecture must verify support instead of treating fluency as evidence.

## Separate four kinds of reasons

An operator-facing explanation becomes more honest when it labels the type of reason being presented.

**Observed reason.** A referenced system of record contains the stated value. Example: the credential-status record was `suspended` at the decision time.

**Computed reason.** A deterministic calculation produced a value from named inputs. Example: the event occurred 47 minutes outside the current access schedule. The explanation should preserve the schedule version and timezone rather than merely say “after hours.”

**Model-associated reason.** An attribution or feature-contribution method indicates that an input was associated with the model output. This is not automatically a causal explanation, and it may be unstable or incomplete. The method and model version belong in the technical view.

**Policy reason.** A rule outside the model controlled routing or action eligibility. Example: any suspended credential event is sent to human review, regardless of the model score.

These labels stop a policy rule from being described as machine insight and stop a model association from being described as an observed facility fact. They also help operators decide what to verify. A facility manager may need the observed and policy reasons immediately; a model owner may need the technical attribution later.

## Give each audience the explanation it needs

One explanation cannot serve every person equally well.

A site manager needs a short statement of what was observed, what remains unknown, why the case is in the queue, and what authority the manager has. A regional operator may need the same facts plus the governing policy and any cross-facility exception. A model reviewer needs input versions, reason codes, attribution method, uncertainty and test results. A customer-facing communication needs separately verified facts and approved language; it should not copy an internal model rationale.

The underlying receipt can be shared while each view remains purpose-specific. That is different from generating three independent stories. Every view should resolve back to the same claim IDs and source references.

NIST's AI Risk Management Framework describes explainability and interpretability as connected but distinct characteristics, and its Measure function calls for models to be explained, validated and documented while outputs are interpreted in context.[^3] It does not prescribe a particular interface or certify any explanation method. The practical implication is that “more detail” is not a sufficient design goal. The right question is whether the right person can understand the bounded reason for the output without receiving an unsupported claim.

## Make unsupported claims fail closed

Explanation generation needs an enforcement point after drafting and before display.

Parse the draft into claim units. For each unit, require one allowed support type: direct source reference, deterministic calculation, model-attribution record, policy reason code, or explicitly labeled inference. Reject or rewrite claims with no support. Block causal verbs such as “caused,” “led to,” or “because” unless the governing method can support that claim. Block precise counts, times, locations and identities when they do not reconcile to source records.

The validator should also test contradiction. If the rationale says three denied entries but the admitted records show one denial and two unrelated events, the explanation cannot be released. If facility hours are stale, “outside current hours” should become “the stored schedule indicates the event was outside hours; current schedule not verified.” If evidence is too incomplete to explain the result, the system should say so and route the case appropriately.

An abstention is better than fabricated clarity.

This control should not depend solely on a second language model grading the first. A model can help identify claims, but deterministic checks should reconcile identifiers, counts, timestamps, source citations, reason codes and allowed vocabulary. High-consequence cases should add human review, especially when the explanation may influence access, customer treatment, safety escalation or financial action.

## Preserve the explanation that the reviewer actually saw

Explanations change. A source may be corrected. A prompt may be revised. A policy may receive a clearer label. A model may produce different language on a repeated run.

Do not silently replace the original explanation in the audit record. Preserve its version and hash, the underlying decision receipt, the validation result, the viewer, and the display time. If a correction is necessary, create a linked correction that identifies which claims changed and why. Re-evaluate any pending action that relied on a corrected claim.

This does not require retaining unlimited sensitive content. Store governed references, claim IDs, reason codes, hashes and the minimum text necessary for review under the organization's retention rules. Explanation traceability is not permission to copy customer, access or camera data into a general-purpose log.

## A fictional gate-review example

Consider **Harbor Finch Storage**, a fictional facility used only to demonstrate the control. No real deployment, customer, model, vendor or performance result is described.

An AI-assisted workflow places fictional event `GF-2041` into a manager-review queue. The first generated rationale says: “Three denied attempts occurred after closing, followed by a successful entry from an unrecognized vehicle.”

The explanation validator stops it.

The decision receipt shows one denied attempt for the subject credential. Two other denials belong to different credentials. The current model used credential status and event time; it did not use vehicle recognition. A camera-review note exists, but it says only that a vehicle identifier was unavailable. The hours source is 19 days old and has not been confirmed after a seasonal change.

The released explanation is narrower: “This event was routed for review because the credential was marked suspended and the stored access schedule placed the event outside its permitted window. Current facility hours have not been verified. No vehicle identity was used in the decision.”

The interface shows `policy_reason=suspended_credential_review`, links the credential-status and schedule records, and instructs the manager to verify the live account and access settings before any action. The fictional case remains a review item; no access restriction, customer contact or other outcome is claimed.

The improved explanation is less dramatic. It is also more useful because it tells the manager what is known, what controlled the routing, what remains uncertain and what the system did not decide.

## Use an explanation-fidelity release gate

The companion **AI Explanation Fidelity and Action Boundary Card** turns these principles into a release test. It records the decision receipt, audience, claim inventory, support type, source or reason-code link, fidelity status, knowledge limit, prohibited implication, reviewer, display version, action boundary and correction path. A blank CSV template and an explicitly fictional worked example are included.

Before an explanation reaches an operator, require five outcomes:

1. Every material claim has an allowed support type.
2. The explanation distinguishes observed, computed, model-associated and policy reasons.
3. Missing or conflicting evidence is visible rather than smoothed over.
4. The displayed rationale states what action it does and does not authorize.
5. The exact explanation shown to the reviewer can be reconstructed and corrected.

Evaluate the control with cases that tempt the system to tell a better story than the records support: duplicate events, stale schedules, cross-facility records, missing camera identifiers, conflicting status fields, unsupported causal language, and policy overrides that the model never considered. Measure unsupported-claim rate, contradiction rate, citation resolution, correct reason-type labeling, appropriate abstention, reviewer comprehension and actions taken outside the stated boundary.

Do not optimize only for whether users say the explanation feels helpful. A persuasive rationale can increase confidence while decreasing accuracy. Helpfulness belongs beside fidelity, not above it.

## A trustworthy explanation is allowed to be incomplete

The purpose of explanation is not to make every AI output sound reasonable. It is to give a person a faithful, bounded view of the system's path so that judgment can improve rather than be steered by invented certainty.

In self-storage operations, that means preserving the line between facility evidence, model association, policy routing, generated language and authorized action. When the path cannot support a claim, remove the claim. When evidence conflicts, show the conflict. When the system does not know, let it say so.

The most responsible explanation may be shorter than the one the model wants to write. It should also be the one the operator can safely use.

<!-- BODY_WORD_COUNT_END -->

## Sources

[^1]: P. Jonathon Phillips et al., National Institute of Standards and Technology, *Four Principles of Explainable Artificial Intelligence*, NISTIR 8312, September 2021, checked October 15, 2026. https://doi.org/10.6028/NIST.IR.8312
[^2]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*, NIST AI 600-1, July 2024, checked October 15, 2026. https://doi.org/10.6028/NIST.AI.600-1
[^3]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework (AI RMF 1.0)* and official AI RMF Core resource, January 2023, checked October 15, 2026. https://doi.org/10.6028/NIST.AI.100-1 and https://airc.nist.gov/airmf-resources/airmf/5-sec-core/

## Disclosure

This article was prepared with AI-assisted research and drafting under human editorial direction. The architecture, operator guidance, fictional example, source interpretation and final wording were reviewed for publication under Jared Mastroianni's name. The fictional scenario is not evidence of a modSTORAGE or Facily.ai deployment, product feature, customer result or operating outcome.
