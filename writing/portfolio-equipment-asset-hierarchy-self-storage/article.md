# The Gate Was Fixed. Which Asset Changed?

## A portfolio equipment hierarchy for comparing maintenance without flattening systems, components, and replacements into one vague record

By Jared Mastroianni

“Gate repaired” is a reasonable note at the end of a hectic shift. It is not enough information to manage equipment across a portfolio.

The phrase could mean a technician adjusted a hinge, replaced a vehicle-loop detector, reset a controller, installed a new operator, repaired the gate leaf, or restored communication between the access system and the opener. Those actions have different costs, failure patterns, service lives, and follow-up requirements. If every one of them lands in the same maintenance category, the portfolio does not have comparable history. It has a stack of stories that happen to use the same noun.

The answer is not a longer free-text field. It is an equipment hierarchy that tells the team exactly what physical thing a work event affected.

For a self-storage operator, a useful hierarchy can be simple:

**Facility → system → functional asset → maintainable component → installed instance**

That structure turns a work order from “something happened to the gate” into a traceable event against a defined piece of equipment. It also prevents a common reporting mistake: treating a component repair, an asset replacement, and a system return-to-service as if they were the same operating state.

## Start with the physical question

Before standardizing failure codes or building a dashboard, ask one question:

> What is the smallest physical item we need to identify separately to make a maintenance, replacement, warranty, safety, or capital decision?

That boundary will vary by equipment class. A roll-up door may need separate records for the curtain, guides, spring assembly, bottom bar, latch, and installed door instance. A vehicle gate may need a gate leaf, operator, controller, credential reader, safety devices, and loop detectors. An HVAC system may need an air-handling unit, compressor, fan motor, thermostat, and filter class.

Not every bolt needs an asset ID. The hierarchy should stop where the operating decision stops. If the team never services, replaces, warrants, or compares a piece independently, it may remain an attribute of its parent. If it has its own maintenance history, serial number, expected life, inspection requirement, or replacement decision, it deserves its own identity.

This is a management design choice, not a claim that one taxonomy fits every portfolio.

## Separate the five levels

The levels have different jobs.

**Facility** identifies the operating location. Use the governed facility ID, not a nickname that can drift.

**System** is the operating capability: vehicle access, life safety, HVAC, surveillance, elevators, lighting, or building envelope. A system can contain several assets that must work together.

**Functional asset** is an equipment unit that performs a defined function: entry gate, exit gate, rooftop unit, elevator, fire-alarm panel, or camera recorder.

**Maintainable component** is a part that the operator chooses to track independently because it can fail, be serviced, or be replaced: gate operator, loop detector, compressor, contactor, reader, or power supply.

**Installed instance** is the specific physical item in service during a bounded period. Model and serial number belong here when verified. If a gate operator is replaced, the asset may remain “Entry Gate 01,” but the installed operator instance changes.

This final distinction is what keeps replacement history honest. Editing the old record to show the new serial number erases the predecessor. A replacement should retire one instance and begin another, with both connected to the same parent component or asset.

ISO 55000:2024 provides vocabulary, principles, and an organizational framework for managing assets across their life cycles. It does not publish a self-storage equipment schema on its public page. The practical implication here is narrower: lifecycle history needs stable identities if an operator wants decisions to remain explainable after equipment changes.

## Use parent-child relationships, not one flat asset list

A flat list creates ambiguous peers. “Gate 1,” “Gate motor,” “Keypad,” and “Loop” may appear as four unrelated records even though they form one vehicle-access path.

Every record should therefore carry:

- its own unique ID;
- its object class;
- its parent ID;
- facility ID;
- location within the facility;
- status and effective dates; and
- the evidence supporting its identity.

The National Institute of Building Sciences’ public COBie material separates facility, type, component, system, attribute, job, and event data and emphasizes unique keys. A self-storage operator does not need to adopt COBie wholesale to use that sound idea. Systems, components, work, and events should not be collapsed into one description field.

Parent-child rules should be explicit. A component can belong to one current parent in the operating hierarchy. A system may contain many functional assets. An installed instance must have an installation date or a declared unknown-start state. A retired instance cannot receive new completed work after its retirement time unless the record is clearly a late correction.

Those rules make bad joins visible before they become bad conclusions.

## Put work at the level actually touched

Each service event should identify both its **work target** and its **release boundary**.

The work target is the item inspected, adjusted, repaired, or replaced. The release boundary is the larger item that was actually verified ready for use.

If a technician replaces an operator control board, the work target may be the board instance. If the technician then performs an authorized functional test of the complete entry gate, the release boundary may be the functional asset. If no system-level test was performed, the vehicle-access system should not automatically be marked fully released.

This protects the portfolio from upward inference:

- a completed component task does not prove the asset works;
- an operating asset does not prove every sibling component is healthy;
- a functioning entry gate does not prove the exit gate works; and
- an invoice description does not prove the physical identity of the item serviced.

The record should preserve who observed the condition, who performed the work, what evidence was attached, and who had authority to release the relevant level. Those may be different people.

## Record replacement as a transition

Replacement is not an edit. It is a transition with at least four facts:

