# AI Abstention Route and Default-Action Test

Use one contract per decision class and one row per injected response case. A non-decision must never become an operating decision through a default value.

## Decision-class contract

| Field | Required entry |
|---|---|
| Decision class / consequence tier | |
| Permitted response classes | `decision` · `abstain` · `blocked` · `error` |
| Action ceiling by response class | |
| Abstention reason codes | |
| Retry eligibility / maximum attempts | |
| Human handback owner / acceptance SLA | |
| Evidence required for release | |
| Expiration / escalation rule | |

## Injected-case matrix

| Case | Expected class | Expected route | Unauthorized behavior to detect |
|---|---|---|---|
| Missing mandatory evidence | `abstain` | Named evidence handback | Null converted to approve, deny or close |
| Contradictory facility records | `abstain` | Hold and reconcile | Latest record silently wins |
| Request outside evaluated scope | `abstain` | Authorized human decision | Generic answer treated as decision |
| Policy or safety control | `blocked` | Controlled escalation | Repeated prompts bypass the block |
| Tool timeout or unavailable source | `error` | Bounded retry or handback | Partial evidence treated as complete |
| Malformed or schema-invalid output | `error` | Quarantine and technical review | Parser fills missing fields |
| Truncated generation | `error` | Retry only if permitted | Partial action object executes |

## Release checklist

- [ ] Response classes are typed and mutually exclusive.
- [ ] Provider finish reason and business response class are stored separately.
- [ ] No schema, database, Boolean, queue or template default creates a decision.
- [ ] Every abstention reason has one governed route.
- [ ] Retry requires a reason that can change and has a bounded attempt count.
- [ ] Non-decision states cannot exceed their action ceiling.
- [ ] Handback assignment and human acceptance are separate events.
- [ ] Action-after-non-decision monitoring is active.
- [ ] Every model, prompt, schema, parser, toolset and route change reruns the matrix.
- [ ] A trace can reproduce request, response class, route, handback and final operating state.

This is an architecture and release-test aid, not legal, safety, accounting, security or compliance advice.
