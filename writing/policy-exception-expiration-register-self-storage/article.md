---
title: "The Policy Changed. Which Facilities Are Still Authorized to Operate the Old Way?"
slug: "policy-exception-expiration-register-self-storage"
author: "Jared Mastroianni"
canonical: "https://jaredmodstorage.github.io/writing/policy-exception-expiration-register-self-storage/"
publication_destination: "Jared Mastroianni personal authority site"
publisher_owner: "Master Personal Site Authority"
intended_slot: "2026-10-30 midday-systems"
status: "publisher-ready; not yet published"
featured_image: "063-operations-metrics-roundtable.png"
---

# The Policy Changed. Which Facilities Are Still Authorized to Operate the Old Way?

**By Jared Mastroianni**

A portfolio can publish a new operating policy in the morning and still have facilities following the old one that afternoon. That is not automatically a failure. A gate controller may need a replacement board. A local fire official may require a different inspection sequence. A software migration may reach ten sites before the eleventh. The problem begins when a temporary exception turns into an undocumented operating model.

Most exception tracking starts as a note: “Site 14 stays on the old process until the new hardware arrives.” The sentence sounds specific. It is not. Which policy version applies? Who approved the exception? What keeps the old process safe and controlled? When does the authority end? What evidence closes it?

If those answers live in email, memory, and meeting notes, portfolio leadership cannot tell the difference between an approved exception and an unapproved deviation. A policy library alone will not solve that. The operating system needs an exception register with expiration, compensating controls, evidence, and disposition.

## A published policy is not the same as an effective policy

At a single facility, a manager can often explain the local reality. Across a portfolio, that reality fragments quickly. The official document says one thing; the access system, vendor instruction, training packet, and manager checklist may each say another.

The first discipline is to separate three states:

1. **Policy issued:** the governing document has been approved and released.
2. **Policy adopted:** the required people, systems, assets, and procedures at a facility have changed.
3. **Exception authorized:** a defined facility or process may temporarily operate outside the new baseline under stated conditions.

Those states should never be collapsed into a single “complete” field. A portfolio can be 100 percent issued, 82 percent adopted, and 18 percent operating under active exceptions. That is a useful picture. “Rollout complete” is not.