1. The predecessor instance stopped being the current item.
2. The successor instance became current.
3. A work event connected the transition.
4. Evidence supported the identity and timing of both states.

Use installation and retirement timestamps with an explicit time basis. Preserve the old model, serial number, and evidence. If the serial number is unreadable, record `unknown` and the reason; do not infer it from the invoice or another facility’s equipment.

The W3C PROV data model offers a useful general pattern for this history: entities can be generated, invalidated, derived, and associated with activities and agents. It is not a maintenance standard, but it reinforces a practical point. The old physical instance, the new physical instance, and the replacement activity are different records.

This distinction also improves warranty and capital review. The operator can see whether repeated work followed the same installed instance or occurred across successive replacements. Without instance intervals, a dashboard may attribute a predecessor’s failures to its successor—or make a troubled asset look new simply because its serial number was overwritten.

## Compare like with like

Once the hierarchy is stable, portfolio comparison becomes more defensible.

Compare failure and cost at the level that matches the question:

- System: Which facilities have the most vehicle-access downtime?
- Functional asset: Which entry gates require the most service visits?
- Component class: Which gate-operator models have repeated corrective work?
- Installed instance: Did this specific operator require another repair within its current service interval?

Keep denominators aligned. Cost per gate operator requires a known population of current operator instances. Failure rate by model requires verified model identity and exposure time. A count of work orders labeled “gate” cannot support either calculation.

Unknowns should remain visible. An asset with no serial number is not the same as a duplicate asset. A component not represented in the register is not proof that the facility lacks it. A closed work order is not proof that the equipment passed a release test.

## A fictional portfolio example

Consider the explicitly fictional Juniper Span Storage Group. Two facilities each close a work order with the note “gate repaired.”

At fictional facility `JSS-FIC-01`, the work target is installed gate-operator instance `JSS-FIC-01-VA-ENT-01-OP-002`. The prior operator instance is retired, the successor’s verified model and serial number are recorded, and the replacement event links both. A qualified owner records a separate functional release of entry-gate asset `JSS-FIC-01-VA-ENT-01`. The credential reader and safety-device components remain unchanged.

At fictional facility `JSS-FIC-02`, a vendor adjusts the entry gate leaf’s hinge assembly. No component instance is replaced. The work target is the hinge assembly, the gate leaf remains the same installed instance, and the service evidence supports only the documented adjustment and authorized release.

Both notes could fit under “gate repaired.” They are not comparable replacement events. One changes an operator instance; the other preserves the existing hierarchy and records an adjustment. The example is instructional and does not describe a real customer, deployment, vendor, or result.

## The Portfolio Equipment Hierarchy and Service Map

Use one governed register for the equipment structure and one event section for work history. At minimum, capture:

### Identity

- Facility ID, system ID, functional asset ID, component ID, and instance ID
- Object class and parent ID
- Governed name and facility location
- Equipment type, manufacturer, model, and serial number, with unknowns explicit

### Lifecycle

- Install, in-service, out-of-service, and retirement times
- Current-state flag and state reason
- Predecessor and successor instance IDs
- Evidence reference and verification owner

### Service event

- Work-event ID and target level
- Condition, work type, and exact scope
- Parts replaced and resulting instance transition
- Start, completion, and evidence times
- Performer, observer, reviewer, and release authority

### Release and comparison

- Release boundary: component, asset, or system
- Test or observation performed
- Released, limited use, hold, or unknown
- Permitted comparison class
- Open variance, owner, due time, and correction link

The accompanying template includes validation rules and a fictional worked example. Start with one consequential equipment class—vehicle access, HVAC, elevators, or life safety—before trying to inventory every object on every property.

## Make the hierarchy part of the work, not cleanup after it

The hierarchy should be selected when the work request is opened, confirmed when service begins, and updated when equipment changes. If asset identity is added weeks later during reporting, the portfolio will rely on memory and invoice wording.

Build three simple controls into the workflow:

1. No service closure without a work target at the correct hierarchy level.
2. No replacement closure without predecessor and successor instance records.
3. No higher-level release without evidence from the authorized test or observation for that level.

This is not about turning facility managers into database administrators. It is about making a physical maintenance decision survive translation from the property to the portfolio.

“The gate was fixed” may be enough to end a phone call. It is not enough to compare failure patterns, validate warranty history, plan capital, or know what equipment is actually in service. Name the system. Name the asset. Name the component. Preserve the instance that changed.

## Sources

- [ISO, *ISO 55000:2024 — Asset management — Vocabulary, overview and principles*](https://www.iso.org/cms/%20render/live/en/sites/isoorg/contents/data/standard/08/30/83053.html?browse=tc)
- [ISO/TC 251, *Asset Management*](https://committee.iso.org/home/tc251)
- [National Institute of Building Sciences, *COBie V3: Structure and Format*](https://nibs.org/nbims/v3/cobie/1-4/)
- [W3C, *PROV-DM: The PROV Data Model*](https://www.w3.org/TR/prov-dm/)

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

*Editorial disclosure: The operating method and fictional example are instructional. They do not report a customer deployment, product capability, performance result, certification, or industry standard.*
