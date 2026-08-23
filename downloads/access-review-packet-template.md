# Access review packet

Use one packet for one subject, one platform role, one resource scope, and one review decision. Do not record passwords, private keys, recovery codes, session cookies, or reusable tokens.

## Record control

- Review ID:
- Grant ID:
- Packet version:
- Review opened at:
- Review due at:
- Reviewer:
- Decision owner:
- Final state: `approved` / `reduce` / `expire` / `revoke` / `investigate` / `unknown`

## Subject

- Subject type: `person` / `team` / `group` / `service account` / `app` / `integration` / `key`
- Display name:
- Platform-native immutable identifier:
- Organizational identity:
- Employment, vendor, or service relationship evidence:
- Owning team:
- Manager or sponsor:
- Shared identity: `yes` / `no` / `unknown`

## Role and permissions

- Platform:
- Account, tenant, organization, group, or site:
- Exact role label:
- Role version or documentation date:
- Direct permissions:
- Inherited permissions:
- Group or team paths:
- Parent-resource paths:
- App, key, token, or verification paths:
- Highest-consequence permitted action:

## Scope

- Resource type:
- Stable resource identifier:
- Facility IDs:
- Included resources:
- Excluded resources:
- Geographic or entity boundary:
- Data boundary:
- Environment boundary: `production` / `candidate` / `test` / `multiple`
- Can the subject add other users? `yes` / `no` / `unknown`
- Can the subject change or remove the resource? `yes` / `no` / `unknown`

## Purpose and authority

- Exact operating task:
- Why the current role is necessary:
- Lower role considered:
- Narrower scope considered:
- Approver identity:
- Approval authority source:
- Approval evidence:
- Segregation-of-duties conflict:
- Exception and expiry, if any:

## Time

- Requested at:
- Approved at:
- Invitation or provisioning at:
- Accepted at:
- Active from:
- Expires at:
- Standing review cadence:
- Last reviewed at:
- Removal triggers:
- Activity freshness:

## Authentication and non-secret dependencies

- Authentication method:
- MFA state and evidence date:
- Identity provider:
- Recovery-factor custodian:
- Credential class:
- Credential vault or provider location, without secret:
- Last rotation:
- Verification token type and owner:
- Service or app installation owner:
- Domain, DNS, hosting, repository, deployment, billing, or reseller dependency:

## Revocation and continuity

- Assignment removal route:
- Group or parent removal route:
- Token, key, app, and session revocation route:
- Verification-token cleanup route:
- Credential rotation requirement:
- Approved continuity identity:
- Rollback or emergency restoration path:
- Fresh readback performed at:
- Remaining access or unknown dependencies:
- Revocation evidence:

## Decision

- Effective role and scope reproduced: `yes` / `no`
- Purpose still active: `yes` / `no` / `unknown`
- Role is least necessary for the task: `yes` / `no` / `unknown`
- Scope is least necessary for the task: `yes` / `no` / `unknown`
- Expiry or review trigger is enforceable: `yes` / `no` / `unknown`
- Revocation and continuity paths are proven: `yes` / `no` / `unknown`
- Platform label kept separate from legal or business ownership: `yes` / `no`
- Final disposition and reason:

## Boundary

This packet documents a proposed operating review. It is not a credential store, legal ownership determination, employment or contract conclusion, security assessment, certification, compliance opinion, platform capability guarantee, proof of current access, or authorization to add, remove, reduce, transfer, or exercise access.
