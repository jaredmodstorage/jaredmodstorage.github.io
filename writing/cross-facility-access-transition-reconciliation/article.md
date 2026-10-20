# The Customer Moved Facilities. Did the Old Gate Permission End?

**Deck:** A cross-facility transfer is not complete when the new unit appears. The portfolio must reconcile the old entitlement, the new entitlement, any approved overlap and the readback from both access boundaries.

**By Jared Mastroianni**

![Three facility leaders review access technology on a tablet beside an entry terminal.](065-access-technology-leadership-demo.png)

*A simple customer move can span identity, rental and physical-access systems. The operating system needs evidence from each boundary before it calls the transition complete. Editorial image; provenance and non-documentary-use limits are recorded in the package.*

<!-- BODY START -->

A customer transfers from one facility to another. The new rental is active. The customer can enter the new gate. The transfer ticket is marked complete.

But can the customer still enter the old property?

That question exposes a common portfolio weakness. Teams treat access as a feature attached to the new rental instead of an entitlement that must be changed across two operating boundaries. The grant at the destination is visible because the customer needs it immediately. The removal at the source is easier to miss, especially when rental, access and customer systems update on different schedules.

A strong multi-location process does not assume that creating the new permission removed the old one. It defines both changes, allows overlap only when someone has authorized it, reads back the effective state from both facilities and keeps the transfer open until the two sides reconcile.

## A transfer has two access obligations

For access control, a cross-facility move should create at least two explicit obligations:

1. Grant the approved entitlement at the destination facility.
2. End the no-longer-approved entitlement at the source facility.

Those actions may share one customer identity, but they are not one system event. One can succeed while the other fails. A portfolio workflow that stores only “access updated” hides that possibility.

The record should name the subject using a governed internal identifier, not a phone number, email address or gate code. It should name both facilities, both unit references, the exact permission scopes and the effective transition time. If another authorized user is associated with the rental, that person’s entitlement needs its own disposition. A primary customer’s transfer does not prove that every secondary user, vendor code or temporary credential moved correctly.

This is where identity and entitlement must stay separate. The identity answers **who** the subject is. A credential supports a method of authentication. An entitlement answers **where, when and for what purpose** access is allowed. The same credential can remain bound to the person while the authorized facility scope changes.

## Do not confuse request, acceptance and enforcement

Access workflows often collapse several states into one green checkmark. Keep these stages distinct:

- **Requested:** The business workflow asked for a grant or revocation.
- **Accepted:** The receiving system acknowledged the request.
- **Enforced:** The target access system reports the permission in the expected state.
- **Verified:** An approved readback confirms the facility, subject, scope and effective time.
- **Reconciled:** Source and destination results agree with the transfer contract.
- **Closed:** Exceptions have owners, evidence is attached and the designated authority closes the transition.

A provider receipt is important, but it is not always proof of enforcement. “Request accepted” may mean the item entered a queue. A successful destination test does not say anything about the source facility. A closed rental does not prove that a separate access platform removed its permission.

The National Institute of Standards and Technology’s SP 800-53 Revision 5 includes account-management practices for establishing, activating, modifying, disabling and removing accounts; defining authorized users and privileges; reviewing accounts; and aligning access with approved use. Its access-control catalog is designed for information systems and organizations and is customizable. It is not a self-storage gate standard or a legal rule for a particular operator. It is still useful architecture guidance: lifecycle changes deserve named owners, defined triggers and reviewable evidence.

## Define the transition contract before automating it

The portfolio should publish one versioned access-transition contract. At minimum, it should answer:

- What event authorizes the destination grant?
- What event authorizes the source revocation?
- Are the events simultaneous, ordered or allowed to overlap?
- Which facility schedules, door groups and time windows belong to each entitlement?
- Which source owns the effective time?
- Which system provides the authoritative readback?
- What happens when either side is unavailable?
- Who may approve an exception, for how long and for what scope?
- What evidence is required before closure?

The contract matters because different facilities may be configured differently even when their screens look the same. One site may manage gate and building permissions as a single group. Another may assign separate door schedules. A third may use a portfolio-wide identity with facility-level entitlements. The reconciliation layer should compare the intended outcome, not assume that identical button presses produce identical scope.

## Make overlap explicit

Some transfers legitimately need an overlap window. A customer may require a day to move property between locations. That operational need should become a bounded authorization, not an indefinite side effect.

Record the overlap start, overlap end, approving role and exact facility scopes. At expiration, the source permission should enter the revocation workflow automatically or appear as a priority exception. If the end time is extended, preserve the original authorization and create a new approved interval. Do not overwrite history.

An overlap is different from an unresolved revocation. The first is authorized and time-bounded. The second is a control failure or unknown state. Dashboards should not display both as “active at two facilities” without the reason, because the operator consequence is entirely different.