The governance principle is broader than self-storage. The [NIST Cybersecurity Framework 2.0](https://www.nist.gov/cyberframework) puts policy, roles, oversight, and continuous improvement inside its Govern function. [NIST Special Publication 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) describes controlled change as a sequence that includes proposal, justification, review, approval, implementation, testing, documentation, record retention, and monitoring. These are cybersecurity publications, not self-storage rules. Their value here is the operating pattern: a change is governed through evidence and authority, not merely announced.

## An exception is a bounded authorization

A proper exception is not permission to “keep doing what we were doing.” It is permission to perform a specific activity, at a specific place, for a specific reason, until a specific event or date, under specific controls.

Every exception record should answer nine questions:

- **Baseline:** Which policy, standard, procedure, or control is being excepted, including version?
- **Scope:** Which facility, asset, workflow, vendor, role, or customer segment is affected?
- **Conflict:** What exact requirement cannot be met now?
- **Reason:** What verified condition creates the need?
- **Authority:** Who may accept the temporary operating risk?
- **Compensating control:** What reduces risk while the baseline is unmet?
- **Owner:** Who performs the control and gathers evidence?
- **Term:** When does the exception begin, when is it reviewed, and when does it expire?
- **Disposition:** Did the site adopt the baseline, renew through a new decision, replace the policy, or stop the affected activity?

If a record cannot answer those questions, it is an observation or request—not an active authorization.

## Expiration must change what the system allows

An expiration date that only changes a cell from green to red is weak governance. Expiration should trigger a change in authority.

At minimum, the system should notify the site owner and regional operator before expiry, require evidence for closure or renewal, and stop representing the exception as valid after its end time. For higher-consequence activities, expiry should also place the affected action on hold until an authorized person makes a new decision.

Do not auto-renew. A renewal is a new authorization based on current facts. It may use the prior record as history, but it needs a new rationale, current evidence, a new term, and an accountable approver. Otherwise, six 30-day extensions quietly become a permanent policy that no one wrote.

The register also needs explicit states. A practical set is:

| State | Meaning | Portfolio action |
|---|---|---|
| Requested | Exception proposed; no authority granted | Continue baseline or hold affected activity |
| Active | Approved term and controls are in force | Monitor controls and evidence |
| Review due | Decision point is approaching | Close, revise, or submit renewal |
| Expired | Authorization ended without disposition | Escalate and apply defined hold |
| Closed—baseline adopted | Facility now meets the current policy | Verify closure evidence |
| Closed—superseded | A later policy or design resolved the conflict | Link the replacement authority |
| Revoked | Authorization withdrawn before expiry | Stop excepted operation and document handback |

“Pending renewal” should not be treated as active. Pending means the decision has not been made.

## Compensating controls must be observable

The phrase “manager will monitor” is not a compensating control. It does not say what the manager checks, how often, against what threshold, where evidence is stored, or what happens when the check fails.

A usable control has five parts:

- a named action;
- a responsible role;
- a frequency or trigger;
- retained evidence; and
- a failure response.

Suppose a site cannot yet use the portfolio’s automated after-hours access review. A temporary control might require the facility manager to review the prior day’s access exceptions by 10:00 a.m., attach the exported exception list to the record, and escalate any unmatched entry to the regional manager before access settings are changed. That is testable. “Review access regularly” is not.

The control should also match the gap. A daily reconciliation may address delayed automation; it does not correct a broken gate, replace emergency access, or authorize a manager to override a lease restriction. One vague control should not be stretched across unrelated risks.

## Make the denominator honest

Exception reporting becomes misleading when the denominator excludes inconvenient records. A weekly portfolio view should include every in-scope facility and show at least:

- facilities on the current baseline;
- facilities with active exceptions;
- exceptions due for review within the selected window;
- expired exceptions awaiting disposition;
- requested exceptions that are not approved; and
- facilities with missing adoption evidence.

Count exceptions by both record and facility. Five exceptions at one conversion site are different from five facilities each carrying the same unresolved gap. Track age by first approval date as well as current renewal date so repeated extensions remain visible.

Useful operating measures include median exception age, percentage with current evidence, number expiring within 7/30 days, number expired, and time from closure claim to verified closure. These are management indicators, not proof that a control works. The underlying evidence still matters.

## Keep the decision trail attached

The exception record should link the policy version, approval, control evidence, renewal decisions, and closure evidence. That relationship is provenance: what changed, who acted, which source informed the decision, and what later replaced it. The [W3C PROV-O Recommendation](https://www.w3.org/TR/prov-o/) provides a formal model of entities, activities, and agents. A self-storage operator does not need to implement a semantic-web standard to benefit from the idea. A durable record should show the lineage of the operating decision.

Do not overwrite the old exception when terms change. Close it or supersede it, then create the next record. That preserves the difference between “approved for 30 days twice” and “approved for 60 days from the start.” It also prevents a later editor from making history look cleaner than it was.

## A fictional portfolio example

**The following scenario and every facility, date, record, and condition in it are fictional. They are provided only to demonstrate the method.**

Cedar Harbor Storage releases Policy ACC-07 v4, requiring an automated daily comparison between access exceptions and approved customer or vendor records. Eleven facilities adopt the new workflow. Harbor East cannot because its controller export is incompatible with the comparison job.

The regional operator opens exception EX-104. The scope is one controller at Harbor East, not the entire facility and not all access requirements. The approved compensating control requires the manager to export the prior day’s exception list by 10:00 a.m.; match each entry to an approved record; attach the signed review; and escalate unmatched activity before any credential change. The regional operator owns weekly evidence review. The exception expires in 21 days or when the controller connector is verified, whichever occurs first.

On day 18, the connector is installed, but the first comparison job fails. The project team cannot close EX-104 based on installation. The exception remains active through its existing term while the manual control continues. On day 20, a successful comparison, output review, and manager handoff are attached. EX-104 closes as “baseline adopted.”

That record shows what happened without pretending the automated control existed before it worked.

## The operator tool: an exception expiration register

The companion **Portfolio Policy Exception Expiration and Compensating-Control Register** is designed for one row per authorization. It separates scope, authority, control execution, review, expiration, and final disposition. It also includes stop conditions and evidence links so a regional operator can act without reconstructing the decision from email.

Use it in four routines:

1. **Before approval:** reject requests with vague scope, missing authority, or untestable controls.
2. **Weekly:** review evidence status, failed controls, approaching dates, and expired records.
3. **At renewal:** create a new decision from current evidence; do not extend silently.
4. **At closure:** verify adoption or replacement evidence before changing the record to closed.

The goal is not to eliminate every exception. Portfolios need a disciplined way to handle real differences among facilities. The goal is to make each difference explicit, temporary when intended, and visible to the people responsible for customer service and operating risk.

A policy becomes real when the facility can perform it. Until then, leadership should know exactly who is authorized to operate differently, why, under what control, and for how long.

