# AI Incident Replay and Isolation Record

## Purpose

Use this record to investigate a disputed AI-assisted operating decision without repeating its side effects, changing its historical evidence or treating a new model output as an observed facility fact.

This is an authored operational control, not a standard, certification, legal conclusion, product feature or proof of any real deployment.

## Required state separation

Keep these states distinct:

1. **Original production evidence** — records actually retained from the disputed run.
2. **Current operating evidence** — source records observed after that run.
3. **Reconstruction** — a deterministic assembly of retained artifacts without a new model or production tool call.
4. **Isolated rerun** — a new model result produced in a non-effectful environment.
5. **Counterfactual** — a test in which one or more declared inputs or components changed.
6. **Historical finding** — the conclusion supported about the original run.
7. **Change decision** — a separately evaluated and authorized future-state change.
8. **Operating correction** — any real-world review or remediation, verified from its governing source.

## Stop conditions

Do not run the replay when any of these remains unresolved:

- the runner can reach a production side-effecting tool;
- the replay identity carries production authority;
- the original evidence is being edited in place;
- sensitive snapshots lack an approved storage and access boundary;
- the replay mode or changed variables are not declared;
- outputs cannot be labeled and rejected downstream as `replay_only`;
- the team cannot distinguish current records from records observed during the original run; or
- the proposed test would resend, rewrite, charge, restrict, close, publish or otherwise repeat an operating action.

## Workflow

### 1. Preserve

Assign an incident ID and preservation owner. Freeze the original decision ID, trace identifiers, decision-build reference, submitted context, source references, model output, policy decision, human-review state, tool requests, receipts and governing-source readback. Record unavailable evidence as unavailable.

### 2. Bound access

Classify protected content. Store snapshots, prompts and facility records under the required access and retention controls. Prefer protected references and digests where broad duplication is unnecessary.

### 3. Prove isolation

Use a replay identity with no production permissions. Replace live tools with fixtures or simulators. Block outbound routes. Confirm that `replay_only` outputs are rejected by downstream operating systems. Name the person who verified isolation and the evidence retained.

### 4. Declare the replay mode

Choose exactly one primary mode per record: `reconstruction`, `same_build_rerun`, `repeated_run_test` or `counterfactual`. If a new question requires another mode or another changed variable, create a new replay record.

### 5. Execute and compare

Record the bundle digest, build identity, run number, generation settings and result. Compare retrieval, context assembly, model structure, parser, policy, review gate, tool request and authoritative readback separately. Classify each delta as `reproduced`, `explained`, `unexplained`, `unavailable` or `outside_boundary`.

### 6. Conclude without rewriting history

Write the historical finding separately from the replay finding. Identify unresolved gaps. A qualified owner decides whether the evidence supports containment, additional review, a candidate change, no change or another investigation.

### 7. Route future changes normally

Any changed prompt, model, retrieval rule, policy, tool or context assembler enters the normal evaluation, approval, release, monitoring and rollback path. A successful counterfactual is not production approval.

### 8. Verify real-world follow-through

If the incident requires review of an open work order, communication, access state, accounting record or other real effect, assign that work separately. Verify it from the governing source. Do not mark it corrected because a replay produced a better output.

## Minimum release questions

- Can the team identify what the original model actually received?
- Can it prove which policy and tool schemas were active?
- Can it show which side effects were attempted and what the governing source later showed?
- Is the replay technically unable to touch production?
- Is every output labeled with mode, bundle digest, build and changed variables?
- Are repeated-run results reported as a distribution rather than a preferred sample?
- Are unavailable evidence and unexplained differences still visible?
- Is the proposed production change routed through its own evaluation and authority path?

If any required answer is no, the record remains open. Do not convert the gap into a confident explanation.

## Companion files

- `ai-incident-replay-template.csv` — blank record for implementation.
- `ai-incident-replay-fictional-example.csv` — explicitly fictional teaching data only.

