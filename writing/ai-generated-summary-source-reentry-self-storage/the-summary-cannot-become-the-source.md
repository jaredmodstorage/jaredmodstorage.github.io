# The Summary Cannot Become the Source: Stop AI-Generated Facility Text from Feeding Itself

**By Jared Mastroianni**  
Chief Operating Officer of modSTORAGE; CEO and Founder of Facily.ai

<!-- BODY START -->

An AI-generated shift summary can become more persuasive every time a system repeats it—even when nobody has added a new fact.

The first assistant reads a manager note and writes that a gate “appears to be operating normally.” That summary is copied into a work order. The work order is indexed for retrieval. A second assistant cites it in a portfolio brief. The brief is saved to the knowledge base. A third assistant finds two documents that now seem to corroborate the same condition.

There is still only one underlying observation. The other records are descendants of a model’s wording.

This is a recursive evidence problem. AI-generated text leaves the output surface, re-enters the operating corpus, and later returns as apparent support for another answer. The loop can turn cautious language into false consensus, preserve an error after its source is corrected, and make a derived statement look more authoritative merely because it appears in several places.

Self-storage operators need a re-entry control: generated content must carry its origin, derivation and permitted use wherever it travels. A summary may help people find work. It cannot quietly promote itself into observed facility fact.

## Repetition is not corroboration

Independent evidence comes from independently informative sources. Four documents do not provide four-source support when three were copied, summarized or generated from the fourth.

This distinction matters in everyday facility work. A work-order description may be generated from an email. A shift handoff may summarize that work order. A regional report may summarize the handoff. A customer-service assistant may retrieve the regional report when drafting a response. Without lineage, each derivative can look like a separate confirmation.

The architecture should preserve two different counts:

- **document count:** how many artifacts mention the claim; and
- **independent-root count:** how many distinct, eligible observations or governing records support it.

The second count controls the decision. A model should not gain confidence from documents that share the same ancestor.

W3C PROV-O provides a general vocabulary for recording entities, activities, agents and derivation relationships such as `wasGeneratedBy` and `wasDerivedFrom`.[^1] It does not define self-storage evidence rules, but it supplies the right architectural idea: a derived artifact should remain connected to the records and process that produced it.

## Give every record an origin class

Content type is not enough. “PDF,” “ticket,” “email” and “note” describe containers. They do not explain how the statement inside came to exist.

Use an origin class that survives copying and indexing:

1. **Observed:** a bounded human or device observation with an identified observer, time, facility and method.
2. **Governing:** a record authorized to decide a defined field or policy for a defined scope.
3. **Reported:** a person’s claim about an event or condition that has not yet been independently verified.
4. **Derived:** a deterministic transformation, join, calculation or extraction from named inputs.
5. **AI-generated:** text, classification, summary or proposal produced by a named model runtime from recorded inputs.
6. **Human-adjudicated derivative:** generated or derived content reviewed for a specific use by an authorized person.
7. **Unknown origin:** content whose creation path cannot be established.

Human review does not automatically turn a derivative into an observation. A manager can approve a generated incident summary for handoff without personally inspecting the gate. The artifact becomes approved for that handoff, not promoted to “gate verified normal.”

The National Institute of Standards and Technology’s Generative AI Profile treats content provenance, data provenance, information integrity and lifecycle risk management as relevant practices for generative systems.[^2] The profile is voluntary and cross-sectoral. It does not prescribe these seven classes or certify a workflow. Its value here is the discipline of documenting where content came from and how it is used.

## Put a gate in front of re-entry

Every destination that can later inform a model—a document store, work-order system, CRM note, data warehouse, ticket index, vector store, message archive or training set—needs an admission decision.

Use five dispositions:

**Exclude.** Do not admit generated content when it contains sensitive material outside the destination’s access boundary, lacks required provenance, or serves no approved operating purpose.

**Quarantine.** Hold content when origin, source coverage, facility identity, ownership, rights or integrity is unresolved. Quarantine keeps it available for review without allowing retrieval as evidence.

**Admit as derivative.** Store and retrieve the content with a visible generated-content label, parent references, permitted-use boundary and reduced evidence weight. This is the normal state for useful summaries.

