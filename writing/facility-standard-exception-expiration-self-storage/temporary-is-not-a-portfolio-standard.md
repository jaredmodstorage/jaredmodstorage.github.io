# Temporary Is Not a Portfolio Standard: Put an Expiration Date on Every Facility Exception

**By Jared Mastroianni**

<!-- BODY START -->

A portfolio standard can be perfectly clear at headquarters and quietly untrue at three facilities.

One site delays a controller update because its gate hardware is different. Another uses a manual patrol while a camera component is unavailable. A third keeps last season’s extended access window because nobody owned the return to normal. Each decision may have started with a reasonable operating need. The problem begins when the deviation outlives the decision that authorized it.

That is how a temporary exception becomes a shadow standard.

Multi-location operators need exceptions. Buildings, equipment, vendors, staffing, weather, local requirements and customer commitments do not line up neatly across a portfolio. A mature system does not pretend those differences are absent. It gives each meaningful deviation a controlled life: proposed, reviewed, active, observed, expired or closed.

The key word is **life**. An exception is not a note attached to a policy. It is a governed operating object with scope, authority, evidence, compensating controls, time boundaries and an exit decision.

## The spreadsheet cell is not the control

Most exception tracking fails because it records the explanation but not the operating state. A row may say “temporary gate process approved,” yet leave the consequential questions unanswered:

- Which facility, system, workflow and policy clause are affected?
- What exact behavior is allowed to differ?
- Who had authority to accept the risk?
- What control is operating while the standard is not?
- What evidence shows that control is actually being performed?
- When does the exception stop being valid?
- What must happen at expiry if restoration is not yet safe?
- Who proves that the facility returned to the approved standard?

Without those fields, the tracker is an explanation archive. It cannot tell an operator whether the current condition is authorized.

Configuration-management guidance provides a useful foundation. NIST describes a baseline as an approved reference for later changes and treats change control, monitoring and recorded deviations as connected activities.[1] NIST’s control catalog likewise links documented change decisions, impact analysis, configuration settings and review.[2] Those publications address information systems and risk management, not self-storage operating policy. The transferable lesson is narrower: a deviation cannot be governed unless the baseline, the changed object and the evidence of current state are identifiable.

## Give every exception two boundaries

An exception needs both a **scope boundary** and a **time boundary**.

The scope boundary says exactly where the deviation applies. “Colorado sites” is usually too broad. “CR-03, north-gate controller, weekday opening schedule, policy OPS-AC-04 section 3.2” is testable. If the exception affects a customer message, payment path, access schedule or security process, name that downstream consequence too.

The time boundary says when the authority begins, when it will be reviewed and when it expires. These are different dates. A review date is a prompt to examine the exception. An expiry is the point after which the existing authorization is no longer enough.

Expiry should not blindly trigger an automated reversal. Returning a controller, access rule or facility process to a prior setting without checking current conditions can create a new problem. Instead, expiry should force a deterministic disposition:

1. restore the approved standard and verify it;
2. renew the exception through the same authority path with fresh evidence;
3. replace it with a newly approved standard; or
4. place the affected function in a defined hold or degraded mode until a qualified owner decides.

“Leave it as is” is not a fifth option. If the original authorization has expired, continued operation needs a new, visible basis.

## Separate the exception from the compensating control

An exception describes what is different. A compensating control describes what will reduce or detect the resulting risk while the difference exists. They should never share one vague sentence.

Suppose a fictional facility cannot complete a gate-controller update during the approved window. “Patch deferred” identifies the deviation. “Opening and closing event logs reviewed by the regional operations manager each business day, with unresolved anomalies held for technical review” identifies a separate control. The register should record the control owner, cadence, evidence location and most recent result.

That distinction matters because an exception can remain active while its compensating control fails. If the daily review was not performed, the authorization did not magically cover the missing control. The record should move to an attention state even if the exception’s calendar expiry is still two weeks away.

The same applies to assumptions. A deviation approved because a replacement part was expected Friday should not remain green when Friday passes and the shipment is still unconfirmed. The reason for the exception and the conditions supporting it are part of the evidence set.

## Use five states, not “open” and “closed”

A useful exception lifecycle has at least five states:

**Proposed.** The deviation is described, but authority has not been granted. The facility continues under the approved standard or an explicitly declared safe hold.

**Active.** The exception is within scope and time, the approving authority is recorded, required compensating controls are operating, and current evidence is available.

**Attention required.** The exception has not necessarily expired, but an assumption, control, owner, evidence item or review checkpoint has failed. The record needs action before it can be treated as active.

**Expired or held.** The authorization window ended without verified restoration, renewal or replacement. The affected function follows the predefined expiry behavior; the old approval is no longer presented as current.

**Closed and reconciled.** The standard was restored or formally changed, downstream copies were corrected, the effective state was independently read back, and the exception record carries its final disposition.

