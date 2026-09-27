# Permission to Observe Is Not Permission to Decide: Purpose-Bound Data for Self-Storage AI

*An AI system can be technically authorized to read a record and still be operationally unauthorized to use it for the decision in front of it. Responsible architecture has to govern purpose, not only access.*

**By Jared Mastroianni**

*Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai*

*Editorial disclosure: Research synthesis, drafting and quality assurance were AI-assisted under human-directed editorial controls. The architecture and every facility, person, system, record and result in the teaching example are fictional. This article is not evidence of a deployed product, customer implementation or operating result.*

<!-- BODY START -->

A self-storage company has a legitimate reason to collect gate-controller health records: determine whether an access system is communicating and route technical exceptions. A regional leader can view those records. An AI assistant serving that leader can retrieve them. Then someone asks the assistant to rank facility managers by operational performance.

The data is available. The identity is valid. The query is easy to run. None of those facts establishes that controller telemetry is an authorized or meaningful input to an employee-performance decision.

That distinction is where many otherwise careful AI architectures become loose. Teams build strong login, role and facility controls, then treat successful retrieval as permission for any analysis the model can produce. The system quietly moves from “this role may see this record” to “this record may support this decision.” Those are different grants.

In self-storage operations, a single workflow may touch access events, payment state, customer messages, call transcripts, work orders, camera-health signals, employee assignments and public facility information. Each source can be appropriate for one purpose and inappropriate, misleading or insufficient for another. A record collected to diagnose equipment should not become a workforce score because it happens to contain an employee name. A message retained to resolve one service case should not become marketing material because a model can summarize it. A payment-status field used to determine a controlled account workflow should not drift into an unrelated customer profile.

The architecture needs a purpose-binding layer between access and inference. Its job is to answer a harder question than “can this actor read the data?” It must decide whether these specific data, transformations, outputs and downstream actions are permitted for this declared operating purpose, under this version of policy, for this period of time.

## Access control answers only the first question

NIST describes attribute-based access control as evaluating attributes of the subject, object, requested operation and, in some cases, the environment against policy.[^1] That is a useful foundation. It can determine that a regional operations role may read a device-health record for facilities in an assigned region.

But a read grant does not, by itself, define every acceptable use after retrieval. The same person may hold several responsibilities. The same table may serve maintenance, security, customer service and reporting. The same AI service may support multiple workflows. If the application sends a broad record set into a general context window and relies on the prompt to remember why each field was collected, purpose has become a suggestion.

NIST SP 800-53 Revision 5 makes the separation explicit for personally identifiable information. Its PT-3 control calls for identifying processing purposes and restricting specified processing to uses compatible with those purposes.[^2] SP 800-53 is a flexible federal control catalog, not a self-storage law or a certification for this proposed architecture. The important engineering lesson is narrower: authority to process data has a purpose dimension that should be documented and enforced.

The final NIST Privacy Framework 1.0 similarly treats data processing as a lifecycle that includes collection, retention, logging, generation, transformation, use, disclosure, sharing, transmission and disposal.[^3] NIST’s Privacy Framework 1.1 remained an Initial Public Draft with the final labeled “coming soon” on the page accessed for this article.[^4] Neither version determines a company’s legal obligations. Together, they reinforce a practical point: governing collection without governing later transformation and use leaves most of the AI path uncontrolled.

## Define the decision before admitting the data

A purpose-bound workflow begins with a decision contract. That contract should be created before retrieval, not inferred after the model produces an answer.

At minimum, bind:

- a stable `purpose_id` and version;
- the exact decision or work product being requested;
- the requesting actor, role and facility scope;
- the people, accounts, assets or events that may be subjects;
- the consequence class and permitted downstream actions;
- approved and prohibited source classes;
- allowed transformations and derived artifacts;
- prohibited inferences and combinations;
- reviewer role, expiration and retention class; and
- the evidence required to enforce and later reconstruct the decision.

“Improve operations” is not a usable purpose. It can be stretched to cover almost anything. “Triage current device-communication exceptions for named facilities and create maintenance-review tasks” is testable. The system can determine whether controller heartbeat data belongs, whether customer balances do not, whether the output may create a technical-review item and whether it may not change access or evaluate an employee.

Purpose is not merely a label attached to the prompt. It has to become an input to deterministic policy. The policy should compare the declared decision contract with data-class rules before a record enters the model’s context.

## Enforce the boundary before retrieval

Filtering after generation is too late. Once a model has received a prohibited field, redacting that field from the visible answer does not undo the exposure or prevent it from influencing the response.

The safer sequence is:

1. authenticate the requesting actor and resolve exact facility scope;
2. load the approved decision contract and purpose version;
3. identify candidate source classes without retrieving unrestricted payloads;
4. evaluate each source against allowed purpose, subject, field, freshness and consequence rules;
5. create a minimum purpose-specific view;
6. pass only admitted fields and governed references into the model; and
7. enforce output and downstream-action limits again before any effect.