**Promote for bounded use.** An authorized person may approve an exact version for a named purpose, audience and expiration. Promotion does not erase the generated origin or grant broader authority.

**Replace with a governing record.** When a person verifies the actual condition or updates the authorized source, create or update the governing record. Link the generated artifact as prior context; do not overwrite its origin history.

The gate should operate on stable identifiers and hashes, not on filenames alone. A summary copied into a ticket body remains the same derivative even if it receives a new title. Near-duplicate detection can help find unlabeled copies, but similarity is a review signal rather than proof of ancestry.

## Carry a provenance envelope with the text

A generated artifact should have a compact envelope that travels with it or can be resolved from a durable ID. At minimum, record:

- artifact ID and content hash;
- origin class and creation time;
- facility, portfolio and decision scope;
- model provider, resolved runtime, prompt and tool versions;
- retrieval receipt or input-set reference;
- parent artifact IDs and independent root IDs;
- source-owner and operating-owner roles;
- permitted and prohibited uses;
- admission disposition, destination and index status;
- review decision, reviewer and expiration when applicable;
- correction, supersession and invalidation links; and
- retention and deletion policy.

A cryptographic hash can establish that the content has not changed since the hash was recorded. It cannot establish that the text is true. C2PA makes the same boundary explicit for content provenance: provenance information can help establish origin and history, but it does not by itself determine factual accuracy.[^3] C2PA is designed for digital content credentials, not facility-system authority; the relevant lesson is to keep authenticity and truth as separate questions.

## Detect loops before retrieval ranks them

The retrieval layer should calculate ancestry before treating multiple hits as support. Build a derivation graph in which nodes are artifacts and edges identify generation, quotation, summarization, revision or deterministic transformation.

For each claim or decision packet, compute:

- the set of independent roots;
- the number of derivative hops from each root;
- whether the current output already appears in the ancestry;
- whether two candidates share a parent or model-generated ancestor;
- whether any parent was corrected, superseded or invalidated; and
- whether a generated artifact is being used outside its approved purpose.

Then apply hard stops. Do not count siblings as corroboration. Do not allow an artifact to support itself through a cycle. Do not release a consequential answer when every supporting path terminates in generated or unknown-origin text. Do not retrieve an invalidated descendant without the correction attached.

The OWASP GenAI LLM Top 10 2026 is a current community security guide, not a self-storage standard or certification.[^4] Its attention to risks such as poisoning and misinformation is relevant because an uncontrolled re-entry path expands the material that can influence later model behavior. The operating control still has to be designed locally around facility identity, data rights, authority and consequence.

## Corrections must travel down the graph

Suppose a manager corrects the original gate note from “operating normally” to “intermittent failure not reproduced.” Editing only the first record is not enough. Every derivative that used the earlier wording may now be stale.

The correction service should identify descendants, assign each one a state and route the affected use:

- **unaffected:** the corrected field was not used;
- **refresh required:** regenerate before reuse;
- **human review required:** the correction may change a prior decision;
- **withdrawn:** the artifact should no longer be available for the approved use; or
- **historical only:** retain for audit with a prominent invalidation link.

Do not silently regenerate a customer-facing draft or completed decision record. Preserve what was originally reviewed, attach the correction, and create a new version. The audit question is not only “What does the summary say now?” It is also “Which version informed the action at that time?”

## A fictional four-facility example

The following teaching case uses the invented Juniper Loop Storage portfolio. Names, locations, people, systems, artifacts, versions, counts and outcomes are fabricated. Nothing in it reports modSTORAGE operations, a Facily.ai capability or any real deployment.

The fictional portfolio asks an assistant for overnight access exceptions across four facilities. At one site, a manager writes: “Customer reported keypad delay; not reproduced during the closing walk.” The assistant produces a shift summary: “Keypad issue reported; closing walk found no reproducible fault.”

That summary is copied into a maintenance ticket. A regional digest summarizes the ticket as “no fault found.” Both are indexed. The next morning, another assistant retrieves the shift summary, ticket and digest. It reports that three records indicate the keypad was operating normally.

The re-entry register changes the decision. All three artifacts trace to one reported observation, and none is a governing access-controller record or an independent onsite test. The independent-root count is one. The digest also strengthened the language from “not reproduced” to “no fault found,” so its use state is `human_review_required`.

