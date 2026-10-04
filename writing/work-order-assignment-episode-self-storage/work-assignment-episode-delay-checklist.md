# Work-Assignment Episode Delay Checklist

Use this checklist before assigning delay to a person, team, queue or vendor.

## Identity and sequence

- Confirm the exact facility and work-order identifiers.
- List every assignment episode in sequence.
- Verify each episode's owner type and owner identifier.
- Link each episode to its predecessor and successor.
- Flag unexplained gaps, overlaps and duplicate sequence numbers.

## Route, acknowledgement and acceptance

- Record when the work was routed.
- Record when it became available to the destination, if known.
- Keep acknowledgement separate from acceptance.
- Preserve rejection and its reason.
- Do not treat a queue entry as proof that a person accepted responsibility.

## Work state and service clock

- Reconcile assignment episodes to work-state changes.
- Reconcile blocked intervals to a reason and release event.
- Identify the service-clock rule and version.
- Separate custody time, actionable time and measured service time.
- Do not infer a pause from an assignment change.

## Corrections and evidence

- Preserve both effective time and recorded time.
- Link corrections to the original event; do not overwrite silently.
- Retain source-system and source-event identifiers.
- Use explicit unknown values where evidence is missing.
- Place unreconciled work in a named exception queue.

## Release test

Publish comparative owner-delay metrics only when every included interval can be rebuilt from the assignment, work-state and clock histories. Document any visible exclusion and its reason.
