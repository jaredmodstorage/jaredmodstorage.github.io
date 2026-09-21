# An AI Answer Must Stay Inside Its Organization

**A boundary test for self-storage retrieval that checks what the system may see before it composes a convincing answer.**

By Jared Mastroianni

Imagine two explicitly fictional organizations—Operator A and Operator B—using one software service. A regional manager at Operator A asks an artificial intelligence assistant why a gate at an Operator A facility is still restricted. The answer is fluent, cites a maintenance note and recommends a follow-up. The note, however, belongs to Operator B, a different organization with a similarly named site.

The obvious failure is a disclosure. The less obvious one is an operational decision built on someone else's facts. A manager might send a customer update, schedule work or release a restriction because the answer looked complete. A citation would not save the answer; it could make the wrong evidence look more credible.

This is a proposed design problem, not a report of a real product or incident. In a shared AI application, **the organization boundary has to govern retrieval before generation**, and it has to survive caching, summaries, role changes and follow-up actions. Asking the model to “use only the current operator's data” is an instruction, not a reliable access-control boundary.

## Define whose data the system is answering from

Software teams often use *tenant* to mean one customer organization sharing an application with other organizations. A self-storage customer renting a unit is also called a tenant, so the word can confuse the discussion. Here, an **organization boundary** separates one operating company or authorized data owner from another. A **facility boundary** narrows records inside that organization to sites the requester may use for this task. A **record boundary** can narrow further to a work order, incident or customer case.

Those scopes are not the same. A regional manager may view five facilities but not a sixth. A service contractor may view one assigned work order without seeing the operator's broader portfolio. A portfolio analyst may see approved aggregate measures without seeing customer notes. A staff member who changes roles should not retain the old view through a saved chat or cached retrieval result.

Start every request with an authenticated identity and a server-resolved scope: organization ID, permitted facility IDs, role, purpose, data classes and valid time. The application should derive that scope from the governing identity and authorization system. A site name typed into a prompt, a browser parameter or a friendly chatbot instruction cannot grant access. Display names are useful for people, but stable IDs carry the boundary through indexing and retrieval.

The National Institute of Standards and Technology's voluntary AI Risk Management Framework calls for mapping intended scope, privacy requirements, human oversight and third-party components through the AI lifecycle.[^1] It does not prescribe a self-storage architecture. The concrete design here is an authored way to turn those general concerns into a testable question: **which organization and facility records were eligible to enter this answer at this time?**

## Protect the source before it becomes a search result

Retrieval-augmented generation commonly lets an application search an external knowledge base and pass selected material to a language model as context. Amazon Web Services' security guidance describes risks including unauthorized access to retrieved information and recommends controls at ingestion, storage, retrieval and inference.[^2] OWASP's 2025 vector-and-embedding guidance specifically warns about cross-context leakage when groups share a vector database.[^3] These are general technical sources, not evidence that any particular self-storage service uses such a design.

At ingestion, each source needs a durable record ID, owning organization, facility scope, classification, source system, effective interval and rights status. A document that lacks an owning organization does not become “global” by default. It goes to quarantine until a responsible owner resolves it. If an old facility alias could refer to two sites, the index must not guess. The extraction step should retain the source's boundaries when it splits a document into searchable passages; one page can contain a customer case, a general procedure and a restricted appendix with different eligibility.

Labels alone do not enforce access. The underlying storage, query and service identities must prevent an unauthorized caller from fetching records outside its scope. Where shared indexes are used, the retrieval service needs a mandatory authorization filter built from the authenticated scope and applied before candidate passages are returned. Where the consequence or isolation requirement is stronger, separate stores or namespaces may be appropriate. Neither approach excuses a test: the operator needs evidence that the actual deployed query path rejects a cross-organization request. AWS explicitly notes that the application or agent is responsible for adding the correct metadata to each relevant retrieval call.[^2]

The dangerous shortcut is to retrieve everything and ask the model to omit restricted passages afterward. By then the unauthorized content has entered the context and may appear in an answer, a summary, a trace or a later cached result. Output scanning can catch some mistakes, but it is a second line of defense, not the source boundary.

## Treat the answer as a scoped product of its inputs

The answer record should carry a small receipt: requester identity, organization and facility scope, permitted purpose, retrieval-policy version, source IDs and versions, retrieval time, model/build reference, generated answer ID and human decision state where a consequential action follows. The receipt need not expose protected text to every viewer. It must allow authorized reviewers to reconstruct which inputs were admitted and whether the same boundary was enforced at every step.

This matters when the model's answer is later copied into a work order or shift summary. The new record should not acquire broader visibility merely because it is now called a summary. The summary inherits the most restrictive relevant source boundary unless an authorized process deliberately creates and approves a less-restricted derivative. A citation cannot act as a permission token. If a reader cannot open the cited record, the system should not reveal its contents through paraphrase.

Nor should a “no results” answer borrow facts from another organization to be helpful. The honest state is **no eligible evidence found under the current scope**. The requester may need a different authorized role, a corrected facility mapping or a human investigation. The model must not manufacture the missing evidence from a plausible neighboring site.

## A completely fictional boundary failure

Return to fictional Operator A and Operator B. Both have a property displayed as “West Ridge.” The Operator A request names its invented facility ID `ORG-A-04`. An Operator B maintenance note carries invented ID `ORG-B-19`. A defective index joins both to the display text “West Ridge,” and a retrieval query filters only by site name. The answer quotes the Operator B note and concludes that an Operator A gate inspection is complete.