NIST Cybersecurity Framework 2.0 expresses the same general discipline in outcome terms. Its Identity Management, Authentication and Access Control category says that access permissions, entitlements and authorizations should be defined in policy, managed, enforced and reviewed, and that physical access should be managed, monitored and enforced commensurate with risk. CSF 2.0 is voluntary guidance, not proof that a particular design is sufficient. For portfolio operators, the practical translation is straightforward: the entitlement needs a policy state and an observed state, and the two need to be compared.

## Reconcile the negative side of the move

Most operational dashboards are good at showing what now exists. They are weaker at proving what should no longer exist.

For each transfer, run a two-sided reconciliation:

| Question | Required evidence |
|---|---|
| Is destination access expected? | Approved transfer and destination scope |
| Was the grant accepted? | Provider or system receipt |
| Is the grant enforced? | Authoritative destination readback |
| Is source access expected to end? | Approved effective time and source scope |
| Was revocation accepted? | Provider or system receipt |
| Is old access absent? | Authoritative source readback |
| Is any overlap still valid? | Current authorization and unexpired interval |
| Are secondary users resolved? | Individual dispositions or linked evidence |

The source readback is the step most likely to be skipped. It should state what was queried and what absence means. A blank search result, a disabled account and an account with no source-facility entitlement are not automatically the same state. The contract should specify which evidence satisfies the expected outcome.

## Design the exception before the failure

If the destination grant fails, the customer may be standing at the new gate. If the source revocation fails, no one may notice. Both deserve a response, but the operational consequences differ.

Define exception classes such as:

- destination grant pending;
- destination scope mismatch;
- source revocation pending;
- source entitlement still observed;
- overlap expired but still active;
- secondary-user disposition missing;
- provider receipt without enforceable readback;
- identity or facility mismatch;
- conflicting system states.

Every exception needs a current owner, next review time and an approved manual control when one exists. Manual control must be narrow. It should not create an unrecorded master code, duplicate identity or broad portfolio permission simply to get past the gate.

NIST SP 800-53A Revision 5 emphasizes assessing whether controls are implemented, meet their stated objectives and achieve intended outcomes. Its procedures are customizable and aimed at security and privacy controls, not at certifying self-storage operations. The useful operating principle is that configuration alone is not evidence of the outcome. A transition should be tested against its stated contract.

## A fictional two-facility example

**The following scenario and every facility, identifier, person, time, system response and outcome in it are fictional. They demonstrate the method only.**

At fictional Summit Lane Storage, customer subject `CUS-FIC-204` transfers from unit E-214 at the East facility to unit N-118 at the North facility. The approved contract allows access at both facilities from 9:00 a.m. until 6:00 p.m. on transfer day. After 6:00 p.m., North access should remain active and East access should end.

The destination grant receives a fictional provider receipt at 8:56 a.m. A North-facility readback at 9:02 a.m. shows the expected gate and building schedule. The East entitlement remains active under the approved overlap, so the record is not treated as an exception.

At 6:01 p.m., the workflow requests source revocation. The provider accepts the request, but the first readback at 6:07 p.m. still shows East access. The transition changes to **source revocation pending**, receives a reconciliation owner and schedules a review for 6:20 p.m. It is not closed merely because North access works.

The fictional second readback at 6:18 p.m. shows no East-facility entitlement for the subject while the North entitlement remains correct. The secondary-user check has a documented not-applicable disposition. The reconciliation owner closes the transition at 6:22 p.m. with both readbacks and receipts attached.

This example does not prove that any real provider processes changes on that schedule, that access attempts occurred, or that the fictional controls prevented an event. It shows how the portfolio preserves authorization, receipts, observed state and closure as different facts.

## Use the ledger as a daily control

The accompanying **Cross-Facility Access Transition Ledger** gives operations, access administration and data owners one record for the intended transition and the observed results. Use it for every move that changes facility scope, even if the rental platform presents the move as one action.

Review open transitions daily. Group them by exception class, age, provider state and reconciliation owner. Report authorized overlaps separately from unresolved dual access. Track missing readbacks separately from confirmed mismatches. Do not calculate a clean completion rate by excluding the cases with unknown outcomes.

The goal is not to add paperwork to a customer move. It is to make the system answer the question that matters: after the move, does the customer have exactly the facility access that is authorized now—and evidence that the old permission ended when it was supposed to?

<!-- BODY END -->

## Sources

- [NIST SP 800-53 Revision 5 — Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), National Institute of Standards and Technology.
- [NIST Cybersecurity Framework 2.0](https://doi.org/10.6028/NIST.CSWP.29), National Institute of Standards and Technology.
- [NIST SP 800-53A Revision 5 — Assessing Security and Privacy Controls](https://csrc.nist.gov/pubs/sp/800/53/a/r5/final), National Institute of Standards and Technology.

## Disclosure

Summit Lane Storage, customer subject CUS-FIC-204, both facilities, both units, all access records, provider receipts, timestamps, readbacks and outcomes are fictional teaching examples. They do not describe a real customer, facility, provider, product, integration, deployment, security result or access event. This article provides an operating-system framework, not legal, privacy, security or code-compliance advice. Operators must align access processes with their own agreements, approved policies, system capabilities, risk owners and applicable requirements.