This can be implemented with separate purpose-specific indexes, database views, row and column policies, a policy decision point in front of retrieval, or a combination of controls. The product choice matters less than the invariant: the retrieval layer must be able to refuse data even when the user could view it in another authorized workflow.

The result should also preserve why candidate data was excluded. Otherwise an incomplete answer may look comprehensive. A useful evidence packet can say that three approved record classes were queried, one prohibited class was never retrieved and one required source was unavailable. It should not silently substitute an available but incompatible dataset.

## Derived data inherits the boundary

Purpose drift rarely stops at the source record. AI workflows create summaries, embeddings, feature vectors, labels, notes, caches and evaluation examples. Teams often treat those artifacts as new, neutral data because the original fields are no longer obvious.

They are not neutral. A summary of a restricted conversation can carry the same sensitive meaning as the transcript. An embedding can remain linked to its source and be retrieved for a different task. A model-generated label can become a database field that later looks authoritative. A cached answer can outlive the contract that permitted its creation.

Every derived artifact should therefore retain:

- source references and lineage;
- the purpose and policy version under which it was created;
- inherited sensitivity and use restrictions;
- approved audiences and downstream actions;
- an expiration or revalidation trigger; and
- a correction and deletion path appropriate to the governing policy.

The rule is simple: transformation does not expand authority. Aggregation or de-identification may support a newly approved purpose, but the system should record the method, threshold, reviewer and residual limitations rather than declaring that risk disappeared. A human owner must approve the new contract before the derived artifact is admitted to a new decision.

## Govern inferences, not only fields

A field-level allowlist is necessary and insufficient. Seemingly ordinary fields can be combined to infer something the workflow was never authorized to decide.

Suppose a maintenance workflow legitimately receives device ID, facility ID, exception time, assigned technician role and resolution state. A model could still use assignment frequency and resolution intervals to produce an employee ranking. Nothing new was retrieved; the purpose changed inside the inference.

The decision contract should therefore name prohibited inference classes. Examples may include employment evaluation, customer propensity scoring, legal conclusions, safety clearance, fraud findings or eligibility decisions unless a separately governed workflow expressly permits them. The exact list depends on the organization’s policies and applicable requirements; this article does not supply those decisions.

Output schemas help enforce the boundary. A maintenance-triage contract may permit `exception_summary`, `source_reference`, `recommended_review_role` and `task_draft`. It may reject `employee_score`, `customer_risk_label`, `access_change` and `payment_action`. Structured output cannot make an unsupported conclusion safe, but it gives the application an enforcement point stronger than prose instructions alone.

## Treat purpose changes as new requests

A common failure begins with a reasonable follow-up: “Now compare that with…” The user adds customer messages to device records, or asks the assistant to convert a service summary into a marketing list. The conversation feels continuous, so the application reuses the existing context.

Operationally, the decision has changed.

When the requested purpose, subject class, data class, inference or downstream action changes, invalidate the current decision envelope. Create a new request with a new decision ID. Re-run policy. Clear or partition context that is not admitted under the new contract. Do not let conversational continuity become data authority.

This is especially important for agents that plan several steps. A plan may begin with an allowed diagnostic, branch into a communication draft and end with a proposed system change. Each transition needs its own purpose and action admission. The agent should hand back when the next step requires data or authority outside the current envelope.

## Human review cannot manufacture compatibility

Human review is appropriate when policy reserves a bounded judgment for a named role. It is not a cure for an undefined purpose.

A review screen should show the declared purpose, requested decision, candidate data classes, exclusions, prohibited inferences, proposed output and allowed action. The reviewer should answer a specific question: for example, whether an aggregated, minimum-necessary dataset is acceptable for a staffing-capacity analysis under an approved internal policy.

The reviewer should not receive a generic “approve use” button after the system already sent unrestricted records to the model. Nor should the requester be allowed to relabel the purpose until policy returns a permit. If compatibility cannot be established, the correct result is `DENY` or `UNKNOWN`, followed by a named policy or source-owner task. Unknown is not consent, compatibility or low risk.

NIST’s AI Risk Management Framework places governance across the AI lifecycle and calls for roles, responsibilities, policies, monitoring and documentation appropriate to context.[^5] Its Generative AI Profile adds cross-sector risk considerations and suggested actions for generative systems.[^6] Both are voluntary and use-case agnostic. They do not approve a self-storage workflow, define a lawful purpose or validate the control proposed here. They do support treating context, privacy risk and lifecycle governance as operating work rather than a launch-day statement.

## Observe the data that did not enter

Purpose enforcement needs evidence without turning logs into a second uncontrolled dataset.

For each request, record the decision-contract ID, purpose version, candidate source classes, admission result, reason code, excluded-field categories, policy version, model or rule version, output class, enforcement result and downstream readback. Prefer record references, hashes and reason codes over copying sensitive payloads into general logs.

Monitor at least four failure modes:

- a prohibited source class reaches a model context;
- a derived artifact loses its inherited restrictions;
- a purpose change reuses earlier context without reauthorization; or
- a downstream action exceeds the permitted consequence class.

