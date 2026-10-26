# Portfolio Recurring Control Run Ledger

Use this tool for recurring facility work whose completion affects a portfolio decision, exception queue, comparison, release or assurance claim. It does not set a legal, regulatory, contractual, safety or inspection frequency. Adapt the control, cadence, evidence and authority fields to the organization’s approved sources.

## 1. Control definition

- Control definition ID and version
- Operating objective
- Governing procedure or instruction
- Recurrence trigger and time-zone rule
- Applicability rule and governing facility source
- Performer role and verifier role
- Evidence requirement
- Acceptance rule
- Escalation conditions
- Change, suspension and retirement authority

## 2. Generate the expected run set

For each recurrence, freeze:

- run-family ID;
- generated-at time;
- definition version;
- facility-register snapshot reference;
- expected applicable facilities or assets;
- additions, exclusions and unknowns; and
- authority for every scope disposition.

Never remove a due facility because work is late, evidence is missing or the current owner is unavailable.

## 3. One row per facility-level run

Record:

- run ID and run-family ID;
- facility stable ID and name;
- applicability state and reason;
- due-window start, end and named time zone;
- primary owner, alternate owner and verifier;
- required evidence and current evidence reference;
- performance receipt;
- verification receipt;
- run state;
- exception or miss reason;
- consequence record and operating boundary;
- next action, owner and due time; and
- final disposition and disposition time.

## 4. Allowed run states

`planned / open / submitted / verified / exception / missed / not_applicable / superseded`

Do not use `complete` unless the organization defines exactly which of those states it represents.

## 5. Rollup test

Before publishing a completion rate, answer:

- What is the expected applicable population?
- Which definition and facility snapshot produced it?
- How many runs are verified, submitted, exception, missed or unknown?
- Are not-applicable and superseded rows visible outside the numerator?
- Are stale or prior-period artifacts rejected?
- Are open consequences displayed separately from control performance?
- Can another operator reproduce the calculation from the ledger?

## 6. State boundary

A scheduled reminder does not prove performance. A submission does not prove verification. Verification of the recurring work does not prove that every discovered condition is resolved. A late recovery does not erase a missed run. Publication, compliance, safety and operating results require their own evidence and authority.

## Fictional-data rule

Any teaching row must label every facility, person, system, time, condition, action and outcome as fictional. Never use a fictional row as evidence of a real task, inspection, control, incident, customer outcome or facility result.
