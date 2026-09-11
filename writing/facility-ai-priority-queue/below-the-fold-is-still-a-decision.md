# Below the Fold Is Still a Decision: Audit the AI Priority Queue in Self-Storage

An AI system does not need permission to change a facility record to change what the team works on. Ranking, suppression and screen position already allocate attention.

**By Jared Mastroianni**

<!-- BODY START -->

The safest-looking AI workflow in a self-storage operation may be the one that never writes to a system.

It reads maintenance notes, access events, customer messages and portfolio exceptions. Then it gives a manager a ranked list: the eight items most likely to need attention. The manager still makes every decision. No gate schedule changes. No message sends. No work order closes.

That sounds like a low-authority assistant. It may not be.

If the system decides which eight items appear, it also decides which items start below the first screen, which records wait for another review cycle and which exceptions disappear because they did not satisfy an eligibility rule. The model may have no write permission, yet its ranking can influence response time, staffing attention and the evidence a person sees before acting.

The queue is therefore part of the operating control. It needs a record that explains the full candidate population, not just the items the interface chose to show.

## A recommendation list contains three decisions

Teams often inspect the model score and miss two earlier decisions. A governed priority queue should separate three stages.

The first is **admission**. Which events were eligible to become candidates? A customer message may be excluded because the facility identifier is missing. A camera-health event may be filtered because the site is in a declared maintenance window. A payment exception may be rejected because the data is outside its authorized purpose. These outcomes are not low rankings. They are admission decisions.

The second is **ordering**. Among admitted candidates, what rule assigns a score, priority class or position? The answer may combine a model output with deterministic consequence rules, record age, facility operating mode, open incidents and duplicate detection. Each component needs a version and a defined meaning.

The third is **exposure**. What did a particular reviewer actually have a reasonable chance to see? A candidate ranked ninth in a list that initially displays eight items was not exposed merely because it existed in the response payload. Pagination, filters, screen size, collapsed groups, notification settings and shift handoffs all affect visibility.

NIST's AI Risk Management Framework calls for organizations to document how AI output may be used and overseen, define human oversight and monitor system behavior in production.[^1] The framework is voluntary and currently being revised. It does not prescribe a self-storage queue design. It supports the more basic point that the human-AI configuration includes the interface and operating process around the model—not only the model itself.

## Start with the complete candidate set

The audit record should begin before ranking. Assign an immutable candidate-set identifier to every queue build. Preserve the query scope, source cutoff, facility population, relevant operating mode, admission-policy version and total records considered.

Then give every candidate a disposition:

- **admitted**, with the rule that made it eligible;
- **excluded**, with a typed reason and an appropriate review route;
- **quarantined**, because identity, authorization, source integrity or purpose is unresolved;
- **merged**, with a durable link to the governing duplicate; or
- **not evaluated**, because a required source or service failed.

Do not let `not evaluated` become `excluded`. If the queue builder cannot read the access-event source for one facility, the honest result is an evidence gap. The system did not determine that the facility had no relevant event.

This distinction matters to an operator reading a clean morning queue. Ten displayed items can coexist with two silent sites, thirty unparsed messages and a failed connector. The screen should show the completeness of the candidate build beside the ranked result.

## Make score meaning narrow and explicit

A number such as 0.91 looks precise, but it is incomplete without a definition. Is it an estimated probability, a similarity value, a classifier margin, a severity score, a retrieval score or a normalized blend of several signals? Which population and time period were used to calibrate it? Is a higher number always more urgent?

The queue contract should store the model and feature-set versions, score type, calibration scope and ranking-policy version. It should also preserve deterministic changes made after scoring. If a rule moves an aged access exception above a newer maintenance suggestion, record both the initial and final rank and the reason for the change.

Do not allow model confidence to carry consequence authority. A high-confidence duplicate-detection result can support a merge review; it cannot establish that two customer records are the same person. A low-confidence but plausibly consequential signal may need an exception route instead of the bottom of a general list.

NIST's Generative AI Profile describes risks and actions for managing generative-AI systems, including human-AI configuration, monitoring and the risk of people placing inappropriate trust in generated output.[^2] It is cross-sector guidance, not proof that a particular queue is safe or compliant. For an operator, the practical translation is to expose what the score can and cannot establish before the number influences work.

## Govern the screen, not only the API response

Logging the ordered array returned by a ranking service is not enough. The system also needs an exposure event.

For each review session, record the reviewer role, interface version, active filters, viewport or batch size, displayed candidate IDs, display positions and display time. Record when an item was opened, deferred, escalated, corrected or dismissed. A hover, impression, click and completed review are different events.

Research on ranked interfaces has repeatedly observed position effects: items shown higher in a list can receive more interaction independent of their actual relevance. One field study in digital-library recommender systems found a significant relationship between displayed rank and clicks.[^3] That research does not establish how self-storage employees behave, and a click is not an operational decision. It does show why teams should not treat list position as neutral or interpret interaction data without exposure context.