The absence of a prohibited field in the final answer is not proof that the model never received it. Test the retrieval trace. Test the context assembly. Test caches and memory. Test exports, evaluation datasets and support logs. Purpose has to survive the whole path.

## A fictional purpose conflict

The following scenario is entirely fictional. Juniper Vale Storage, its facilities, people, systems, records, policies, times and outcomes do not represent a real company or deployment.

A fictional portfolio uses controller heartbeat and maintenance records to route equipment exceptions. The approved purpose, `PURPOSE-MAINT-TRIAGE-v3`, permits device identifiers, facility identifiers, observation times, technical state, work-item references and assigned operating roles. It prohibits customer data, employee performance scores, access changes and customer communications.

At 9:10 a.m., a regional user asks an assistant to identify unresolved controller exceptions. Policy admits the minimum technical view. The assistant produces a structured list with source references and drafts three maintenance-review tasks. A deterministic action gate confirms that task creation is allowed. Provider acceptance is recorded, then the governing work queue is read back. The result is “three fictional review tasks present,” not “three controller problems resolved.”

The user then asks, “Which facility manager is performing worst based on these records?” The application creates a new decision ID. The requested decision is now employment evaluation. The earlier purpose does not permit that inference, and the maintenance records do not establish a fair performance measure. The policy returns `DENY_INCOMPATIBLE_PURPOSE`. No prior context is reused, no ranking is produced and no employee conclusion is stored.

A later request asks for regional staffing-capacity analysis using aggregated counts with no employee identifiers. That is also a new purpose. It remains held for a data and workforce-policy owner to determine whether the proposed aggregation, fields, thresholds, retention and use are acceptable. The architecture does not treat “less identifiable” as automatically approved.

The important result is not that the assistant refused a difficult question. It is that the system preserved the difference between technical visibility, authorized inference and downstream decision authority.

## The purpose-binding release test

Before an AI workflow can use operating data, an accountable owner should be able to answer twelve questions:

1. What exact decision is this workflow allowed to support?
2. Which stable purpose ID and policy version govern it?
3. Which actors, facilities and subjects are in scope?
4. Which source classes and fields may be retrieved?
5. Which sources or fields are prohibited even if the requester can view them elsewhere?
6. Which transformations and derived artifacts are allowed?
7. Which restrictions follow summaries, embeddings, caches and labels?
8. Which inferences are prohibited?
9. Which output classes and downstream actions are permitted?
10. What event forces a new purpose decision and context reset?
11. What evidence shows what entered the model and what was excluded?
12. Who owns review, expiration, correction, retention and deletion under applicable policy?

If the answer is “the prompt explains it,” the boundary is not ready. Prompts can help models follow instructions. They are not the authoritative control for data admission or operating consequences.

Purpose-bound architecture is a discipline of restraint. Authenticate the actor. Resolve the facility. Declare the decision. Admit only compatible data. Carry restrictions through every derivative. Reauthorize when the purpose changes. Enforce the output and action. Preserve enough evidence to prove the boundary held.

Permission to observe is the beginning of governance. It is not permission to decide.

<!-- BODY END -->

## Practical tool

Use the accompanying **Purpose-Binding Data Admission Register** to evaluate one declared AI decision against source purpose, requested use, data minimization, derived-artifact restrictions, prohibited inferences, review, enforcement and readback. It contains one blank template row and six explicitly fictional teaching rows.

## Sources

[^1]: National Institute of Standards and Technology, [*Guide to Attribute Based Access Control (ABAC) Definition and Considerations*, NIST SP 800-162](https://csrc.nist.gov/pubs/sp/800/162/upd2/final), published January 2014 and updated August 2, 2019; accessed September 12, 2026.
[^2]: National Institute of Standards and Technology, [*Security and Privacy Controls for Information Systems and Organizations*, NIST SP 800-53 Revision 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), final publication with current supplemental release information; accessed September 12, 2026. PT-3 addresses PII processing purposes. The catalog does not determine private-sector legal obligations or certify this architecture.
[^3]: National Institute of Standards and Technology, [*NIST Privacy Framework: A Tool for Improving Privacy through Enterprise Risk Management, Version 1.0*](https://www.nist.gov/privacy-framework/privacy-framework), final Version 1.0 published January 16, 2020; accessed September 12, 2026.
[^4]: National Institute of Standards and Technology, [*Privacy Framework 1.1*](https://www.nist.gov/privacy-framework/new-projects/privacy-framework-version-11), current project page accessed September 12, 2026. The page identifies Version 1.1 as an Initial Public Draft and labels the final release “coming soon.”
[^5]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework (AI RMF 1.0)*](https://www.nist.gov/itl/ai-risk-management-framework), released January 26, 2023; page accessed September 12, 2026. NIST states that AI RMF 1.0 is being revised.
[^6]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile, NIST AI 600-1*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), published July 26, 2024; page updated April 8, 2026 and accessed September 12, 2026.
