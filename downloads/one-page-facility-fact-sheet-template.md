# One-page facility fact sheet — governed template

> Copy this template only into an approved operating location. Do not add real facility data until the responsible source owners define field authority, public/internal classification, review cadence, and retention. Do not place credentials, alarm details, access instructions, personal contacts, private customer data, or sensitive security information in this sheet.

## Record control

| Field | Current value | Source / authority | State | Last checked | Owner / next action |
|---|---|---|---|---|---|
| Facility ID | `[durable ID]` | `[approved registry]` | `[state]` | `[timestamp]` | `[owner]` |
| Fact-sheet version | `[version]` | `[change record]` | `[state]` | `[timestamp]` | `[owner]` |
| Effective at | `[timestamp + zone]` | `[approval]` | `[state]` | `[timestamp]` | `[owner]` |
| Next review | `[timestamp + zone]` | `[review policy]` | `[state]` | `[timestamp]` | `[owner]` |
| Overall state | `[current / conflict_open / change_pending / temporarily_closed / retired / unknown]` | `[authority]` | `[state]` | `[timestamp]` | `[owner]` |

## Identity

| Field | Approved value | Public / internal | Source / authority | Limitation / conflict |
|---|---|---|---|---|
| Customer-facing name | `[value]` | `[class]` | `[source]` | `[note]` |
| Sign name | `[value]` | `[class]` | `[dated observation]` | `[note]` |
| Internal portfolio name | `[value]` | `internal` | `[registry]` | `[note]` |
| Platform display name | `[value by platform]` | `public candidate` | `[platform rule + approval]` | `[note]` |
| Legal-entity reference | `[approved reference or withheld]` | `[class]` | `[qualified source]` | `[do not infer relationship]` |
| Prior / alias name | `[historical value or none]` | `[class]` | `[source]` | `[not current]` |

## Physical and postal location

| Field | Approved value | Source / authority | State / checked at |
|---|---|---|---|
| Address line 1 | `[value]` | `[source]` | `[state / timestamp]` |
| Address line 2 | `[value or not applicable]` | `[source]` | `[state / timestamp]` |
| Locality / region / postal code / country | `[structured values]` | `[source]` | `[state / timestamp]` |
| Validated mailing format | `[value]` | `[validation source]` | `[state / date]` |
| Public display address | `[value]` | `[approval]` | `[state / timestamp]` |
| Map pin | `[coordinates or withheld]` | `[source + precision]` | `[state / timestamp]` |
| Approved arrival note | `[value or none]` | `[source]` | `[state / timestamp]` |

## Customer contact routes

| Purpose | Public value | State | Technical check | Operational check | Owner |
|---|---|---|---|---|---|
| Main phone | `[value]` | `[state]` | `[time / result]` | `[time / result]` | `[owner]` |
| Email / contact URL | `[value]` | `[state]` | `[time / result]` | `[time / result]` | `[owner]` |
| Canonical facility page | `[URL]` | `[state]` | `[time / HTTP result]` | `[content review]` | `[owner]` |
| Rental / account support | `[approved route]` | `[state]` | `[time / result]` | `[time / result]` | `[owner]` |
| Accessibility contact | `[approved route]` | `[state]` | `[time / result]` | `[time / result]` | `[owner]` |

## Hours and time zone

Time-zone identifier: `[IANA zone]`<br>
Schedule version: `[version]`<br>
Special-hours overlay: `[reference / none / unknown]`

| Schedule type | Mon | Tue | Wed | Thu | Fri | Sat | Sun | Valid interval | Source / owner |
|---|---|---|---|---|---|---|---|---|---|
| Office | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[from / through]` | `[source / owner]` |
| Gate access | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[from / through]` | `[source / owner]` |
| Phone support | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[from / through]` | `[source / owner]` |
| Appointment / vendor | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[hours]` | `[from / through]` | `[source / owner]` |

## Lifecycle, approved features, and holds

| Item | Approved value | State | Source / authority | Public wording / hold |
|---|---|---|---|---|
| Operating lifecycle | `[approved state]` | `[state]` | `[source]` | `[approved consequence]` |
| Feature 1 | `[value]` | `[verified_current / limitations / unknown / do_not_publish]` | `[source]` | `[wording / hold]` |
| Feature 2 | `[value]` | `[verified_current / limitations / unknown / do_not_publish]` | `[source]` | `[wording / hold]` |
| Open conflict | `[description or none]` | `[state]` | `[evidence]` | `[owner / next action]` |
| Publication hold | `[scope or none]` | `[state]` | `[authority]` | `[release gate]` |

## Destination reconciliation

| Destination | Fact-sheet version sent | Send / submission state | Applied state | Public readback | Discrepancy | Owner / rollback |
|---|---|---|---|---|---|---|
| Facility webpage | `[version]` | `[state / time]` | `[state]` | `[state / time]` | `[note]` | `[owner / action]` |
| Structured data | `[version]` | `[state / time]` | `[state]` | `[state / time]` | `[note]` | `[owner / action]` |
| Business / map profile | `[version]` | `[state / time]` | `[state]` | `[state / time]` | `[note]` | `[owner / action]` |
| Call routing | `[version]` | `[state / time]` | `[state]` | `[state / time]` | `[note]` | `[owner / action]` |
| Internal directory | `[version]` | `[state / time]` | `[state]` | `[state / time]` | `[note]` | `[owner / action]` |

## Sign-off

- Prepared by: `[identity / role / timestamp]`
- Source-owner review: `[identity / scope / timestamp / disposition]`
- Publication authority: `[identity / scope / timestamp / disposition]`
- Open exceptions: `[IDs / none]`
- Next review: `[timestamp / trigger]`
- Prior version and rollback: `[reference]`

**State reminder:** prepared is not approved; submitted is not applied; applied is not public readback; public readback is not indexing, ranking, coverage, or recognition.