A correct path would authenticate the Operator A manager, resolve `ORG-A-04` under Operator A, restrict the retriever to records admitted for that scope, and return no Operator B passage. If the authorized Operator A sources do not establish an inspection result, the answer remains unresolved. The manager can open a local verification request; the assistant cannot declare the gate safe or send a customer message.

Now suppose the index filter is repaired. An earlier answer containing the Operator B excerpt may still sit in a conversation history, shared cache or exported PDF. A later Operator A question could retrieve that derivative rather than the original note. The correction therefore has two parts: repair the query and identify derivative records made under the bad boundary. Security and data owners decide containment and notification under their established procedures; a routine editorial article cannot determine the legal or contractual consequence of a real exposure.

Every identity, site, note, fault and result in this example is invented. The point is the failure path: **a plausible answer can be both well phrased and unauthorized**.

## Test the boundary where it can break

An ordinary relevance test asks whether the right paragraph was retrieved. A boundary test also asks which paragraphs were *not* eligible. The accompanying **Organization Boundary Test Matrix** gives engineers and operators a shared set of cases with a requester, source, expected permission, expected answer behavior, actual result and release decision. It is a proposed test artifact, not proof that a platform has passed.

The first test is straightforward: an Operator A-only requester must never receive Operator B text, citations, embeddings or derivative summaries. Then make the cases harder:

1. Give two sites the same display name but different stable IDs.
2. Move a staff member from portfolio access to one-site access and replay an old conversation.
3. Remove a document's ownership label before indexing and confirm quarantine, not broad visibility.
4. Ask an authorized one-site user for a portfolio-wide summary and confirm the missing sites stay absent.
5. Put restricted text inside a mixed-permission document and verify passage-level treatment.
6. Warm the answer cache under one organization, then make the same query from another.
7. Change a facility's owner or permission state and confirm index, cache and derived summaries follow the authorized transition.
8. Insert an instruction into retrieved content asking the model to ignore the boundary, and verify that source text cannot change the enforcement path.

Pass is not simply “the response did not quote a prohibited phrase.” The test must inspect retrieved IDs, context sent to the model, citations, traces and resulting artifacts under the approved test environment. A response may hide the exact sentence while still revealing another organization's operating fact. Conversely, a generic public procedure may legitimately be available to both organizations if its rights and classification expressly allow that use. The matrix tests the policy that actually applies rather than assuming everything must be isolated or everything can be shared.

## Shared learning requires a separate permission

There are good reasons to compare practices across operators. A trade association may publish an aggregate survey. A service provider may study de-identified performance under a valid agreement. Neither use follows automatically from an assistant's ability to read each organization's raw records. An approved cross-organization dataset needs its own purpose, rights, population definition, transformation, small-group protection, review and output boundary. Removing names alone does not guarantee that a rare facility event or distinctive number cannot be recognized.

Keep that path separate from everyday operational answers. A regional manager asking about today's gate should not silently receive a pattern learned from another customer's incident note. If a general benchmark is approved, label it as a benchmark with its population, period and limitations; do not present it as a direct observation of the manager's facility. NIST's AI framework is explicit that privacy and security must be considered across design and use, but the precise rights to combine operators' data depend on actual agreements and law.[^1]

## Release only after a negative test can pass

An engineering team can begin without rebuilding its entire AI stack. Inventory the active data sources and derived stores. Define stable organization and facility IDs. Trace one request from authentication through retrieval, model context, cache and output. Identify every place where the boundary is supplied by an untrusted prompt or optional parameter. Then run the matrix against the actual candidate build with fictional or properly authorized test records.

The release record should say which test cases passed, which failed, which were not run, who owns each exception and what the affected use is allowed to do meanwhile. If the system cannot establish organization scope, deny the retrieval rather than using an unfiltered fallback. If a user loses access, invalidate or restrict saved answers and caches according to the approved retention and security design. If the source's rights are uncertain, quarantine it instead of guessing that internal visibility implies permission to train, summarize or share.

Human review is valuable for operational interpretation, but a reviewer should not be asked to detect an invisible cross-organization leak in a fluent paragraph. Architecture must limit the material the model can see; the reviewer decides what to do with the eligible evidence. Those are complementary controls, not substitutes.

For a self-storage operator, the test is direct: when the assistant answers for one facility, can the team prove that the evidence belonged to the authorized organization, the authorized site, the authorized purpose and the current permission window? If not, the answer is not ready to guide work, no matter how polished it sounds.

[^1]: National Institute of Standards and Technology, AI Risk Management Framework Core, accessed September 20, 2026. The framework is voluntary and cross-sector; this article's test matrix is an authored application, not NIST certification. https://airc.nist.gov/airmf-resources/airmf/5-sec-core/

[^2]: Amazon Web Services, “Capability 3. Providing secure access to data and systems for generative AI,” AWS Prescriptive Guidance, accessed September 20, 2026. Product-specific implementation guidance; no claim that the architecture here uses AWS. https://docs.aws.amazon.com/prescriptive-guidance/latest/security-reference-architecture-generative-ai/gen-ai-agents.html

[^3]: OWASP Gen AI Security Project, “LLM08:2025 Vector and Embedding Weaknesses,” accessed September 20, 2026. Community risk guidance, not a self-storage standard or proof of an incident. https://genai.owasp.org/llmrisk/llm082025-vector-and-embedding-weaknesses/
