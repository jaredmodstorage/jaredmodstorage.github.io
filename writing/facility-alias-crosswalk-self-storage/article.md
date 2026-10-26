# Site 14, Oak Avenue, or 7842? Build the Facility Alias Crosswalk Before You Compare the Portfolio

**Deck:** When the same property carries a different identity in every system, the portfolio does not have a reporting problem. It has an identity-control problem.

**By Jared Mastroianni**

![Jared Mastroianni and three colleagues review operating metrics in a conference room overlooking a self-storage facility.](063-operations-metrics-roundtable.png)

*Portfolio comparisons begin with knowing which source-system records refer to the same facility. Editorial image; provenance, reuse and non-documentary-use limits are recorded in the package.*

<!-- BODY START -->

A regional manager opens the property-management system and sees facility 7842. The access-control platform calls the same place Oak Avenue. Accounting uses Site 14. A repair invoice says 4100 Oak Ave. The weekly scorecard abbreviates it OAK-1.

Those labels may all refer to the same self-storage facility. They may also refer to a main building, an annex, a legal entity, a bank account, or an old property record that should no longer receive activity. Until the portfolio resolves that question, every comparison built on those records is conditional.

This is where multi-location operators get into trouble. A dashboard can look polished while invoices, work orders, access events, leads and rent data are quietly joining to the wrong property. A name match feels reasonable. An address match feels stronger. Neither is a durable portfolio key by itself. Names are shortened, addresses are reformatted, ownership changes, annexes share street names, and vendors keep labels long after an internal rename.

The answer is not to force every system to display the same name. The answer is to establish one stable internal facility key and maintain a governed crosswalk from every source-system identifier to that key.

## The label is an attribute, not the identity

Operators naturally recognize a property by the name on the sign. Software does not have that context. It sees strings and record IDs.

That distinction matters. “Oak Avenue Storage,” “Oak Ave,” and “4100 Oak Avenue” can appear to be obvious matches. But a nearby annex might use “Oak Avenue Annex.” A vendor might type only “Oak Ave” on invoices for both buildings. A management system might create a new record after an acquisition while the old record remains searchable. If the portfolio treats the display name or normalized address as the identity, an apparently successful join can be wrong.

A governed facility key should represent the operating location the company intends to manage and compare. It should not change when the marketing name, ownership entity, manager, street formatting, software vendor or reporting hierarchy changes. The key might look like `QBS-014` or another controlled internal format. The format matters less than the rules: each active operating location receives one key; the key is not recycled; and changes to descriptive attributes do not silently create a new identity.

External patterns support this separation. EPA's ENERGY STAR Portfolio Manager distinguishes its own property ID from parent, custom and standard IDs. The Federal Real Property Council requires a real-property identifier that remains stable over time and enables linkage to other systems. GS1's General Specifications identify a physical location with a unique Global Location Number. None of those sources dictates a self-storage data model. They do demonstrate the same control principle: a location can carry several identifiers, but the relationship among them must be explicit.

## Preserve source IDs instead of overwriting them

Once an internal facility key exists, the next temptation is to replace source identifiers with the new key. That destroys evidence.

The access-control system's property code, the property-management-system ID, the accounting class, the utility account, the vendor's location label and the internal facility key each answer a different question. If a manager changes the source record or strips it from imported data, the portfolio loses the ability to trace a result back to the system that produced it.

Keep the source identifier exactly as received. Store its source system, source record type, display label and effective dates. Map that record to the internal facility key in a separate crosswalk. This creates a visible chain:

`source system + source record ID -> approved alias record -> internal facility key`

That chain lets a reviewer reproduce a join, explain why a row landed at a facility and reverse a bad mapping without rewriting the original transaction. It also supports systems that legitimately use more than one facility-related code. Accounting may distinguish a legal entity from a property class. Access control may distinguish a building from an individual gate. A vendor may bill the main building and annex separately. The crosswalk should record the scope of each identifier rather than pretending all codes mean the same thing.

## Build the crosswalk as an operating control

A useful facility-alias crosswalk needs more than two columns. At minimum, record:

- the stable internal facility key;
- the source system and source record type;
- the exact source identifier and display label;
- the alias scope, such as facility, building, gate, legal entity or billing account;
- the effective-from and effective-through dates;
- the mapping status;
- the evidence used to validate the relationship;
- the owner who approved it and the approval date; and
- a change-ticket or review reference.

Effective dates are essential. A property may change vendors, ownership entities or accounting structures without changing its operating identity. A source ID may be valid through one date and replaced the next day. If the crosswalk stores only the current answer, historical reports can be remapped incorrectly.

The mapping status should also be operational, not decorative. I use five useful states:

1. **Matched:** evidence supports one source record mapping to one internal facility key for the stated scope and dates.
2. **Ambiguous:** the record could reasonably map to more than one facility or scope.
3. **Unknown:** the identifier has not been resolved.
4. **Retired:** the mapping is no longer current but remains valid for its historical period.
5. **Rejected:** review determined that the proposed relationship was wrong.

Only a matched record should flow automatically into portfolio reporting or downstream action. Ambiguous and unknown records belong in quarantine. Retired records remain available for historical reconstruction. Rejected proposals should remain visible so the same bad match is not repeatedly suggested.

