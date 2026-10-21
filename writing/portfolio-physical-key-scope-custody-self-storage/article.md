# The Key Ring Says “Master.” Which Doors Does It Actually Open?

**Deck:** A portfolio cannot govern physical keys with labels and memory. It needs a controlled relationship among each key copy, the locks it is expected to operate, the person holding it and the current authorization behind that possession.

**By Jared Mastroianni**

![Four self-storage leaders compare operating practices during an industry conference roundtable.](066-industry-conference-peer-roundtable.png)

*Portfolio discipline improves when experienced operators compare the control behind the label. Editorial image; provenance and non-documentary-use limits are recorded in the package.*

<!-- BODY START -->

A regional leader opens a facility key cabinet and finds a ring tagged `MASTER`. The site manager says it opens “pretty much everything.” The regional leader asks which buildings, offices, mechanical rooms and vacant-unit cylinders are in scope. No one can answer without walking the property.

The ring is present. Its authority, scope and copy history are not.

That is the physical-key problem in many portfolios. The metal is easy to see, so the organization mistakes possession for control. A handwritten label becomes a substitute for a lock map. A former manager’s assurance becomes the copy count. A returned ring becomes proof that access ended, even though no one knows whether another copy exists.

A multi-location operator needs a more exact operating model. Every governed key copy should connect five things: a stable identity, the locks it is expected to operate, its current holder or controlled storage location, the authorization for that custody and the events that changed its state. “Master” can remain a useful local description. It cannot remain the system of record.

## Treat the key, the key pattern and the key ring as different objects

Three physical objects are often collapsed into one field.

A **key pattern or system** describes the relationship that allows one or more keys to operate one or more locks. A **key copy** is an individual physical item that can be issued, returned, lost or destroyed. A **key set or ring** is a collection of copies assembled for a role or assignment.

Those distinctions matter. A ring may be returned while one copy from the same key system remains outstanding. A lock may be rekeyed while the label on the ring stays the same. Two keys on one ring may have different facility scopes, expiration dates and loss responses. If the data model has only `master_key = yes`, none of those conditions can be represented honestly.

Assign stable internal identifiers to the facility, controlled opening, lock or core group, key system, individual copy and key set. Link them rather than forcing them into a single description. The register should answer: which exact copy is this, where is it now, who is responsible for it, which controlled openings is it believed to operate, what evidence supports that mapping and when was the relationship last verified?

Do not turn the ordinary operating register into a public blueprint. Detailed bitting, cut codes and unnecessarily sensitive security information should remain in the more restricted system designated by the operator and qualified security or locksmith professionals. The operating layer needs enough detail to control custody and exceptions without broadly exposing how to reproduce or defeat a key.

## Make scope a maintained relationship, not a nickname

The words `office`, `maintenance`, `vacant unit` and `master` describe intent. They do not prove scope.

For each copy, maintain an approved relationship to specific controlled openings or to a precisely defined lock group. A group should have its own identifier, owner and version. “All exterior doors” is useful only if the portfolio can show which doors currently belong to that group. When a new building is added, a core is replaced or an office door is moved to a different system, update the relationship rather than assuming the old label expanded automatically.

Record the scope source and verification method. That may be an approved locksmith schedule, a controlled lock inventory, a commissioned site survey or another operator-approved record. Record what is unknown. If a manager has not tested a key against every door, the register should not silently convert belief into fact.

This creates an important operational separation:

- `expected_scope` states what the approved design says the key should operate.
- `verified_scope` states what an authorized check actually confirmed.
- `exception_scope` states where the two disagree or remain unknown.

The portfolio can then route discrepancies without teaching staff to “try the key everywhere.” Verification must follow the operator’s safety, privacy and access procedures, especially around electrical, mechanical, communications and customer areas.

## Separate possession from authorization

A person can physically possess a key without retaining current authority to use it. That is why a custody register needs both a holder and an authorization source.

Record the approved role or individual, business purpose, authorizer, issue time, expected return or review date and any time or location restriction. A key assigned to the on-call manager for one weekend is not the same authorization as a standing facilities assignment. A vendor receiving a key for a defined service window is not a member of staff with continuing access.

Transfers, reassignments, leave, termination, role changes and vendor completion should trigger a review of physical-key authorization. NIST SP 800-171 Revision 3 discusses returning old and issuing new keys or building passes during personnel transfers and reassignments. That publication is written for protecting Controlled Unclassified Information, not for self-storage operations, but the control distinction is useful: a change in role can require a change in physical access, even when employment continues.

Do not close the transition when someone says, “I asked for the keys.” Close the custody event only when the assigned evidence exists. If the item is not returned, preserve `overdue` or `unresolved` and activate the operator’s response path. A missing key may require a qualified assessment of affected locks, not an optimistic note.

## Control duplication as its own workflow

The number stamped on a tag is not a copy count.

Define who may request a new copy, who may approve it, which vendor may produce it, who may receive it and how the new copy enters inventory. Give each authorized copy its own identifier before issue. Reconcile the request, production record, receipt and assignment. If the vendor cannot confirm historical duplicates, keep the historical copy count unknown.

Never infer “no duplicates” because no duplicate is visible. The register should carry separate values for `expected_copy_count`, `verified_copy_count`, `unresolved_copy_count` and `count_verified_at`. This lets the portfolio distinguish an ordinary inventory variance from a material access exception.

The same discipline applies to emergency boxes, vehicle rings, contractor sets and keys stored off site. A key is not controlled merely because it is “in the lockbox.” The lockbox needs a stable location, accountable owner, authorized opener list, access log or check record where required, and a defined response when the box itself cannot be reconciled.

## Use states that describe the lifecycle

A useful key lifecycle is more precise than `active` and `inactive`. Consider states such as:

1. `requested`
2. `approved_for_production`
3. `produced`
4. `received_into_custody`
5. `stored`
6. `issued`
7. `return_due`
8. `returned`
9. `quarantined`
10. `lost_or_stolen`
11. `destroyed`
12. `unknown`

Each transition should record time, actor, evidence and next owner. `Returned` means the identified copy was received, not that every copy of its pattern has been recovered. `Destroyed` means the approved destruction event was completed, not that an email requested it. `Unknown` is not a softer version of `stored`; it is an exception.

Locks need lifecycle records too. When a core, cylinder or locking device changes, record its effective time and predecessor. End the old key-to-lock relationship and start the new one. Otherwise the portfolio may report a key as active against a lock it can no longer operate—or worse, report access as ended while an unchanged lock still accepts an unreturned copy.

## Measure exceptions, not just inventory

A portfolio dashboard should not celebrate having 412 keys in the register. It should expose the conditions that require action.

Useful measures include:

- issued copies past their return or review date;
- copies whose holder lacks a current authorization;
- active locks linked to former employees or completed vendors;
- keys with unknown location, scope or duplicate count;
- lock changes not reconciled to affected key relationships;
- storage containers whose own access review is overdue;
- facility records that have not completed the current attestation cycle; and
- production records that do not reconcile to received copies.

These are exception measures, not security guarantees. A zero count means the register has no open exception under the configured rules and available evidence. It does not prove that an unauthorized copy cannot exist.

NIST SP 800-171 Revision 3 calls for maintaining and reviewing physical access authorizations, removing people when access is no longer required, maintaining physical access logs and securing keys and other physical access devices. Again, its formal scope is CUI protection. Self-storage operators can borrow the architecture of authorization, review, logging and device security without claiming NIST compliance or turning federal guidance into an industry mandate.

## A fictional portfolio example

**Everything in this example—including the company, facilities, people, identifiers, dates, evidence and outcomes—is fictional and exists only to demonstrate the method.**

Fictional Orchard Current Storage Group operates fictional facilities `FIC-OC-011`, `FIC-OC-024` and `FIC-OC-031`. Regional manager Tessa Vale transfers to a different region. Her ring is labeled `REGIONAL MASTER` and is returned to the operations office.

The portfolio does not close the transition on the ring’s return. The register shows three individual copies on the ring. Copy `FIC-KC-208` has an approved relationship to the offices and mechanical closets at facilities 011 and 024. Copy `FIC-KC-209` is expected to operate vacant-unit cylinders at facility 024, but its last scope verification predates a lock change. Copy `FIC-KC-210` is labeled for facility 031, yet its stable lock-group relationship is blank.

The return event closes Tessa’s custody of all three identified copies. It does not prove that no duplicates exist. The transfer workflow expires her authorization, places the ring in controlled storage and creates two exceptions: reconcile `FIC-KC-209` to the post-change cylinder group, and establish or retire the unknown scope for `FIC-KC-210`.

The fictional qualified locksmith record confirms that the facility 024 change ended the old relationship for `FIC-KC-209`. The portfolio records the superseded lock group and quarantines the obsolete copy for approved destruction. Facility 031 has no reliable source for `FIC-KC-210`, so the operator keeps its scope `unknown` and routes a qualified assessment. It does not test the key casually or assert that access ended.

No real customer, employee, vendor, facility, deployment, loss, security incident or performance result is represented in this example.

## Start with one key class and one region

The accompanying **Portfolio Physical-Key Scope and Custody Register** is deliberately structured as a relationship model, not a key list. Start with a bounded class—regional and facility masters, for example—and one accountable region.

Inventory the copies that are physically present. Assign stable IDs without renaming the locks. Link each copy to a controlled key system and scope record. Reconcile its holder, storage location, authorization and lifecycle state. Preserve unknowns. Then work outward to duplicates, vendor sets, emergency boxes and lower-level keys according to risk and operational need.

Set a review cadence and event triggers. Personnel transitions, locksmith work, new construction, acquisitions, facility transfers, lost-key reports and unexplained scope discrepancies should all create a governed review. Require the system to show the previous state, the approved change and the readback after implementation.

The goal is not to build the largest key spreadsheet in the industry. It is to make one physical fact answerable across the portfolio: which controlled openings can this exact copy reach, why is it where it is, and what evidence says that authority is still current?

Until those questions have structured answers, `MASTER` is not a control. It is a warning label.

<!-- BODY END -->

## Sources

- [NIST Special Publication 800-171 Revision 3 — Protecting Controlled Unclassified Information in Nonfederal Systems and Organizations](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/800-171r3/NIST.SP.800-171r3.html), National Institute of Standards and Technology.
- [NIST Special Publication 800-53 Revision 5 — Security and Privacy Controls for Information Systems and Organizations](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final), National Institute of Standards and Technology.
- [Facility Access Control: An Interagency Security Committee Best Practice](https://www.cisa.gov/sites/default/files/2025-02/Facility%20Access%20Control%20-%20An%20Interagency%20Security%20Committee%20Best%20Practice-02-20.pdf), Cybersecurity and Infrastructure Security Agency / Interagency Security Committee.

## Disclosure

Orchard Current Storage Group, every facility, person, identifier, key, lock relationship, date, record, decision and outcome in the example are fictional. They do not describe a real operator, deployment, security event, customer, employee, vendor, performance result or legal conclusion. The cited federal publications address federal facilities, federal information systems or Controlled Unclassified Information within their stated scopes; this article uses their control distinctions as architecture references and does not claim that they impose self-storage requirements, establish legal compliance or confer a certification. Operators should follow applicable law, contracts, company policies and qualified security and locksmith guidance.
