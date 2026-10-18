# Portfolio Equipment Hierarchy and Service Map

Use this card before a service event becomes portfolio evidence. The control separates equipment identity, instance lifecycle, work scope, and release authority.

## 1. Define the hierarchy

| Level | Required identifier | Operating question | Rule |
|---|---|---|---|
| Facility | `facility_id` | Which property owns the record? | Use the governed facility ID. |
| System | `system_id` | Which operating capability is affected? | Examples: vehicle access, HVAC, life safety. |
| Functional asset | `asset_id` | Which equipment unit performs the function? | Keep identity stable through component replacement. |
| Maintainable component | `component_id` | Which independently serviced part is involved? | Track only where a separate decision is useful. |
| Installed instance | `instance_id` | Which specific physical item was in service? | Never overwrite a predecessor with successor identity. |

## 2. Validate the identity chain

- [ ] Every object has a unique ID and object class.
- [ ] Every non-facility object has a valid parent ID.
- [ ] Facility and location agree with the parent chain.
- [ ] Manufacturer, model, and serial number are supported by evidence or marked `unknown` with a reason.
- [ ] Exactly one current installed instance exists for a single-instance component.
- [ ] Installation and retirement intervals do not overlap unless the configuration intentionally permits parallel instances.

## 3. Classify the work

- Work target ID and level:
- Condition observed:
- Work type: inspect / adjust / repair / replace / test / retire / other
- Exact scope:
- Parts changed:
- Evidence reference:
- Performer:
- Observer:
- Start and completion times:

## 4. If replacement occurred

- [ ] Predecessor instance is preserved and retired.
- [ ] Successor instance receives a new ID.
- [ ] Replacement event links predecessor and successor.
- [ ] Verified successor manufacturer/model/serial are recorded; unverified values remain unknown.
- [ ] Warranty or capital records reference the correct instance.

## 5. Release only what was verified

| Release boundary | Required evidence | Allowed state |
|---|---|---|
| Component | Component-level observation or test | released / limited / hold / unknown |
| Functional asset | Authorized asset functional test | released / limited / hold / unknown |
| System | Authorized end-to-end system verification | released / limited / hold / unknown |

Do not infer parent release from child work completion.

## 6. Set comparison eligibility

- Comparison class:
- Required identity fields complete: yes / no
- Exposure interval known: yes / no
- Open identity or evidence variance:
- Variance owner and due time:
- Permitted use: eligible / limited use / hold / reject
- Correction or superseding record:

## Close rule

No service closure without the exact work target. No replacement closure without predecessor and successor instances. No higher-level release without evidence for that level.
