# Incident-Family Review Checklist

Use this checklist only when an operating event produces multiple records, crosses systems or functions, or supports a consequential portfolio conclusion. A routine isolated task with clear scope and completion does not need an incident family.

## 1. Open a candidate family

- [ ] Assign a durable family ID without changing any source record.
- [ ] Record facility, local timezone, affected asset or service, candidate time window and affected audience.
- [ ] Link every source record by its original system and identifier.
- [ ] Preserve direct observations separately from theories and copied summaries.

## 2. Test membership

For every proposed member, answer:

- [ ] Same facility, asset, lane or service area?
- [ ] Same plausible time window after timezone normalization?
- [ ] Same observable condition, downstream effect or operating consequence?
- [ ] Established dependency, suspected dependency or no known dependency?
- [ ] Same affected audience or decision?

The result must be one of:

- **Link:** possible relationship; separate incident status remains.
- **Merge:** evidence supports one bounded operating episode.
- **Split:** later evidence supports a different episode, scope or asset.

Record the decision, rationale, owner, timestamp and evidence reviewed.

## 3. Separate the facts

- [ ] Signal or direct observation
- [ ] Workflow record created from the signal
- [ ] Bounded incident scope
- [ ] Verified operational impact
- [ ] Suspected cause, clearly labeled
- [ ] Verified cause or explicit unknown
- [ ] Containment
- [ ] Correction
- [ ] Release test and evidence

## 4. Review clocks independently

- [ ] First verified affected time
- [ ] First portfolio awareness time
- [ ] Containment time
- [ ] First verified restored time
- [ ] Family close time
- [ ] Unknown bounds and timezone limitations preserved

Do not substitute ticket creation, alert clearance or a completion click for an unobserved operating time.

## 5. Release the family

Release only when all applicable conditions are satisfied:

- [ ] Scope and audience are explicit.
- [ ] Impact and restoration evidence are recorded, with limitations.
- [ ] Temporary controls are removed or transferred to a named owner.
- [ ] Required facility checks pass.
- [ ] Open cause or follow-up questions have owners and dates.
- [ ] The authorized release owner records the decision and timestamp.

Allowed family states:

- **CANDIDATE / REVIEWING**
- **CONFIRMED / CONTAINED**
- **OPERATIONALLY RESTORED / FOLLOW-UP OPEN**
- **CLOSED**
- **SPLIT**
- **CANCELLED AS NON-INCIDENT**

## 6. Report without double-counting

Report separately:

- incident families;
- customer contacts;
- device alerts;
- vendor dispatches;
- affected facilities, assets and audiences; and
- each named duration clock.

Never convert the number of member records into the number of operating incidents.
