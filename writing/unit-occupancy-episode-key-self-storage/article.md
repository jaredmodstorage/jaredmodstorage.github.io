# The Unit Number Did Not Change. The Occupancy Did.

## A time-bounded occupancy episode keeps one customer’s history from following the next customer through a multi-location self-storage system

By Jared Mastroianni

A unit number feels permanent. B-214 is still B-214 after one customer moves out, another transfers in and a third rents it online. That stability is useful for finding the door. It is dangerous when software treats the door label as the identity of every relationship that has ever touched it.

In a multi-location portfolio, the same unit can accumulate access credentials, balances, photographs, protection-plan records, incident notes, maintenance history and customer communications. Those records do not all belong to the physical unit forever. Many belong to one specific period in which one customer had a defined relationship to that unit.

The missing operating object is the **unit-occupancy episode**: a durable identifier for one bounded occupancy relationship at one facility, tied to explicit effective dates and source records. The unit identifies the space. The customer identifies a party. The episode identifies which customer-unit relationship was active at a particular time.

Without that third identity, old history can quietly become current history.

## A plausible failure that looks like a data-quality problem

Consider a fictional three-site portfolio. At Harbor North, customer A vacates unit B-214 on March 3. An inspection photo is uploaded the next morning. Customer B transfers into B-214 on March 5 and receives a new access credential. Two weeks later, a regional operator opens the current-unit view and sees a late fee, a gate exception and an interior photo together.

All three records say B-214. Only one belongs to customer B.

The late fee belongs to customer A’s closed agreement. The gate exception belongs to customer B. The photo records the empty-unit inspection between the two occupancies. A report joined those records on facility and unit number, then displayed them as one current story.

Nothing in that example requires a broken database. Every source record can be accurate. The failure is the relationship model: a stable place was mistaken for a stable occupancy.

That distinction matters beyond reporting. It can affect collections work, access review, incident response, transfer handling, customer service and privacy. An operator should not have to infer ownership from timestamps and narrative notes while a customer is waiting.

## Three identities, not one overloaded field

A defensible design separates three things.

**Physical unit identity** answers, “Which space is this?” It should survive customer turnover. If a unit is split, merged, renumbered or materially redefined, that is a separate physical-identity cutover problem.

**Party identity** answers, “Which person or organization is involved?” It can span facilities and multiple agreements. It should not be reconstructed from a name, email address or phone number alone.

**Occupancy episode identity** answers, “Which bounded customer-unit relationship does this record concern?” It starts and ends under explicit rules. It can link to an agreement, a transfer predecessor or successor, access credentials, charges and operational evidence without pretending that those items belong permanently to the door.

This is not merely a new column. It is a contract for how systems establish, use and retire a relationship.

## Define the episode boundary before building the join

Teams often agree that they need an episode identifier, then disagree about when the episode begins. Is it reservation time, agreement signature, access enablement, scheduled move-in or confirmed possession? The correct answer depends on the decision being supported.

That is why one timestamp should not carry every meaning. The register should preserve several events when they exist:

- agreement created;
- occupancy effective from;
- access enabled;
- possession or move-in confirmed;
- transfer initiated and completed;
- move-out or vacancy observed;
- occupancy effective through;
- access revoked; and
- financial or claim resolution completed.

The episode’s operating boundary should be explicit and consistent. Separate events can remain visible without forcing them to collapse into one “start date” or “move-out date.”

Use fully qualified timestamps with offsets or UTC for exchanged records. RFC 3339 exists to improve consistency and interoperability in Internet timestamps. A local display time may help the operator, but the stored event should remain unambiguous across sites, daylight-saving changes and system handoffs.

## Transfers are linked episodes, not an address edit

A transfer is where weak identity models become obvious. Customer B moves from A-107 to B-214. If the software simply changes the unit field on one continuing record, the old and new relationships can blur together. Which door did a photo describe? Which credential opened which area? Which rate and protection selection applied before the transfer? Which unit should receive a later maintenance note?

A cleaner pattern closes or supersedes the A-107 episode and creates a new B-214 episode. The two episodes are linked by a transfer identifier and direction. The customer relationship may continue, while the occupancy identity changes.

That preserves continuity without erasing the boundary.

The same rule helps when a transfer is reversed, partially completed or corrected after the fact. Do not overwrite the earlier episode into the shape of the final outcome. Preserve what was recorded, what became effective, what was corrected and who authorized the correction.

## Every linked record needs an episode test

Before a system attaches a record to the current occupancy, it should pass a small linkage test:

