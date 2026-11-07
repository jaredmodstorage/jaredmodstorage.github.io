# AI Absence-State Contract and Validation Matrix

Use this tool for one action-relevant field at a time. It defines what the field answers, which absence states are permitted, how each state crosses the operating path, and which evidence is required before release.

## 1. Contract identity

- Contract ID and version
- Field name and human-readable label
- Exact governing question
- Facility and workflow scope
- Consequence tier
- Contract owner and approval authority

## 2. Source and semantic definition

- Governing source and stable source record ID
- Source schema and version
- Allowed value type
- Allowed semantic states
- Definition of `explicit_none`
- Definition of `not_applicable`
- Freshness window and stale trigger
- Authorization or withholding rule

## 3. Boundary preservation

For each boundary—source admission, transport, storage, transformation, retrieval, prompt assembly, policy gate, operator surface, and audit log—record:

- input representation;
- output representation;
- mapping version;
- preservation test;
- failure state;
- evidence reference.

## 4. Consequence policy

| Semantic state | Recommendation allowed? | Automated action allowed? | Required treatment |
| --- | --- | --- | --- |
| `observed_value` | Within scope | Only if separately authorized | Apply freshness and policy checks |
| `explicit_none` | For the exact governed question | Only if separately authorized | Preserve source-backed negative meaning |
| `unknown` | Review-only | No | Assign resolution owner and deadline |
| `not_collected` | Review-only | No | Decide whether collection is required |
| `not_applicable` | Only outside the non-applicable rule | No action based on absence alone | Preserve applicability basis |
| `withheld` | No inference | No | Preserve authorization boundary |
| `stale` | Review-only | No | Refresh or obtain approved exception |
| `transform_error` | No | No | Quarantine, repair mapping, and read back |

## 5. Required validation fixtures

Test omitted member, JSON `null`, empty string, `false`, zero, each approved semantic state, stale value, withheld value, unexpected type, mapping failure, and correction after a prior recommendation.

For each fixture, record schema result, mapping result, retrieved state, model interpretation, policy decision, operator label, audit evidence, and correction-propagation result.

## 6. Release gates

Release only when:

1. Every action-relevant absence has an explicit state.
2. Structural and semantic validation both pass.
3. The state survives every boundary without an undocumented default.
4. Policy blocks prohibited inference and action.
5. The operator sees a plain-language state and resolution path.
6. Correction propagation passes for every decision consumer.
7. The named release authority records the scope, evidence, limitations, and rollback.

The companion CSVs provide a blank 50-column template and an entirely fictional Cedar Vane Storage example. They do not establish a real facility, customer, deployment, incident, integration, decision, or performance result.
