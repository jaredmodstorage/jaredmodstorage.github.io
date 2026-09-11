# Keep, Hold, Delete, Prove: A Portfolio Evidence-Retention Map for Self-Storage

**By Jared Mastroianni**

**Proposed destination:** Jared Mastroianni personal authority site  
**Proposed slug:** `self-storage-portfolio-evidence-retention-map`

<!-- BODY START -->

A self-storage portfolio can accumulate operating evidence faster than anyone can explain why it still exists. Gate events remain in an access platform. Incident photographs sit in a shared drive. Call recordings live with one vendor, payment receipts with another, and work-order attachments inside a maintenance system. Exports multiply. Backups persist. A manager saves a local copy because the central team may need it later.

The usual response is one of two extremes: keep everything, or let every system use its default. Neither is a retention program.

Keeping everything increases exposure, cost and discovery burden. Accepting defaults can remove evidence before an operational, contractual or legal need has ended. The portfolio needs a third approach: decide by record class, purpose, authority, trigger and verified disposition.

That requires a portfolio evidence-retention map. It does not invent a universal number of days. It shows which qualified owner must supply the rule, when the clock begins, what pauses disposition, where copies exist and what evidence proves that an authorized deletion actually finished.

## Retention starts with purpose, not storage capacity

The first question is not, “How much space do we have?” It is, “What decision or obligation does this record support?”

A gate event may support access investigation. A signed rental agreement may establish a contractual record. A work-order photograph may support technical closeout. A call recording may serve quality review. A payment-provider receipt may support financial reconciliation. Those records can sit in the same cloud account and still have different retention logic.

The Federal Trade Commission advises businesses not to keep sensitive personal information without a legitimate business need and to maintain a written policy covering what is kept, how it is protected, how long it is kept and how it is securely disposed.[^1] That guidance does not give a self-storage operator a complete schedule. It establishes the operating problem: “We might need it someday” is not enough.

Start by naming a bounded record class. “Camera data” is too broad. “Exported loading-area clip attached to incident record IR-104” is usable. “Customer documents” is too broad. “Executed rental agreement for facility FAC-017 under contract version 6” is usable.

Then state the purpose. If a record supports several purposes, list them separately. The end of one purpose must not silently erase another. A customer-service review may finish while a dispute, audit or incident review remains open.

## Separate the record from every copy

Operators often map the primary system and miss the rest of the evidence population. One file may exist in the operating platform, an email attachment, a manager’s desktop, a reporting warehouse, a vendor archive and several backups. A deletion request against the primary application does not establish that all governed copies are gone.

For each record class, identify:

- the system of record;
- exports and downloaded copies;
- integrations and downstream derivatives;
- vendor-controlled copies;
- backups and recovery media;
- reports, dashboards or AI indexes derived from the source; and
- the owner responsible for each location.

NIST’s Privacy Framework treats collection, retention, use, transformation, sharing and disposal as parts of a data lifecycle.[^2] That lifecycle view matters in a portfolio because the same evidence may move across facility, regional, corporate and provider systems. The map should follow the record through those movements rather than treating the application where it began as its entire life.

Derived data needs an explicit rule. Deleting a photograph does not automatically delete a thumbnail, extracted text, embedding, incident summary or model-evaluation record created from it. Some derivatives may have a valid separate purpose; others may not. The map should name which derivatives remain governed by the source disposition and which have their own approved class.

## Give every retention clock a defined trigger

“Keep for three years” is incomplete because it does not say three years after what.

Creation, contract termination, incident closure, claim settlement, audit completion and policy supersession are different triggers. If two facilities calculate from different events, the portfolio does not have one retention standard even when the duration field matches.

The National Archives’ federal records guidance distinguishes fixed periods after creation from periods that begin after a predictable event, and it warns that vague directions such as “when no longer needed” can undermine control.[^3] Federal records rules do not govern an ordinary private self-storage company simply because they are useful examples. The transferable lesson is precision: record the event that starts the clock, the source that proves the event occurred and the time at which the system calculated eligibility.

Do not calculate an eligibility date when the trigger is unknown. Use `not evaluated`. If the trigger depends on contract termination but the facility identity or contract is unresolved, the record is not eligible for automated disposition. Unknown is a control state, not permission to guess.

The map also needs a policy version. A record created under one schedule may be reviewed under a later schedule. The organization’s qualified owners must decide whether the new rule is prospective, retrospective or subject to transition instructions. A systems team should not silently recompute historic disposition dates because a spreadsheet cell changed.

## Holds outrank the routine clock

An elapsed retention period does not, by itself, authorize deletion. Litigation, regulatory, insurance, audit, investigation or other preservation duties may require a hold. The exact trigger, scope and release authority belong to qualified counsel and the organization’s approved process.

