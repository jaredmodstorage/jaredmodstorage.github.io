# Portfolio Physical-Key Scope and Custody Register

Use one record per physical key copy, with linked scope, lock and lifecycle records. Do not store cut codes or other reproduction-sensitive details in this ordinary operating register.

## Identity

- Record ID
- Key copy ID
- Key system ID
- Key set/ring ID
- Facility ID
- Key class label
- Physical tag identifier
- Issuing region

## Scope relationship

- Scope record ID
- Controlled-opening group ID
- Controlled-opening group version
- Expected scope description
- Expected scope effective from/to
- Scope source type
- Scope source reference
- Scope source owner
- Verified scope state (`verified`, `partial`, `unknown`, `exception`)
- Verification method
- Verified by
- Verified at
- Scope exception ID
- Sensitive-detail location reference

## Custody and authorization

- Custody state
- Holder type
- Holder/role ID
- Controlled storage location ID
- Business purpose
- Authorization source
- Authorized by
- Authorized at
- Issue time
- Expected return/review time
- Actual return time
- Return received by
- Use restrictions
- Geography/time restrictions

## Copy control

- Copy request ID
- Production approval ID
- Approved producer/vendor ID
- Produced at
- Received at
- Received by
- Expected copy count
- Verified copy count
- Unresolved copy count
- Count verified at
- Count evidence reference

## Lock dependency

- Lock/core group ID
- Lock/core version
- Relationship effective from/to
- Predecessor lock/core group ID
- Locksmith/service record reference
- Lock-change reconciliation state
- Reconciled by/at

## Lifecycle and exceptions

- Lifecycle state
- State changed at
- State changed by
- State evidence reference
- Lost/stolen reported at
- Loss response owner
- Quarantine location
- Destruction authorization
- Destroyed by/at
- Open exception ID
- Exception severity
- Exception owner
- Target resolution date
- Closure evidence
- Attestation cycle
- Last attested by/at
- Next review due

## Control rules

1. A label does not create scope.
2. Possession does not create current authorization.
3. A returned ring proves only the return of identified copies.
4. `Unknown` is an exception, not a blank to be treated as approval.
5. A lock change ends and creates key-to-lock relationships at explicit effective times.
6. Copy production, receipt, issue, return, quarantine and destruction remain separate states.
7. Store reproduction-sensitive details only in the restricted system designated by the operator.
8. Close an exception only with assigned evidence and an accountable owner.