Microsoft Research's human-AI interaction guidelines similarly emphasize making system capability clear, supporting efficient correction, allowing granular feedback and updating adaptively with care.[^4] Those guidelines were evaluated across general AI-infused products, not facility operations. They provide a useful interface test: can the reviewer understand why an item is present, see what may be missing and correct the system without turning one click into a broad policy change?

The interface should therefore make at least five things visible: candidate age, source freshness, priority reason, evidence limitation and the next state caused by the review control. “Dismiss” should not ambiguously mean false event, duplicate, already handled, out of scope or postpone. Each disposition teaches a different lesson and creates different follow-up work.

## Protect consequential work from quiet starvation

A score-sorted queue can be internally consistent and still create an operating failure. New high-scoring items may continually push older work down. One busy facility may occupy every visible position. A candidate type with sparse training data may rarely reach the first page. A connectivity problem may keep one site's records out of the population altogether.

Build deterministic safeguards around the ranking model. Depending on the approved use, they may include:

- reserved visible capacity for defined consequence classes;
- maximum wait times before an item receives human review or escalation;
- facility and category coverage indicators;
- per-site or per-class concentration limits;
- explicit treatment of ties and missing scores;
- a route for quarantined or excluded consequential records;
- a manual view of the unranked admitted population; and
- a safe fallback order when the model, feature source or ranking service is unavailable.

These are policy decisions. They should not be invented by the model at runtime. A queue owner must define what the system optimizes, which classes it protects, when age overrides score and who may change those rules.

The objective is not to force every item onto the first screen. Scarce attention must be allocated. The objective is to make that allocation explainable, bounded and testable—and to keep an item from disappearing without a recorded reason.

## Do not learn from clicks alone

Once the queue is in use, a tempting feedback loop appears. Reviewers open the top items, so the system treats those interactions as evidence that the top items were relevant. Lower-ranked candidates receive fewer openings, so the system learns that they mattered less. The original ranking has influenced the labels used to justify the next ranking.

Break that loop by retaining exposure. An unopened displayed item is different from an item the reviewer never saw. A dismissed item is not necessarily a false event. A corrected priority is not necessarily a corrected source label. The record should distinguish presentation, human action, verified operating disposition and any later evaluation label.

Use controlled samples from lower-ranked, excluded and fallback populations where the consequence and privacy rules permit it. Review whether important categories are systematically late, whether particular facilities are underrepresented and whether interface changes alter disposition patterns. If the organization cannot support a valid sampling method, it should state that limitation rather than infer queue quality from clicks.

NIST AI 800-4, published in March 2026, describes challenges in monitoring deployed AI systems and explains why pre-deployment evaluation must be complemented by testing, evaluation, validation and verification after deployment.[^5] The report identifies open problems and does not certify a specific monitoring program. Its relevance here is direct: a ranked queue interacts with live users, changing data, interface constraints and surrounding workflow. A benchmark of model scores cannot observe that whole system.

## A fictional portfolio queue

The following scenario, company, facilities, systems, people, records, scores and outcomes are entirely fictional. They are a teaching device, not a customer case, deployment or performance result.

Palisade Grove Storage uses an invented morning-review queue across four fictional facilities. At 8:00 a.m., the build considers 31 source records and creates 12 candidates. Eight appear in the default desktop view.

Candidate `PG-Q-104` is a camera-heartbeat anomaly with a model score of 0.93. A deterministic rule identifies a current, approved maintenance window. The candidate remains visible, but its state is “monitor during declared maintenance,” not “camera outage.” It occupies position three after the rule adjustment.

Candidate `PG-Q-109` concerns a mismatch between an access schedule and a facility calendar. Its score is 0.71 and its initial rank is nine—just below the default view. The queue contract reserves one displayed position for current access-control exceptions, moving it to position six. The record does not claim that access is wrong. It states that the sources disagree and assigns a review owner.

Candidate `PG-Q-111` is a customer-account merge suggestion. It lacks a stable cross-system identity and is quarantined before ranking. It is routed to an identity-review queue with its evidence snapshot. It is not silently discarded and never becomes authority to merge accounts.

A fourth record from Palisade Grove East is not evaluated because the fictional source connector failed. The portfolio completeness banner reports three of four facilities evaluated. The queue does not convert that failure into a zero-candidate result for East.

At shift change, the system records which candidates were displayed, opened and handed forward. The manager closes no operating issue based on rank alone. Each candidate must still follow the authority, execution and readback rules appropriate to its type.

## Instrument the full path

W3C's PROV data model represents entities, activities, agents, usage, generation, attribution and responsibility.[^6] It does not authenticate a queue record or prescribe a database. It offers a sound vocabulary for linking a source event to a candidate, a candidate-set build, a ranking activity, an interface exposure and a human disposition without collapsing those steps.

