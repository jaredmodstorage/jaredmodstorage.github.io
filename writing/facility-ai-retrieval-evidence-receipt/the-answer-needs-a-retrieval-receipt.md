# The Answer Needs a Retrieval Receipt: Prove What Facility AI Was Allowed to Know

**By Jared Mastroianni**<br>
Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai

<!-- BODY START -->

A facility assistant can cite three documents and still answer from the wrong evidence.

The maintenance guide may belong to another property. The access procedure may have been superseded. A regional note may be visible to the software but outside the employee's authority. A summary may omit the one page that changes the decision. The answer can sound careful, quote real text and remain unsafe to use.

This is the gap between retrieval and authority.

Retrieval-augmented generation pairs a generative model with a separate information-retrieval system or knowledge base.[^1] That arrangement can make an answer easier to ground and inspect. It does not prove that the system searched the right facilities, time period, document versions or permission boundary. It also does not prove that the returned passages support the conclusion.

For consequential self-storage work, the answer needs a retrieval receipt: a compact record of what the system was allowed to search, what it actually retrieved, what remained outside coverage and which use the evidence can support.

## A citation proves less than it appears to prove

A visible citation is useful because it gives a reviewer somewhere to look. Its presence alone does not settle four different questions:

1. **Was the source eligible?** A current approved operating procedure has a different standing from an employee's draft, a vendor brochure or an old export.
2. **Was the scope correct?** A policy for Facility A may not govern Facility B. A regional exception may not apply portfolio-wide.
3. **Was the retrieval complete enough?** The system may find a relevant page while missing a controlling addendum, active exception or later revision.
4. **Did the evidence support the claim?** A passage can be related to a question without supporting the answer placed beside it.

Consider a question that appears simple: “Can the gate remain in free-exit mode until the technician arrives?” The assistant retrieves an emergency-access checklist and cites it. The checklist says how to preserve egress during a fault, but a site-specific event plan says who may change gate mode and when. If that second record was excluded, stale or missed, the citation is genuine and the answer is incomplete.

The right response is not to add more confident prose. It is to expose the missing boundary and route the decision to the operating owner.

## Define the retrieval boundary before the question runs

The operating team should decide which sources may speak for a task before tuning search relevance. Start with six boundaries.

**Decision.** Name the exact question and consequence. Summarizing a closed work order is different from recommending an access change, customer message, unit-status update or vendor dispatch.

**Facility and portfolio scope.** List the properties and operating entities whose records are eligible. “All facilities” is not a harmless default when policies, hours, equipment and local authority differ.

**Source classes.** Identify the document types that can govern the answer: approved procedures, current system records, signed vendor instructions, qualified inspections or another defined class. Treat chat transcripts, drafts and informal notes as separate evidence classes rather than quietly mixing them into policy.

**Time scope.** Preserve the effective date, supersession state, retrieval time and freshness limit. A document can be authentic and still be too old for the decision.

**Access scope.** Retrieval should respect the caller's authorized relationship to each resource. The National Institute of Standards and Technology's zero-trust guidance centers protection on resources and calls for authentication and authorization before a session is established; network location or ownership alone does not create implicit trust.[^2] In practice, a search index should not flatten facility, role or sensitivity boundaries merely because all records sit in one technical platform.

**Permitted use.** State whether the evidence may support a summary, comparison, recommendation, draft or proposed action. Retrieval access is not operating authority.

These fields turn a vague instruction such as “answer from our documents” into a reviewable contract.

## Record what was searched, not only what was found

Most answer screens show the top passages. Operators also need the shape of the search.

The receipt should preserve the corpus or index version, query and filter versions, eligible source count, retrieved source count, facilities represented and explicit exclusions. It should also capture the cutoff or top-k rule that limited the result set. These details make three important conditions visible:

- **No hit:** nothing eligible supported the question.
- **Partial coverage:** some relevant evidence appeared, but a required facility, source class, time window or controlling record was absent.
- **Conflict:** eligible sources disagreed and the conflict had not been reconciled.

None of those states should be converted into “normal,” “not applicable” or “no issue found.” Missing evidence is an operating fact.

OWASP's current guidance for large-language-model applications identifies risks around sensitive-information disclosure, data and model poisoning, excessive agency and misinformation.[^3] Its earlier retrieval-specific guidance also described access leakage, cross-context conflict and unverified content in vector and embedding systems.[^4] Those are security and integrity references, not a self-storage standard. They reinforce a practical point: a shared retrieval layer can create new failure paths when content authority and access scope disappear during indexing.

## Separate candidate evidence from governing evidence

Search systems return candidates. The application still needs a release gate.

For every retrieved item, record:

- source identifier and stable location;
- source class and governing owner;
- facility or portfolio scope;
- version, effective date and content hash when available;
- access decision and reason;
- claim or question the passage is meant to support; and
- support state: supports, contradicts, related but insufficient, stale or unresolved.

The support state matters because similarity is not authority. A passage can rank first because it uses the same words while answering a different question. One missing word—“not,” for example—can reverse the meaning without changing most of the vocabulary.