That boundary should be visible in the operating record. At minimum, capture hold status, hold identifier, covered record classes, affected facilities or parties, issue time, issuing owner, acknowledgment state and release authority. “Legal may need this” is not a usable hold. Neither is the absence of a visible hold field proof that no hold exists.

The current Federal Rules of Civil Procedure govern civil cases in United States district courts, and Rule 37 addresses the loss of electronically stored information that should have been preserved in anticipation or conduct of litigation.[^4] Applicability and preservation decisions are legal questions. For the operator, the practical rule is narrower: a routine deletion workflow must query the current approved hold source and stop when the result is active, conflicting, unavailable or not evaluated.

A hold also needs distribution evidence. If the records owner enters a hold in one register but the access vendor, backup owner and facility manager never receive it, the portfolio has a policy statement rather than an implemented preservation control.

## Deletion is an executed change, not a status label

Once a record becomes eligible, the next state is not automatically “deleted.” Eligibility, approval, execution, provider receipt, independent readback and reconciliation are separate events.

NIST SP 800-88 Revision 2 defines media sanitization as rendering access to target data infeasible for a given level of effort and frames sanitization as an organizational program with applicable techniques and controls based on information sensitivity.[^5] That publication is focused on media sanitization, not on choosing a self-storage record’s legal retention period or operating a software provider’s application. It is still a useful reminder that a delete button and a verified sanitization outcome are not interchangeable.

For software records, define the required evidence before execution. It may include a job identifier, affected-record count, provider receipt, query showing the record absent, exception report, backup-expiry path and downstream reprocessing result. For physical media, use the organization’s approved sanitization or destruction method and evidence. The method must fit the medium, sensitivity, contract and applicable requirements.

Never use the primary record’s disappearance as the only test. A failed search could mean the identifier changed, permissions narrowed, an index is stale or the record moved. Read back by stable identity from the governing source, then check expected copies and derivatives.

## Reconcile across the portfolio

Retention becomes a multi-location operating system when central policy and facility execution can be compared without erasing local obligations.

Consider a fictional teaching example. Alder Point Storage Group has twelve fictional facilities. Its approved internal schedule says a fictional category of routine call-review recordings becomes eligible 30 days after review completion, unless a hold or another purpose remains. Ten sites use the portfolio platform. One site exports recordings for coaching. Another has an inherited vendor account with an unknown backup policy.

On day 31, the portfolio cannot truthfully report “recordings deleted.” It can report ten primary-system dispositions verified, one export population awaiting reconciliation and one vendor backup scope not evaluated. The equal duration did not create equal execution coverage.

That distinction is the reason to retain a portfolio control total. For each scheduled run, count the eligible population, approved population, attempted population, provider-accepted population, independently verified population, held population and unresolved population. The counts should reconcile to one exact scope. A clean percentage with missing facilities is worse than an honest exception.

Assign exceptions to named owners and due dates. A record stays open when a vendor cannot confirm its backup behavior, when a local export lacks identity, when a hold source is unavailable or when a derivative was omitted. Closing the central job while those exceptions remain is administrative completion, not portfolio reconciliation.

## Use the map before buying another storage tier

The accompanying Portfolio Evidence-Retention Map is built for records, privacy, security, legal, finance, operations and system owners to complete together. It captures record purpose, source identity, copies, derivatives, schedule authority, trigger, eligibility, holds, approved disposition, execution evidence, readback and residual exceptions.

The blank row intentionally contains no default retention period. The fictional rows illustrate operating states, not legal requirements or modSTORAGE practices. An operator should adapt the fields to applicable law, contracts, insurance requirements, approved policy and the actual capabilities of each system and provider.

A mature retention program does not celebrate deletion volume. It can explain why a record exists, why it must remain, why it may leave and how the portfolio proved the result. Keep, hold, delete and prove are four different decisions. The map keeps them that way.

<!-- BODY END -->

## Sources

[^1]: Federal Trade Commission, [Protecting Personal Information: A Guide for Business](https://www.ftc.gov/business-guidance/resources/protecting-personal-information-guide-business), accessed September 11, 2026.
[^2]: National Institute of Standards and Technology, [NIST Privacy Framework Version 1.0](https://www.nist.gov/privacy-framework/privacy-framework), January 2020; accessed September 11, 2026.
[^3]: National Archives and Records Administration, [Preparing Disposition Instructions](https://www.archives.gov/records-mgmt/scheduling/instructions), reviewed June 6, 2019; accessed September 11, 2026.
[^4]: Administrative Office of the U.S. Courts, [Federal Rules of Civil Procedure](https://www.uscourts.gov/forms-rules/current-rules-practice-procedure/federal-rules-civil-procedure), current rules last amended in 2025; accessed September 11, 2026.
[^5]: National Institute of Standards and Technology, [SP 800-88 Rev. 2, Guidelines for Media Sanitization](https://csrc.nist.gov/pubs/sp/800/88/r2/final), September 2025; accessed September 11, 2026.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.
