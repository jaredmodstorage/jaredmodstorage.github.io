# The Work Order Changed Hands. Who Owned the Delay?

*A time-bounded assignment ledger keeps current ownership from rewriting the history of multi-location facility work.*

By Jared Mastroianni

A work order can be open for nineteen hours and still tell you almost nothing about who owned those hours.

The record may show one current assignee. The history may involve a site manager who opened the request, a regional queue that never acknowledged it, a vendor coordinator who clarified the scope, and a contractor who accepted the dispatch. If the system overwrites the assignee each time the work changes hands, the final record presents the last owner as though that person or team held the work from the beginning.

That is not a harmless reporting shortcut. It can distort response-time comparisons, vendor reviews, staffing decisions and escalation design. It can also punish the person who finally accepted a neglected item.

Multi-location operators need a better rule: **treat assignment as a series of time-bounded episodes, not a single mutable field.** Preserve the work state, the ownership state and the service clock as separate histories. Then measure only the intervals the evidence can actually support.

## A fictional work order with a misleading ending

Consider this fictional example.

At 7:10 a.m., the manager at Cedar Row Storage reports that a climate sensor is no longer transmitting. The manager creates work order WO-1848 and assigns it to the site role while checking the local panel. At 8:05 a.m., the manager routes the work to a regional facilities queue because the panel shows a device fault.

The queue receives the record, but no person accepts it. At 12:20 p.m., an operations lead moves it to the vendor-coordination role. The vendor coordinator accepts it at 12:31 p.m., asks the site for a panel photograph at 12:44 p.m., and pauses dispatch pending that evidence. The site supplies the image at 1:18 p.m. The coordinator dispatches an outside contractor at 1:27 p.m., and the contractor accepts at 1:42 p.m.

The next morning, the dashboard shows the vendor coordinator as the assignee and the work order as nineteen hours old. A simplistic report allocates all nineteen hours to that coordinator.

The record actually contains several different periods:

1. The site owned investigation from creation until routing.
2. The regional queue held an unaccepted item.
3. The vendor coordinator owned it only after acceptance.
4. The request was temporarily blocked while the site supplied evidence.
5. The contractor became the executing party only after accepting the dispatch.

The current assignee is accurate as a present-tense answer. It is false as a historical explanation.

## Keep three histories, not one crowded status field

Operators often try to make one field answer three questions: What condition is the work in? Who is responsible now? Is the response clock running? Those questions are related, but they are not interchangeable.

Use three linked histories.

**The work-state history** records conditions such as reported, triaged, blocked, authorized, in progress, verified and closed. It describes the work.

**The assignment history** records who or what role held responsibility during a defined interval. It describes ownership.

**The clock history** records when a governed response or completion timer started, paused, resumed or stopped. It describes measurement under a specific rule.

A blocked work order may still have an owner. A routed item may not yet have an accepting owner. A clock may pause under one policy while the assignment remains unchanged. Collapsing those facts into one status makes later analysis depend on guesswork.

## The assignment episode is the unit of ownership

An assignment episode should be an append-only record with a beginning, an ending or an explicit open state. At minimum, preserve:

- work-order identifier and facility identifier;
- episode identifier and sequence number;
- owner type, such as person, role, queue, vendor organization or automated service;
- owner identifier and display label as they existed at the time;
- assigned-effective timestamp and the timestamp the record was written;
- assigner and routing reason;
- acknowledgement state and acknowledgement timestamp;
- episode end timestamp and end reason;
- predecessor and successor episode identifiers;
- related work-state and clock-event identifiers;
- source system, source-event identifier and correction lineage;
- an explicit unknown value when a required fact is not available.

The distinction between effective time and recorded time matters. A supervisor may correct a routing error at 3:00 p.m. and state that the corrected assignment became effective at 1:30 p.m. The system should preserve both facts. Rewriting the original event makes the audit trail look cleaner than reality and prevents anyone from seeing that a late correction occurred.

Use timestamps with explicit offsets or UTC. A local display can still show the facility's time zone, but the underlying sequence should not depend on an unstated local clock.

## Routing is not acceptance

Moving a record into a queue proves that a routing action occurred. It does not prove that a person saw the work, accepted responsibility or had the authority and information needed to act.

That boundary deserves its own fields:

- `routed_at`: the sender placed the work with a destination;
- `available_to_queue_at`: the destination system exposed it;
- `acknowledged_at`: a human or governed service recognized the item;
- `accepted_at`: an authorized owner took responsibility;
- `rejected_at` and `rejection_reason`: the destination declined it;
- `escalation_due_at`: the unaccepted item becomes eligible for escalation.