The assistant may say: “One customer report was not reproduced during the closing walk; two later summaries derive from that same note.” It may not claim three confirmations or a verified normal condition. The facility owner receives a bounded verification task. No access rule, customer message or incident closure is released from the generated chain.

This example demonstrates the control logic only. It does not establish that the method improves accuracy, reduces incidents, saves time or is available in a product.

## Monitor the loop as an operating system

Post-deployment monitoring should include the content supply chain, not only model latency and error rate. NIST AI 800-4 identifies human-AI feedback loops, fragmented logging and drift detection among continuing monitoring gaps or barriers.[^5] The report maps challenges and open questions; it does not prove that this specific pattern occurs in self-storage or prescribe this register.

Useful measures include:

- generated artifacts admitted by destination and permitted use;
- records with complete parent and independent-root references;
- retrieval results by origin class;
- claimed support count versus independent-root count;
- cycles, orphaned derivatives and unknown-origin items detected;
- invalidated descendants still eligible for retrieval;
- corrections propagated within the required window;
- bounded promotions that expired on time; and
- consequential answers held because only derivative evidence was available.

Training-data feedback is a related but different problem. Primary research published in *Nature* found degradation when generative models were recursively trained on model-generated data under the study’s conditions.[^6] That research concerns model training, not a facility retrieval index, and it does not validate the operational outcomes proposed here. It reinforces one narrower point: preserving access to original data and identifying generated material matter when outputs can become future inputs.

## Start with one re-entry path

Choose one generated artifact that already travels across systems: a shift summary, work-order description, incident recap, customer-message draft or weekly portfolio brief.

Map where it is created, copied, indexed, retrieved and revised. Add origin class, parent IDs, independent roots, permitted use, expiration and correction state. Run four tests: copy the summary under a new title; cite it through two descendants; correct the root; and attempt to use the chain for a higher-consequence decision. The system should preserve ancestry, collapse false corroboration, propagate the correction and hold the unauthorized use.

AI-generated summaries can be operationally useful. They compress work, make patterns visible and prepare a person to decide. The control fails when compression is mistaken for observation.

The rule is simple: generated text may organize evidence, but it cannot manufacture independence. If the summary comes back as a source, its entire family tree must come with it.

<!-- BODY END -->

---

## References

[^1]: World Wide Web Consortium, [*PROV-O: The PROV Ontology*](https://www.w3.org/TR/prov-o/), W3C Recommendation, April 30, 2013; accessed September 8, 2026.
[^2]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence), NIST AI 600-1, July 2024, page updated April 8, 2026; accessed September 8, 2026.
[^3]: Coalition for Content Provenance and Authenticity, [*C2PA Specifications*](https://spec.c2pa.org/specifications/), current specification index showing version 2.4; accessed September 8, 2026. The associated C2PA explainer states that provenance alone cannot establish whether content is true, accurate or factual.
[^4]: OWASP GenAI Security Project, [*OWASP GenAI LLM Top 10 2026*](https://genai.owasp.org/resource/owasp-genai-llm-top-10-2026/), August 3, 2026; accessed September 8, 2026.
[^5]: National Institute of Standards and Technology, [*Challenges to the Monitoring of Deployed AI Systems*](https://www.nist.gov/publications/challenges-monitoring-deployed-ai-systems-center-ai-standards-and-innovation), NIST AI 800-4, March 2026; accessed September 8, 2026.
[^6]: Ilia Shumailov et al., [“AI models collapse when trained on recursively generated data”](https://www.nature.com/articles/s41586-024-07566-y), *Nature* 631, 755–759, version of record July 24, 2024; accessed September 8, 2026.

## Assistance and claim disclosure

AI assistance supported source discovery, research synthesis, drafting and editorial QA. The architecture, origin classes, fictional scenario and companion register are editorial proposals. They are not a released Facily.ai or Facily OS feature, a modSTORAGE deployment, a customer result, a security control implementation, a certification, legal advice or an industry standard.

**Proposed slug:** `ai-generated-summary-source-reentry-self-storage`  
**Publication state:** Publication-ready local draft only. No publisher handoff, repository change, CMS object, submission, schedule, publication, canonical activation, crawling, indexing, coverage or recognition has been established.