OpenTelemetry's event conventions describe structured named occurrences with timestamps and attributes, while noting that the conventions are still in development.[^7] An implementation can use similar events for `candidate_created`, `candidate_admitted`, `candidate_ranked`, `candidate_displayed`, `candidate_opened`, `candidate_deferred`, `candidate_escalated` and `candidate_closed`. Telemetry alone does not prove correctness. The governing queue record and source evidence still need durable retention, access control and reconciliation.

Measure the system at each boundary. Useful indicators include source and facility coverage, exclusion and quarantine rates, time to first display, time below the visible threshold, rank changes by rule, protected-slot use, items exceeding their wait limit, lower-rank sample findings, reviewer corrections, interface-version effects and closed items lacking governing readback.

Do not reduce the report to average review time. A fast queue can be incomplete. A high click-through rate can be a position effect. A low override rate can mean the recommendations are strong, or that the interface makes correction difficult. The evidence packet should allow the operator to tell those explanations apart.

## Test the queue as an operating system

Before connecting a ranked list to daily work, run synthetic and explicitly fictional cases through the whole path. Remove one facility from the source response. Reverse a score direction. Produce a tie. Let new high-scoring items arrive continuously. Change the interface from eight visible rows to five. Apply a stale filter. Fail the ranking service. Quarantine a consequential identity conflict. Confirm that each case creates the intended visible state and owner.

Then test correction. If a reviewer changes a priority reason, does the system preserve the original output, the correction and the approved downstream label separately? If an item was excluded incorrectly, can it re-enter without losing its age? If a ranking policy changes mid-shift, can the team reconstruct which reviewer saw which order?

The accompanying `ai-queue-exposure-register.csv` provides one blank template and five fictional records covering admission, ranking, exposure, quarantine, missing-source handling and closure boundaries. It is an adaptable governance worksheet, not a deployed product or universal operating standard.

An AI assistant can influence operations long before it receives permission to write. The first page receives attention. The hidden candidate waits. The excluded record may vanish. Responsible architecture makes each of those states observable.

Below the fold is not nowhere. It is a decision the system has already started making.

<!-- BODY END -->

## Sources

[^1]: [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), AI RMF 1.0 resource, accessed September 10, 2026. Voluntary, cross-sector guidance; NIST states that AI RMF 1.0 is being revised. It does not prescribe this queue architecture or establish self-storage compliance.
[^2]: [NIST AI 600-1, *Artificial Intelligence Risk Management Framework: Generative Artificial Intelligence Profile*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), July 2024, accessed September 10, 2026. Cross-sector risk-management profile used for human-AI and monitoring concepts, not evidence of a product, deployment or result.
[^3]: [Beel and Collins, *A Study of Position Bias in Digital Library Recommender Systems*](https://arxiv.org/abs/1802.06565), arXiv:1802.06565, 2018, accessed September 10, 2026. Primary field study in digital-library recommender systems; it does not measure self-storage work, prove causation for a facility queue or make clicks equivalent to decisions.
[^4]: [Amershi et al., *Guidelines for Human-AI Interaction*](https://www.microsoft.com/en-us/research/wp-content/uploads/2019/01/Guidelines-for-Human-AI-Interaction-camera-ready.pdf), CHI 2019, accessed September 10, 2026. Peer-reviewed general interaction guidance validated with design practitioners and AI-infused products; it is not a facility-operations standard.
[^5]: [NIST AI 800-4, *Challenges to the Monitoring of Deployed AI Systems*](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.800-4.pdf), March 2026, accessed September 10, 2026. Research report describing monitoring challenges and open questions; it does not certify a monitoring method or specific implementation.
[^6]: [W3C, *PROV-DM: The PROV Data Model*](https://www.w3.org/TR/prov-dm/), W3C Recommendation, April 30, 2013, accessed September 10, 2026. Generic provenance model used as an architecture reference; it does not authenticate, validate or complete a facility record.
[^7]: [OpenTelemetry, *Semantic Conventions for Events*](https://opentelemetry.io/docs/specs/semconv/general/events/), current development-status specification page, accessed September 10, 2026. Technical telemetry conventions do not establish business authority, event truth, queue fairness or operational completion.

## Disclosure and publication state

Jared Mastroianni serves as Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. This article proposes an architecture and uses entirely fictional teaching data. It does not describe a released Facily.ai or Facily OS capability, a customer deployment, a measured operating result, a certification, legal advice or an industry standard.

**Proposed slug:** `facility-ai-priority-queue`

**Publication state:** Publication-ready local package only. No publisher handoff, repository change, CMS object, submission, schedule, publication, canonical activation, crawling, indexing, ranking, coverage or recognition has been established.
