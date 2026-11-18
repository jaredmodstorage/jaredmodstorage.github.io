---
title: "The Regional Manager Changed. Who Owns the Open Work Tomorrow?"
slug: regional-manager-change-open-work-ownership
author: Jared Mastroianni
destination: Jared Mastroianni personal authority site
canonical: https://jaredmodstorage.github.io/writing/regional-manager-change-open-work-ownership/
lane: Midday systems
intended_slot: 2026-11-17 13:00 America/New_York
---

# The Regional Manager Changed. Who Owns the Open Work Tomorrow?

A regional-manager change can look clean in an organization chart and still leave a portfolio with hundreds of small ownership failures. The directory shows the new name. The open work still points to the former manager. A vendor exception waits in an inbox. A rate approval is routed to an inactive queue. A facility manager assumes someone else is watching the unresolved access issue.

That is not a personnel-directory problem. It is a responsibility cutover.

The operating question is not only, “Who has the role now?” It is, “At the effective time, who can see, decide, escalate and close every item that came with the role?” If that question cannot be answered from a controlled record, the portfolio has created orphan work.

The right cutover preserves two truths at once. Historical records must continue to show who actually made earlier decisions. Future authority must move to the new owner at a defined time. Open work needs an explicit transfer, because it belongs neither entirely to history nor automatically to the future org chart.

## A reporting-line edit is not a work transfer

Most portfolios store responsibility in more places than they realize. The obvious places are the employee directory and facility roster. The consequential places include maintenance queues, vendor approvals, customer escalations, rate exceptions, purchasing requests, access groups, recurring reports, incident channels, project plans and email rules.

Changing the directory entry may update none of them.

This is why a cutover should begin with work surfaces, not names. List every system or process in which the regional manager is an owner, approver, recipient, escalation point or fallback. Then test whether each surface is driven by the directory, by a separate role mapping, by a manually maintained distribution list or by a personal account.

The distinction matters. A role-based route may update automatically. A personal approval queue may not. An automated update can also be wrong if the source mapping is stale. “Synced” is a transport state, not proof that the right person received the right authority.

The [NIST Cybersecurity Framework 2.0](https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf) treats roles, responsibilities and authorities as things an organization should establish, communicate, understand and enforce. That is a useful control principle even though the framework addresses cybersecurity risk, not self-storage reporting lines. A title alone is not enough. Authority has to be made operational.

## Preserve history; transfer the future

A common mistake is to replace the former manager’s name everywhere, including historical records. That makes the current view look tidy by rewriting what happened.

Do not do that.

If the former manager approved a vendor change on Friday, the record should still show that approval on Friday. If the new manager takes responsibility Monday at 8:00 a.m., future decisions should carry the new owner. The cutover record links those states without collapsing them.

Use at least three time fields:

- **Recorded time:** when the source system captured the event or assignment.
- **Effective time:** when authority changes for future work.
- **Acceptance time:** when the incoming owner confirms the transferred scope is visible and usable.

These times can differ. An executive decision may be recorded Friday, become effective Monday and be accepted by the incoming manager after a Monday-morning readback. Treating them as one timestamp hides the interval in which the organization may have authority on paper but no confirmed operator at the controls.

Open items need their own rule. At the effective time, snapshot each item’s identifier, facility, category, status, priority, due date, former owner, incoming owner and next required action. Preserve the former owner as historical attribution. Assign the incoming owner as the responsible party from the effective time forward. If acceptance is missing, route the item to a temporary exception owner instead of pretending the transfer succeeded.

## Inventory the work surfaces before the effective time

The cutover inventory should be specific enough to test. “Update all systems” is not a control. A useful inventory names the surface, its source of responsibility, the expected change and the evidence that will prove the change worked.

Group the inventory into five classes:

1. **People and facility scope.** Facility roster, regional hierarchy, on-call schedule and coverage map.
2. **Decision authority.** Rate exceptions, credits, purchasing thresholds, vendor scope changes and other approvals.
3. **Open work.** Maintenance, customer, safety, collections, project and compliance queues.
4. **Visibility and escalation.** Dashboards, alerts, distribution lists, incident channels and executive reports.
5. **Access.** Physical access groups, application roles, shared resources and privileged accounts.

Access deserves a separate pass because operational ownership and technical permission are related but not identical. The incoming manager may need visibility without authority to approve a particular transaction. The departing manager may lose future approval rights while retaining a legitimate historical record. Apply least privilege to the new assignment and remove obsolete access according to policy.

NIST Special Publication 800-53 includes controls for reviewing access when personnel are transferred or reassigned and for modifying authorization as needed. Its [official publication page](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) is written for federal information systems, not as a self-storage staffing procedure. The transferable lesson is narrower: a personnel change should trigger a defined review of ongoing need, authorization and notification. It should not depend on someone remembering later.