## Quarantine is better than confident misallocation

An unmatched invoice or work order creates visible friction. A wrong match creates hidden damage.

Consider what happens when a vendor invoice labeled “Oak Ave” is assigned to the first facility whose name contains Oak. The expense posts. The facility's repair cost rises. A regional comparison flags the wrong property. A manager explains variance that does not belong to the site. Meanwhile, the facility that received the actual service appears to have no repair activity.

Automation raises the stakes. A misidentified facility can send a work order to the wrong manager, suppress an exception at the affected site, or trigger a customer message using the wrong access conditions. The same fuzzy match that is merely annoying in a spreadsheet becomes an execution risk when it controls action.

Quarantine should preserve the source row and make the missing decision obvious. The exception record should show the raw identifier, likely candidates, why the match failed, the accountable resolver and a due date. It should not guess silently. If the portfolio permits a provisional mapping, label it provisional, restrict what it can drive and require a human release before money, customer communication, access or maintenance action depends on it.

NIST's Cybersecurity Framework 2.0 is not a property master-data standard, but its asset-management guidance is useful here: organizations identify and manage assets, maintain inventories of data and metadata, and account for assets across their life cycles. For an operator, the practical lesson is straightforward. Facility identity is governed inventory. Someone must own it, review it and control changes.

## Resolve identity before calculating performance

A facility crosswalk should sit upstream of portfolio metrics. Do not calculate the comparison and then clean up the facilities that look strange. That makes the metric itself part of the investigation.

Instead, sequence the work:

1. ingest source records without altering their identifiers;
2. attempt a deterministic lookup against approved, effective-dated aliases;
3. quarantine unknown, ambiguous or out-of-period records;
4. have the assigned owner validate the facility and scope;
5. release the mapping through change control; and
6. calculate metrics only from eligible records.

This order creates a clean boundary between source evidence, identity resolution and portfolio interpretation. A region cannot explain a facility's performance if the underlying transactions are still changing properties during cleanup.

It also improves change management. When a new property enters the portfolio, the operating key can be established before data migration. Each source identifier is then attached deliberately. When a property is sold, the facility key is retired for new activity but preserved for history. When two adjacent facilities are operationally combined, leadership must decide whether the management unit truly changed. A shared brand name alone should not collapse two identities.

## A fictional example: Quarry Bend Storage Group

The following example is fictional and uses invented facilities, identifiers and events.

Quarry Bend Storage Group operates `QBS-014`, marketed as Quarry Bend Storage — Oak Avenue. Its property-management-system ID is `7842`, accounting class is `SITE-14`, and access-control property code is `OAK1`. A maintenance vendor submits an invoice with only “Oak Ave.”

The portfolio also operates `QBS-041`, Quarry Bend Storage — Oak Avenue Annex, two blocks away. Both properties have used the abbreviated vendor label “Oak Ave” in prior emails. The invoice includes no unit range, gate code, service address or work-order reference.

The crosswalk does not resolve the invoice by choosing the first Oak Avenue result. It marks the vendor alias ambiguous and quarantines the row. The assigned facilities coordinator requests the service address and work-order number. The vendor confirms the repair occurred at the annex. The coordinator creates a matched vendor-location alias for `QBS-041`, limited to that vendor account and effective from the verified contract date. A second reviewer approves the mapping. The source invoice label remains unchanged.

That resolution proves only which facility the reviewed vendor record refers to. It does not prove the invoice is accurate, authorized, paid, posted or reconciled. Those are separate controls.

## Use the Facility Identity and Alias Crosswalk

The package accompanying this article includes a blank crosswalk template and the fictional Quarry Bend example. Start with the systems that drive the most consequential action: property management, accounting, access control, work orders, utilities and recurring vendors.

For each source, export the native identifier and display label. Do not begin by cleaning the labels. First determine whether an approved mapping already exists for the transaction date and scope. Route exceptions to an owner who can inspect contracts, source records, service addresses, acquisition files and operating evidence. Record the decision, reviewer and effective period.

Then test the control with deliberately difficult cases: a renamed property, a sold property, a main building and annex on the same street, a vendor abbreviation, an old accounting class and a source record outside its effective dates. The purpose is not to prove that the clean rows match. It is to prove that the uncertain rows stop.

A portfolio becomes comparable only after its records refer to the facilities leadership thinks they refer to. The facility alias crosswalk is not clerical cleanup. It is the identity layer that keeps reporting, reconciliation and automation attached to the right place.

<!-- BODY END -->

---

## Practical operator tool

Use the accompanying **Facility Identity and Alias Crosswalk** to govern current and historical source identifiers, quarantine ambiguity and preserve approval evidence. The blank CSV is implementation-ready; the completed CSV is explicitly fictional.

## Sources and limitations

The article draws on current EPA ENERGY STAR Portfolio Manager guidance, the Federal Real Property Council's FY 2026 reporting dictionary, GS1 location-identification guidance and NIST CSF 2.0. These are authoritative examples of identifier and lifecycle controls, not self-storage regulations or proof that a specific operator must adopt any external identifier standard. Full provenance, access dates, HTTP outcomes and material limitations are recorded in `source-register.csv`.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.
