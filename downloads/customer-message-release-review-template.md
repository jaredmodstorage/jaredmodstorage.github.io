# Customer message release review — governed template

> Use only in an approved protected workflow. Do not paste live customer lists, private account records, credentials, personal contacts, sensitive incident details, or unapproved source material into this document or an AI prompt. A completed template is evidence of review work, not permission to send.

## 1. Message control

| Field | Value | Evidence / state |
|---|---|---|
| Message ID / version | `[ID / version]` | `[change record]` |
| Message class / purpose | `[approved class / purpose]` | `[policy reference]` |
| Facility / entity scope | `[approved scope]` | `[identity source]` |
| Consequence tier | `[approved tier]` | `[tier rule / owner]` |
| Requested channel | `[channel]` | `[channel authority]` |
| Send window / time zone | `[start / end / named zone]` | `[source / state]` |
| Drafting actor | `[identity / role]` | `[workflow record]` |
| AI contribution | `[none / draft / extraction / explanation / translation candidate]` | `[model / prompt or protected locator / limitations]` |
| Current owner / next action | `[queue / action]` | `[state]` |

## 2. Audience and population

| Field | Value | Evidence / limitation |
|---|---|---|
| Recipient query ID / version | `[ID / version]` | `[protected locator]` |
| Population cutoff | `[timestamp + zone]` | `[source clock]` |
| Approved count | `[count]` | `[query receipt]` |
| Required inclusions | `[rule]` | `[authority]` |
| Required exclusions / suppressions | `[rule]` | `[authority]` |
| Consent / preference treatment | `[approved disposition]` | `[qualified source]` |
| Rebuild-at-queue rule | `[yes / no / condition]` | `[approval]` |
| Population state | `[current / changed / conflict / hold / unknown]` | `[owner / next action]` |

## 3. Exact draft

Subject / opening:

> `[exact approved candidate]`

Body:

> `[exact candidate body with message version]`

Links, phone numbers, dates, amounts, times, instructions, and calls to action:

| Item | Exact value | Purpose | Source / test | State |
|---|---|---|---|---|
| `[item]` | `[value]` | `[purpose]` | `[source / result]` | `[state]` |

## 4. Claim ledger

| Claim ID | Exact text span | Claim type | Source field / owner | Observed / effective / freshness | Transformation | Limitation | Disposition |
|---|---|---|---|---|---|---|---|
| `[ID]` | `[span]` | `[identity / status / amount / date / feature / instruction / other]` | `[source / owner]` | `[times / horizon]` | `[none / bounded change]` | `[note]` | `[approve / return / remove / unknown]` |

## 5. Source packet

| Source ID | System / record / version | Authority | Read time | Effective time | Freshness result | Conflict / error | Approved use |
|---|---|---|---|---|---|---|---|
| `[ID]` | `[protected locator]` | `[owner]` | `[timestamp]` | `[timestamp]` | `[current / stale / unknown]` | `[state]` | `[claim IDs]` |

## 6. Authority and reviews

| Review | Required actor / scope | Reviewer | Disposition | Time / expiry | Evidence / limitations |
|---|---|---|---|---|---|
| Source-owner review | `[rule]` | `[identity / role]` | `[state]` | `[time / expiry]` | `[record]` |
| Content review | `[rule]` | `[identity / role]` | `[state]` | `[time / expiry]` | `[record]` |
| Operational authority | `[rule]` | `[identity / role]` | `[state]` | `[time / expiry]` | `[record]` |
| Privacy / legal / accessibility | `[when required]` | `[identity / role]` | `[state]` | `[time / expiry]` | `[record]` |
| Channel authority | `[rule]` | `[identity / role]` | `[state]` | `[time / expiry]` | `[record]` |

## 7. Consequence, privacy, and correction

| Control | Approved value / action | Owner | Evidence / state |
|---|---|---|---|
| Potential customer consequence | `[bounded description]` | `[owner]` | `[tier record]` |
| Personal data used | `[minimum fields / protected locators]` | `[privacy owner]` | `[data-flow record]` |
| AI-accessible data | `[none / approved minimum]` | `[AI governance owner]` | `[state]` |
| Masking / tokenization | `[rule]` | `[owner]` | `[test]` |
| Pause / cancel control | `[exact control]` | `[channel owner]` | `[test]` |
| Correction template | `[reference]` | `[communications owner]` | `[state]` |
| Affected-population reconstruction | `[method]` | `[data owner]` | `[test]` |
| Escalation / support | `[governed queue]` | `[owner]` | `[coverage state]` |

## 8. Accessibility and recipient path

| Check | Scope | Result | Evidence / next action |
|---|---|---|---|
| Plain and specific opening | `[subject / first screen]` | `[pass / return]` | `[review]` |
| Dates / amounts / time zone | `[all occurrences]` | `[pass / return]` | `[review]` |
| Descriptive links | `[all links]` | `[pass / return]` | `[test]` |
| Text alternatives | `[non-text content]` | `[pass / not applicable / return]` | `[test]` |
| Desktop / mobile / zoom | `[supported views]` | `[pass / return]` | `[render]` |
| Keyboard / assistive technology | `[action path]` | `[pass / return]` | `[test]` |
| Language / translation | `[variants]` | `[approved / candidate / return]` | `[review]` |
| Help route | `[reply / phone / link]` | `[technical / operational state]` | `[test]` |

## 9. Channel disposition

| State | Exact evidence | What it does not prove |
|---|---|---|
| Approved for exact queue | `[approval record]` | `Not queued or sent` |
| Queued | `[queue identity / time]` | `Not provider accepted or delivered` |
| Provider accepted | `[provider reference]` | `Not delivered, read, understood, or acted upon` |
| Delivery reported | `[provider event]` | `Not read or understood` |
| Recipient response | `[response locator]` | `Not acceptance of every claim` |
| Customer action | `[authoritative workflow record]` | `Not caused solely by the message` |

## 10. Final disposition

- Message version: `[exact version]`
- Recipient query version: `[exact version]`
- Disposition: `[approved_for_exact_queue / approved_with_expiry / returned_for_source / returned_for_population / returned_for_wording / returned_for_accessibility / returned_for_authority / denied / withdrawn]`
- Authorized reviewer: `[identity / role / scope]`
- Reason codes: `[codes]`
- Approval expiry: `[timestamp + zone]`
- Limitations: `[bounded note]`
- Next owner / action: `[queue / action]`
- Rollback or cancellation basis: `[reference]`

**State reminder:** AI draft is not approval; approval is not queueing; queueing is not provider acceptance; provider acceptance is not delivery; delivery is not reading or understanding; customer action needs its own authoritative record.
