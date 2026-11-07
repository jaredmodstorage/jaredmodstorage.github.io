# Facility Change Propagation and Verification Matrix

Use this matrix when a physical facility, asset, route, service, or operating rule changes. It links the source change to every downstream surface that may still describe the old state.

This is an operating-control tool, not a construction closeout, engineering opinion, code determination, emergency-plan design, contract interpretation, or proof that any system performs safely.

## 1. Define the change episode

| Field | Record |
| --- | --- |
| Stable change ID | |
| Governing facility ID | |
| Physical area and affected assets | |
| Authorized old state | |
| Planned new state | |
| Change owner and approving role | |
| Planned physical completion | |
| Planned operating cutover | |
| Rollback or containment plan | |

## 2. Discover every consumer of the old state

Check only surfaces that actually apply:

- [ ] Facility and asset master records
- [ ] Access-control names, mappings, schedules, and permissions
- [ ] Camera, intercom, alarm, or sensor relationships
- [ ] Inspection and preventive-maintenance plans
- [ ] Vendor scope, warranty, contacts, and parts records
- [ ] Emergency, responder, shutdown, or accountability documents
- [ ] Customer maps, directions, notices, and delivery instructions
- [ ] Opening, closing, incident, and outage forms
- [ ] Dashboards, denominators, budgets, and report mappings
- [ ] Training, recurring tasks, offline copies, and cached forms
- [ ] Integrations and automations using the old identity or state

## 3. Classify each row

| Dependency class | Meaning | Release treatment |
| --- | --- | --- |
| Release-critical | Wrong or missing state could misroute frontline work or leave the changed asset without a required control | Verify before normal release |
| Time-bounded follow-up | Can remain temporarily under an explicit owner, due time, and approved instruction | Release only within the documented boundary |
| Historical/analytical | Controls attribution, denominator, budget, or comparison across the cutover | Preserve the effective-time rule and reconcile before reporting |

## 4. Record update and readback separately

Use one explicit state:

- `identified`
- `assigned`
- `updated_unverified`
- `verified_current`
- `exception_active`
- `not_applicable`
- `blocked`

For every row, record the expected version or state, update owner, completed time, readback method, observed result, verifier, and verification time. Do not treat an update submission, sync job, upload, or timestamp as readback.

## 5. Preserve the cutover

- [ ] Record physical completion, operating release, and reporting effective time separately.
- [ ] Preserve the old state for events before the approved cutover.
- [ ] Link later corrections to affected reports without rewriting history.
- [ ] Define how denominators and asset populations change.
- [ ] Assign every temporary exception an owner and expiration.

## 6. Release and close

- **Exact release scope:**  
- **Release-critical rows verified:**  
- **Active exceptions and limits:**  
- **Operating release approved by / time:**  
- **Historical reporting rule approved by:**  
- **Final propagation verifier / time:**  
- **Rows still open:**  

Do not write “project complete” when the physical work is finished but a release-critical or historical dependency remains unowned.
