# Portfolio Responsibility Cutover and Orphan Queue

Use one row per responsibility surface or open item. Preserve historical attribution; assign future authority from the effective time. A blank owner is an exception, not a completed transfer.

## State definitions

| State | Entry condition | Exit evidence |
| --- | --- | --- |
| Identified | Surface or open item is in scope. | Source owner and source record captured. |
| Mapped | Incoming owner and effective time are approved. | Named exception owner and decision boundary. |
| Accepted | Incoming owner confirms visibility, authority and scope. | Acceptance timestamp and unresolved questions. |
| Effective | New routing or authority is live. | Live-system or live-process proof. |
| Reconciled | Expected and actual ownership match. | Counts, test results and exception list. |
| Closed | Exceptions are resolved or accepted by a named next owner. | Independent closeout record. |

## Required fields

| Field | Required entry |
| --- | --- |
| Record ID | Stable cutover identifier. |
| Facility | Governed facility ID and display name. |
| Work surface | System, queue, approval, report, list or process. |
| Source item ID | Native ID when the row represents open work. |
| Historical owner | Person accountable before effective time. |
| Incoming owner | Person accountable after effective time. |
| Decision authority | View, recommend, approve, close or escalate. |
| Effective time | Timestamp when future responsibility changes. |
| Acceptance time | Timestamp when incoming owner accepts scope. |
| Access status | Tested result, not requested state. |
| Route-test status | Actual recipient or workflow result. |
| Exception class | None, unowned, dual-owned, unauthorized or stale route. |
| Exception owner | Person responsible for resolving the defect. |
| Next action and due time | Concrete resolution step and deadline. |
| Evidence link | Retained source, screenshot, export or decision record. |
| Final state | Identified, mapped, accepted, effective, reconciled or closed. |

## Cutover sequence

1. Freeze the in-scope inventory and record its time.
2. Map future ownership and decision authority.
3. Name an exception owner for every incomplete mapping.
4. Obtain incoming-owner acceptance.
5. Activate routes and access at the effective time.
6. Test unowned, dual-owned, unauthorized and stale-route conditions.
7. Reconcile expected and actual item counts.
8. Close only after every exception has evidence or an accepted next handoff.

## Release rule

Do not mark the cutover closed merely because the roster changed. Closure requires preserved historical attribution, active future authority, accepted scope, exactly one accountable route per open item, completed route and access tests, and a zero unresolved orphan count.

The included CSV example is explicitly fictional and must not be treated as an actual portfolio record.