1. Does the record carry a valid facility and physical-unit identifier?
2. Does it carry an episode identifier from its source?
3. If not, can the episode be derived unambiguously from the event’s effective time and source relationship?
4. Does that episode own this type of record under the operating contract?
5. If two episodes are plausible, is the record held as an exception instead of silently choosing the current one?

The fourth question prevents overreach. A door-repair work order may belong to the physical unit, not to the customer occupancy. A customer promise-to-pay belongs to the party and agreement. A move-out inspection may belong to the closing episode, the unit-readiness interval or both through explicit links. The right identity depends on the object and the decision.

W3C’s PROV Data Model offers a useful general principle here: provenance describes entities, activities, responsible agents and time, and it supports links among things that refer to the same underlying subject. It does not prescribe a self-storage schema. It does reinforce why a system should preserve which record was produced by which activity, when and under whose responsibility rather than flattening every event into the latest unit row.

## Store effective time and recorded time

Multi-location operations receive late-arriving records. A manager may confirm a March 3 move-out on March 4. An access platform may deliver an offline event after connectivity returns. A correction may be entered days later with an earlier effective date.

For consequential records, preserve at least two clocks:

- **effective time**: when the event is understood to have applied operationally; and
- **recorded time**: when the system received or saved that assertion.

Also preserve the source, actor, reason and superseded record when a correction changes a boundary. That makes it possible to answer two different questions: “What do we now believe was true on March 3?” and “What did the operation know at noon on March 3?”

Those answers are not interchangeable during an incident review, customer dispute or automation audit.

## The minimum episode contract

An operator does not need a perfect enterprise model to begin. A practical unit-occupancy episode register can start with:

- facility ID and physical-unit ID;
- occupancy episode ID;
- party/customer ID and agreement ID;
- episode state;
- effective-from and effective-through timestamps;
- source system and source record ID;
- predecessor and successor episode IDs;
- transfer ID when applicable;
- access-enable and access-revoke timestamps;
- recorded time, last correction time and correction owner; and
- exception state with a named resolution owner.

The companion template in this package includes those fields and a linkage checklist. Its example is fictional. It is intended as a diagnostic starting point, not a claim that every property-management or access system exposes the same fields.

Privacy belongs inside the design. NIST describes its Privacy Framework as a voluntary tool for identifying and managing privacy risk. Applied here, the lesson is bounded: collect and expose the identifiers needed for a legitimate operating purpose, restrict who can see customer-linked history, and do not make a broader customer profile merely because systems can be joined.

## Release current-state views only when the episode is clear

A “current unit” screen should not mean “all records sharing this unit label.” It should mean records authorized for the active episode, plus clearly separated physical-unit history where the operating purpose requires it.

Set a release condition for current-state views and automated actions:

- exactly one active episode is identified for the decision time;
- its effective boundary is valid;
- linked customer records resolve to that episode or an explicitly permitted parent relationship;
- physical-unit-only records are labeled as such;
- ambiguous and late-arriving records remain exceptions; and
- a named owner can correct the linkage without destroying prior evidence.

If those conditions are not met, the system should show **occupancy unresolved**, not guess from the most recent customer name or the unit’s present status.

This is especially important for automation. A model or rules engine can summarize records only after the relationship boundary is trustworthy. It should not convert “same unit number” into “same customer context.” No output should trigger access, collections, customer communication or incident escalation merely because a join happened to return one row.

## A portfolio test operators can run now

Choose one unit with at least two historical occupancies and one transfer. Pull its records from the property-management, access, payment, communication, inspection and maintenance systems. For each record, ask:

- Is this about the space, the customer, the agreement or one occupancy episode?
- What source identifier proves that relationship?
- What effective time places it inside or outside the episode?
- Could the same join attach it to the next customer?
- Who owns the exception if the answer is unclear?

Run the test at more than one facility. Local workarounds often hide in free-text notes, reused unit labels or site-specific transfer practices. The goal is not to force every record into an episode. The goal is to stop accidental linkage and make deliberate linkage explainable.

A unit number is a locator. It is not a customer-history key. Once a portfolio gives each occupancy its own bounded identity, the door can keep its familiar label without carrying the last customer into the next customer’s story.

## Sources

1. World Wide Web Consortium, “PROV-DM: The PROV Data Model,” W3C Recommendation, April 30, 2013. https://www.w3.org/TR/prov-dm/
2. RFC Editor, “RFC 3339: Date and Time on the Internet: Timestamps,” July 2002. https://www.rfc-editor.org/rfc/rfc3339
3. National Institute of Standards and Technology, “Privacy Framework,” accessed October 3, 2026. https://www.nist.gov/privacy-framework

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.