If the platform does not expose all of these events, do not invent them. Record the available evidence and leave the unsupported state unknown. “In the regional queue for four hours” is a defensible statement. “Regional facilities ignored it for four hours” is an accusation the data may not support.

Queues should also have a named steward. The steward is responsible for the health of the queue—coverage, escalation and routing rules—not automatically responsible for completing every work item inside it.

## Transfer the work without erasing the predecessor

A clean handoff ends one assignment episode and opens another. The transfer record should identify both episodes and explain why the boundary changed.

Useful end reasons include scope changed, specialty required, coverage ended, authority insufficient, vendor dispatch, duplicate assignment corrected and work returned. A free-text note can add context, but a controlled reason lets the portfolio find repeated patterns.

Avoid a sequence in which one system closes the old assignment, another opens the new assignment later, and the reporting layer quietly bridges the gap. If the gap is real, preserve it. If the episodes overlap during a deliberate warm handoff, preserve that too and identify the primary owner. Gaps and overlaps are operating facts, not data defects to conceal.

The successor should not inherit blame for time that ended before its episode began. The predecessor should not be blamed for a downstream pause after a valid handoff. Attribution follows the bounded interval, not the final name on the record.

## Separate owner time from blocked time and clock time

An owner can hold work while waiting for access, a photograph, a purchase authorization or a contractor arrival. That waiting period may or may not count against an internal service target. The answer belongs in a versioned clock rule, not in an analyst's spreadsheet after the fact.

For each timer event, record the rule version, event type, effective timestamp, actor or system, reason code and related evidence. Then calculate elapsed time from those events. Do not use assignment changes as implicit clock pauses unless the policy explicitly says to do so.

This produces three honest measurements:

- **custody time:** how long an assignment episode was open;
- **actionable time:** how much of that episode was not blocked by a documented dependency;
- **measured service time:** the time included under the applicable clock rule.

Those values can differ without contradiction. A coordinator may hold the work for five hours, have only forty minutes of actionable time, and accumulate thirty-five minutes under a response target. A useful review explains the differences instead of compressing them into one number.

## Aggregate only after the episodes reconcile

Portfolio comparisons should begin with a reconciliation test, not a leaderboard.

For each work order, ask:

1. Does every assignment episode have a facility and work-order key?
2. Does each closed episode have a start, end and end reason?
3. Are predecessor and successor links consistent?
4. Are unexplained gaps or overlaps flagged?
5. Does every acceptance follow a route or another documented availability event?
6. Are late corrections preserved rather than substituted silently?
7. Are blocked intervals supported by a reason and release event?
8. Can every reported owner-time total be rebuilt from the episode records?

Only reconciled work should enter comparative owner-delay metrics. Unreconciled items belong in an exception queue with a named reviewer and disposition. Excluding them silently would make the dashboard neat but incomplete; allocating them by assumption would make it precise but wrong.

At the portfolio level, compare roles only when their definitions are equivalent. “Facilities coordinator” at one site may include purchasing authority that a similarly named role lacks elsewhere. Preserve the role identifier and authority profile that applied during the episode. Labels alone are not enough.

## The work-assignment episode register

The companion package includes a practical register template and a fully marked fictional example. A weekly review can use it in fifteen minutes:

1. Select work orders that changed owner, exceeded a time threshold or entered an unaccepted queue.
2. Rebuild their assignment episodes from source events.
3. Mark gaps, overlaps, missing acknowledgements and late corrections.
4. Reconcile blocked periods against clock events.
5. Assign each exception to a reviewer with a due date.
6. Publish comparative metrics only after the exceptions are resolved or visibly excluded.

The point is not to create more administrative work. It is to keep a mutable assignment field from becoming a false history.

## Better accountability starts with an honest boundary

Accountability is strongest when it is narrow enough to be true. The site manager owns the period the site held the work. An unaccepted queue is reported as an unaccepted queue. The coordinator owns the period after acceptance. The contractor's execution window begins when the dispatch is accepted under the governing rule.

That structure does not excuse delay. It locates delay where the evidence supports it. It also reveals system problems that person-level scorecards miss: an uncovered queue, a routing rule that sends specialized work to a general team, a required artifact that sites routinely omit, or an escalation timer that never starts.

A work order should be allowed to change hands. Its history should not.

## Sources

1. World Wide Web Consortium, [PROV-DM: The PROV Data Model](https://www.w3.org/TR/prov-dm/), W3C Recommendation, April 30, 2013.
2. National Institute of Standards and Technology, [SP 800-92: Guide to Computer Security Log Management](https://csrc.nist.gov/pubs/sp/800/92/final), September 2006.
3. RFC Editor, [RFC 3339: Date and Time on the Internet: Timestamps](https://www.rfc-editor.org/rfc/rfc3339.html), July 2002.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.