## Use a cutover state model that exposes failure

I would not label a responsibility change “complete” when the new name appears in the roster. I would use six states:

| State | What it means | Evidence required |
| --- | --- | --- |
| Identified | The affected responsibility surface is known. | Named system, process or queue and current source owner. |
| Mapped | The future owner, effective time and transfer rule are defined. | Approved mapping with exception owner. |
| Accepted | The incoming owner confirms the scope and access. | Timestamped acceptance and unresolved-question list. |
| Effective | The new authority is active at the planned time. | System or process evidence from the live surface. |
| Reconciled | Expected and actual ownership agree; exceptions are visible. | Before-and-after counts and exception queue. |
| Closed | All cutover exceptions are resolved or formally handed off. | Independent closeout and retained evidence. |

The sequence is deliberate. A mapping can exist without being accepted. Acceptance can occur before the effective time. An effective change can still fail reconciliation. Closure is the end of exception work, not the moment someone edits the roster.

This model also prevents a quiet failure from being mistaken for success. If an open item has no incoming owner after the effective time, it remains in an orphan queue. If two people can approve the same action, it enters a dual-authority queue. If the incoming manager owns the work but lacks access, it becomes an unauthorized-to-act exception. If a routing rule still points to the old owner, it is a stale-route exception.

## Run four exception tests

Every cutover should be tested for four conditions:

**Unowned:** Does any open item, facility or escalation path lack exactly one accountable owner after the effective time?

**Dual-owned:** Can both the former and incoming manager make the same future decision when policy calls for one decision owner?

**Unauthorized:** Is someone assigned work they cannot view, approve or close? Conversely, does someone retain access they no longer need?

**Stale route:** Does an alert, report, shared mailbox or approval rule still send future work to the former owner or an obsolete list?

Run the tests against real inventories and live configuration, not only the planned mapping. Count the expected open items before cutover. Count the transferred items afterward. Explain every difference. A zero in the orphan queue is meaningful only if the source population is complete.

Use a short readback with facility managers as well. Ask each manager whom they would contact for an urgent operational decision, which unresolved items they believe are still open and where they would see the new escalation path. Their answers often expose a communications failure that a clean system export will not.

## Require acceptance, not silent assignment

Responsibility should not be pushed onto an incoming manager without a visible acceptance step. Acceptance means the person can see the facilities, understands the decision boundaries, has the necessary access and has reviewed the open-work inventory. It does not mean every inherited item is already solved.

The acceptance record should capture:

- facilities and queues received;
- decision rights granted and excluded;
- open items by category and priority;
- items rejected because the mapping is wrong;
- temporary coverage for unavailable systems or people;
- the first reconciliation deadline; and
- the escalation owner for unresolved cutover defects.

This is a compact operating contract. It gives the outgoing and incoming sides a common scope, gives leadership an exception list and gives facility teams one current route for decisions.

## A fictional portfolio example

The following scenario is explicitly fictional and uses invented names and data.

Cedar Atlas Storage changes the regional manager for four facilities effective Monday at 8:00 a.m. The cutover inventory identifies 62 open items across maintenance, vendor review, rate exceptions and customer escalation. The mapping assigns 58 items to the incoming manager. Two safety items move to the operations director because their escalation authority is separate. One vendor invoice remains with finance. One maintenance item has no valid facility identifier and enters the orphan queue.

At acceptance, the incoming manager can view all four facilities but cannot approve vendor scope changes. That is recorded as an unauthorized-to-act exception, not as a successful transfer. A temporary approver is named, the access defect receives a deadline and the affected vendor item remains visible in the exception queue.

After the effective time, reconciliation finds that an overnight alert still routes to the former manager. The team corrects the stale route and retains the test result. The cutover closes only after the orphan item is matched to a facility, the missing approval right is resolved and the alert route passes a new test.

The point is not the fictional counts. It is the separation of states. The roster changed once. Operational responsibility became trustworthy through inventory, acceptance, effective-time evidence, reconciliation and exception closure.

## The practical tool: Portfolio Responsibility Cutover and Orphan Queue

Use the companion **Portfolio Responsibility Cutover and Orphan Queue** to manage the transfer. Maintain one row per responsibility surface or open item. Do not summarize a queue as “done” when individual exceptions still lack owners.

The minimum fields are: record ID, facility, work surface, source item ID, historical owner, incoming owner, decision authority, effective time, acceptance time, access status, route-test status, exception class, exception owner, next action, due time, evidence link and final state.

The tool is intentionally plain. Its value is in forcing the portfolio to answer the question hidden by an org-chart edit: who owns the open work tomorrow, and what proves they can act?

A regional-manager change is complete when future authority is active, historical attribution remains intact, the incoming owner has accepted the scope, every open item has exactly one accountable route and the exception queue is closed. Anything less is a personnel update with operational debt attached.