Generative AI adds another boundary. NIST's Generative AI Profile recommends documenting how a model was adapted for its task, including retrieval-augmented processes, data sources and content provenance.[^5] A facility receipt should therefore bind the retrieval result to the model runtime, prompt, policy and output that used it. The model's narrative is not observed facility fact. It is a derived output whose usable scope depends on the evidence packet and the action policy around it.

## Use five release states instead of one green check

A single “grounded” badge hides too much. Use a release state that describes what the evidence can support:

1. **Evidence unavailable.** No eligible source supports the question. Return the gap and owner; do not fill it with general model knowledge.
2. **Evidence incomplete.** Some eligible material was retrieved, but required coverage is missing. A summary may be possible if the limitation is visible; a consequential recommendation remains held.
3. **Evidence conflicted.** Two eligible sources disagree. Preserve both, name the conflict and route reconciliation.
4. **Evidence supports bounded use.** The retrieved set supports the named claim for the declared facility, time and audience. Release only that use.
5. **Human or policy release required.** The evidence is sufficient, but the action or consequence class still requires a named approval.

This approach avoids the false choice between fully autonomous answers and no AI at all. An assistant can remain useful while operating authority narrows to the evidence actually available.

## A fictional five-site example

Harbor Pine Storage is fictional. Every facility, person, system, policy, question, record and outcome in this example was invented for instruction and does not describe modSTORAGE, Facily.ai or a deployment.

The fictional portfolio asks an assistant to prepare a morning summary of gate exceptions across five sites. Four sites use the current portfolio procedure. The fifth has a locally approved construction-period exception that expires Friday.

The index contains the portfolio procedure and yesterday's gate events. The local exception is stored in an approved site binder but was omitted from the latest index build. The assistant retrieves relevant records for all five facilities and cites the portfolio procedure. Search coverage looks complete because every facility appears in the result set.

The retrieval receipt shows otherwise. The task contract requires current portfolio procedures **and** active site exceptions. The corpus manifest lists five eligible site-exception sources, but only four are indexed. The release state becomes `evidence_incomplete`; the fifth site's recommendation is withheld, and the summary states that its local exception record must be reconciled.

The operator does not manufacture a portfolio-wide conclusion. After the approved exception is added and its version verified, the query runs again under a new receipt. The new answer remains a draft until the named regional reviewer releases it.

The example does not demonstrate accuracy, savings or a deployed control. It demonstrates a useful stop: five facilities appeared in search, yet required evidence coverage was only four of five.

## Put the receipt where the action can find it

The companion Facility AI Retrieval Receipt records the boundary, retrieval run, evidence coverage, support decision and release state in one row. It includes a blank template and fictional teaching records for a gate exception, rate explanation, maintenance recommendation and customer-message draft.

Do not turn the receipt into another spreadsheet that nobody can connect to the work. Give it a stable identifier and bind that identifier to the answer, recommendation, approval and any downstream action proposal. If the corpus, filters, source version, model runtime, prompt, policy or question changes materially, issue a new receipt.

Assign ownership across three roles:

- the **source owner** approves which record is current and what it governs;
- the **retrieval owner** proves index, filter and coverage behavior; and
- the **operating owner** decides whether the supported use may be released.

Revalidate after a source is superseded, an access rule changes, a facility enters or leaves the portfolio, a retrieval build changes, a known miss is discovered or a correction affects prior answers. Routine brainstorming and low-consequence writing do not need this full control. Cross-site comparisons, customer-facing drafts, access recommendations, financial explanations and action proposals do.

The most important field is not the model's confidence. It is the evidence state the operator can defend.

An answer should say what it knows. A retrieval receipt shows why it was allowed to know it—and when the right answer is still “not enough evidence.”

<!-- BODY END -->

---

## References

[^1]: National Institute of Standards and Technology, [“retrieval-augmented generation”](https://csrc.nist.gov/glossary/term/retrieval_augmented_generation), Computer Security Resource Center glossary, accessed September 7, 2026.
[^2]: National Institute of Standards and Technology, [*Zero Trust Architecture*](https://csrc.nist.gov/pubs/sp/800/207/final), NIST SP 800-207, August 2020, accessed September 7, 2026.
[^3]: OWASP GenAI Security Project, [*OWASP GenAI LLM Top 10 2026*](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/), August 2026, accessed September 7, 2026.
[^4]: OWASP GenAI Security Project, [“LLM08:2025 Vector and Embedding Weaknesses”](https://genai.owasp.org/llmrisk/llm082025-vector-and-embedding-weaknesses/), accessed September 7, 2026. This remains a retrieval-specific reference; the project identifies its 2026 Top 10 as the current release.
[^5]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), NIST AI 600-1, July 2024, updated April 2026, accessed September 7, 2026.

## Assistance and claim disclosure

AI assistance supported research synthesis, drafting and editorial QA. The retrieval-receipt method, fictional scenario and companion tool are editorial proposals, not evidence of a product feature, deployment, customer result, legal requirement, certification or industry standard.
