# Portfolio Lease-Version Issuance and Reconciliation Register

Use this register to connect one approved lease artifact to each facility, channel, generated instance and transaction-safe record. It is an operating-control template, not a lease form, legal opinion, retention schedule or determination of which law, disclosure, consent method, signature process or response applies.

## 1. Freeze the approved release

| Field | Required record | Hold condition |
| --- | --- | --- |
| Release identity | Release ID, artifact class, approval reference, approval owner and approval time | Approval or scope cannot be established |
| Artifact identity | Version ID, controlled source, digest method and digest | Exact approved artifact cannot be reproduced |
| Scope | Eligible facilities, channels, languages or jurisdiction treatment supplied by the authorized owner | Scope is missing, ambiguous or conflicting |
| Effective rule | Effective start/end, time zone and version-selection event | Systems use different or unstated selection events |
| Supersession | Prior version, transition rule and excluded cases | Prior-version disposition is unknown |

## 2. Resolve every issuance path

| Field | Required record | Hold condition |
| --- | --- | --- |
| Facility | Permanent facility ID and governed aliases | Facility identity is unresolved |
| Channel | Web, desk, kiosk, call center, signature link, print or approved fallback | Authorized issuance path is absent from the matrix |
| System identity | Application, environment, tenant/account, workflow and template ID | Test and production or facility scopes are ambiguous |
| Renderer state | Renderer/workflow version, cache state and current reported artifact | Reported state cannot be tied to the approved artifact |
| Local exception | Approved exception ID, boundary, owner and expiry | Unapproved local variation affects issuance |

## 3. Test the customer artifact

| Field | Required record | Hold condition |
| --- | --- | --- |
| Deployment receipt | Target, requested change, acceptance receipt and time | Only a request or success message exists |
| Generated test | Non-customer test instance ID, generated time and retrieval route | Real issuance path was not exercised |
| Artifact comparison | Expected and observed version/digest or approved invariant test | Produced document differs or cannot be evaluated |
| Attachments and fields | Required attachments, signature fields and controlled notices checked | Required component is absent or unknown |
| Readiness decision | Ready, restricted or held; decision owner, reason and evidence | Decision lacks named authority or evidence |

## 4. Reconcile issued instances

| Field | Required record | Hold condition |
| --- | --- | --- |
| Transaction link | Customer-safe transaction reference, facility, channel and selection-event time | Issuance cannot be tied to one transaction |
| Issued instance | Instance ID, issued version, issue time and retrieval reference | Version or instance is unavailable |
| Execution state | Sent, viewed, signed, declined, voided, superseded or other approved state | A generic complete flag hides actual state |
| Eligibility check | Version was eligible for scope and time | Artifact was outside the approved window or scope |
| Reproducibility | Entitled reviewer can retrieve an accurate record through the approved route | Record is missing, inaccessible or not reproducible |

## 5. Route exceptions without inventing facts

Classify the exception as `unknown_version`, `ineligible_version`, `render_mismatch`, `missing_instance`, `duplicate_instance`, `scope_conflict`, `retention_or_access_failure` or another approved code. Record the owner, deadline, operating boundary, evidence required and qualified decision route. Do not label an unknown artifact current based on timing or rollout confidence.

## 6. Prepare rollback before release

- [ ] Rollback authority is named.
- [ ] Last approved artifact and configuration are preserved.
- [ ] Template, renderer, cache and fallback changes are included.
- [ ] A controlled validation test is defined.
- [ ] Current channel state is kept separate from prior transaction disposition.
- [ ] Communication ownership and resume authority are named.
- [ ] Release, exception and rollback evidence has an approved retention and access route.

## Release decision

Release only the facility-channel rows that have a resolved identity, eligible artifact, verified rendered result, named decision owner and recoverable rollback. Keep restricted or held rows visible; do not average them into a portfolio pass.