These states make a portfolio view honest. A dashboard that shows “14 exceptions” is incomplete. Operators need the population: 14 active out of how many applicable facilities and controlled objects, plus how many are proposed, attention-required, expired or awaiting reconciliation. A small number of expired exceptions can matter more than a large number of current ones.

## The register should answer a decision

The accompanying Facility Standard Exception Register is designed for one question: **May this facility continue operating differently from the named portfolio standard right now?**

Its fields fall into seven groups:

- identity: exception ID, facility ID, controlled object and baseline version;
- difference: exact standard requirement and permitted deviation;
- authority: requester, approver, decision time and authority basis;
- protection: risk statement, compensating control, owner, cadence and evidence;
- time: effective start, review date, expiry and local time zone;
- exit: restoration test, expiry behavior, renewal evidence and downstream reconciliation;
- current decision: observed state, last check, disposition, owner and next action.

One row should cover one bounded deviation. If a single approval changes both gate hours and customer communications, use linked rows unless the controls, owners, evidence and expiry behavior are truly identical. Bundled exceptions are difficult to close because one part often returns to standard before another.

The worked rows are explicitly fictional. Copper Ridge Storage Group, its facilities, systems, people, dates and outcomes do not represent modSTORAGE, a customer or a deployment. The examples demonstrate four different states: active with current evidence, attention required because a compensating-control check is missing, closed after verified restoration, and held while qualified review is pending.

## Run the portfolio review by consequence

A weekly review sorted only by expiry date will miss the exceptions that are failing early. Build the agenda in this order:

First, review expired and held records. They have no current authorization basis and need a bounded operating decision.

Second, review attention-required records. Look for missing evidence, failed controls, changed assumptions, absent owners and unresolved downstream effects.

Third, review active exceptions whose next checkpoint falls inside the review horizon. Confirm that the control evidence exists; do not accept the presence of a future expiry date as proof of health.

Fourth, sample closed records. Verify that the policy library, facility procedure, system setting, training aid and customer-facing channel no longer carry the deviation unless a new standard replaced it.

Finally, examine patterns. Repeated exceptions against the same requirement can mean the standard is unrealistic, the implementation is weak, the portfolio contains legitimate facility classes, or local teams are bypassing the process. The register identifies the pattern; it does not decide which explanation is correct.

NIST’s Cybersecurity Framework 2.0 treats policy as something that must be established, communicated, enforced and updated as conditions change, while also making roles and accountability explicit.[3] The 2025 GAO Green Book similarly connects policy implementation, monitoring and timely remediation of deficiencies.[4] These are not self-storage mandates, and they do not validate this register. They reinforce a practical operating point: policy, monitoring and correction fail when they are separated into different conversations.

## Do not turn the exception register into a permission machine

The register should support judgment, not manufacture authority. A completed row does not prove that the approver had legal, technical, safety, financial, privacy or employment authority. It does not replace a qualified review where one is required. It does not make a risky condition acceptable because the form is complete.

Keep three controls outside the spreadsheet:

**Approved authority matrix.** Define which roles may approve which classes of deviation and what requires escalation.

**System-enforced limits.** Prevent unauthorized settings or actions where practical. Documentation after the fact is weaker than bounded access before the change.

**Independent readback.** Verify the actual facility or system state from evidence other than the request or implementation note.

The register joins those controls. It should link to evidence, not substitute for it.

## Close the deviation everywhere it traveled

The most overlooked part of exception management is downstream cleanup. A temporary access window may appear in the facility management system, website, call-center note, printed sign, staff checklist and automation schedule. Changing one system does not close the exception.

Before marking a row reconciled, identify every consumer that received the deviation. Record the expected final state, the readback method, the person responsible and the completion time. If one public or operating surface is still wrong, the exception remains in reconciliation even if the primary system is correct.

This is where portfolio discipline shows up. The goal is not to eliminate local judgment. It is to prevent yesterday’s local judgment from becoming today’s invisible policy.

A temporary exception should make the portfolio more honest, not less. Name the standard. Bound the difference. Record the authority. Test the compensating control. Force a decision at expiry. Then prove the deviation is gone everywhere it mattered.

<!-- BODY END -->

## Sources

1. National Institute of Standards and Technology, [Guide for Security-Focused Configuration Management of Information Systems, SP 800-128](https://csrc.nist.gov/pubs/sp/800/128/upd1/final).
2. National Institute of Standards and Technology, [Security and Privacy Controls for Information Systems and Organizations, SP 800-53 Rev. 5](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final).
3. National Institute of Standards and Technology, [The NIST Cybersecurity Framework (CSF) 2.0](https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=957258).
4. U.S. Government Accountability Office, [The Green Book: Standards for Internal Control in the Federal Government, 2025 Revision](https://www.gao.gov/greenbook).

*Research synthesis, drafting and editorial QA were AI-assisted. The method and all fictional teaching examples require operator review before use.*
