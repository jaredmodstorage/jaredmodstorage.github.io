# The AI Gave Three Different Answers. Which One Became the Operating Decision?

## A release-control method for managing run-to-run variance in self-storage AI workflows

**By Jared Mastroianni**

<!-- BODY START -->

Give an AI system the same operating packet three times and it may return three different answers.

One run says the facility manager should inspect an access-control event today. Another says to ask the regional manager for more evidence. A third says the event looks routine and requires no action. The source records, prompt, model label and user are unchanged. Only the run is different.

That is not automatically a defect. Generative systems can produce variable outputs by design. The operating problem begins when a team treats one sampled answer as though it were the one inevitable conclusion. If the first run can create a work order, the second can suppress it and the third can change its priority, the organization does not have one decision rule. It has a lottery connected to operations.

Responsible architecture must govern the variance before any output becomes an operating decision. The goal is not to force every sentence to be identical. It is to identify whether repeated outputs are materially equivalent, expose consequential disagreement, and place a deterministic release boundary between model proposals and authorized action.

## Separate wording variance from decision variance

Two answers can use different words and still propose the same operating disposition. “Inspect the south gate before close” and “Complete a south-gate inspection today” may be materially equivalent if they name the same facility, action, owner, deadline, evidence and authority state.

Two polished answers can also hide a serious difference. “Inspect today” is not equivalent to “monitor until the next scheduled visit.” “Draft a customer update” is not equivalent to “send the update.” “Review this unit-access anomaly” is not equivalent to “disable the credential.”

Define the fields that make a difference before testing the system. For an AI-assisted operating proposal, those fields may include:

- the facility, asset, unit, customer case or work order affected;
- the proposed action and the systems it would touch;
- the recipient or execution owner;
- the priority, deadline and expiration;
- the evidence cited and any missing evidence;
- the policy and eligibility state;
- the required human authority; and
- the claimed final state.

Normalize each run into those fields. Then compare the normalized proposals rather than comparing prose. This makes harmless language variation visible as harmless and prevents a material change from disappearing inside fluent wording.

## Eligibility must not depend on the most persuasive answer

The safest place to reduce variance is before generation. Decide with ordinary, testable controls whether the case is eligible for the workflow at all.

A facility identifier should resolve to one current property. Required sources should be present and fresh enough for the task. The requested action should be within the approved use case. The user, agent and tool should have a named scope. A legal, safety, payment, access or customer-impact boundary may require a human regardless of what the model recommends.

These gates should produce structured states such as eligible, ineligible, incomplete, conflicted or expired. The model may summarize the evidence or propose an action after the gate. It should not talk an incomplete case into eligibility.

This is a practical division of labor. Generative reasoning can help organize ambiguous information. Deterministic controls can enforce facility identity, required evidence, role scope, prohibited actions, time limits and approval requirements. The proposal can vary. The release conditions should not.

## Test a set of runs, not the answer you happened to keep

One successful demonstration does not characterize a variable system. For a consequential workflow, the evaluation plan should specify how many repeated runs will be performed under the same controlled input and configuration. Preserve every run, including outputs the evaluator dislikes.

The appropriate replication count depends on consequence, cost and expected variability. There is no universal safe number. What matters is that the count and stopping rule are set before results are reviewed. Otherwise, the evaluator can keep generating until the system produces an agreeable answer.

That practice—regeneration shopping—creates false confidence. If a reviewer rejects four proposals and keeps the fifth without recording the first four, the production record hides the behavior the evaluation was supposed to reveal. A new run is new evidence about system behavior, not an eraser.

For each test set, record completed runs, distinct material proposal classes, the share of runs in each class, abstentions, invalid outputs, tool requests and policy-gate outcomes. Keep the raw output under appropriate access controls, but make the normalized comparison available to the reviewer.

NIST's February 2026 guidance on measuring AI system performance notes that standard errors can arise from both benchmark-item selection and nondeterministic sampling from large language models.[^1] The paper concerns benchmark evaluation, not facility decision release. Its useful operational lesson is narrower: when the system can vary across runs, uncertainty from that variation belongs in the measurement record.

## Agreement is evidence, not authority

Suppose five identical-input runs produce the same proposal four times. That may support a finding that the proposal is stable under the tested configuration. It does not prove the proposal is true, safe or authorized.

The repeated answer may rely on the same stale source. All five runs may misunderstand the same facility code. A majority can consistently recommend an action that policy forbids. Conversely, a minority answer may identify the missing evidence that the other runs overlooked.

Do not let a model vote itself into authority. Use agreement rates as diagnostic evidence. Keep policy, human approval and execution authority separate.

NIST's AI Risk Management Framework is voluntary, non-sector-specific and use-case agnostic.[^2] Its Core calls for testing before deployment and regularly in operation, measurement with uncertainty, documented test details, monitoring of production behavior, and interpretation of output within context.[^3] Those outcomes do not prescribe this release pattern or certify a self-storage workflow. They support the broader discipline of measuring the deployed system rather than trusting a selected example.

## Show the reviewer the disagreement packet

A human-in-the-loop control fails if the human sees only the answer chosen by the system or developer. The review screen should show the operating evidence, normalized proposals, material differences, eligibility state, applicable policy, model and configuration identifiers, and the reason a release is being requested.

The reviewer does not need five near-identical essays. A compact variance packet is better:

- three runs propose inspection today;
- one proposes monitoring;
- one abstains because the source timestamp is missing;
- two runs cite a work order that closed before the evidence cutoff;
- every run is blocked from execution until the source conflict is resolved.

Now the person can adjudicate the actual disagreement. The reviewer can approve a bounded action, request current evidence, change the proposed owner, hold the case, or reject the use of AI for that decision type. The record should preserve who decided, what was released, the policy applied and when the decision expires.

Human review is not a ritual checkbox. It is a decision function with an evidence packet, defined authority and an auditable outcome.

## Release one structured decision

After review, downstream systems should receive one structured release record, not whichever paragraph the application happens to display.

The release record should name the decision case, approved action, target, scope, owner, deadline, evidence snapshot, policy version, approving authority and expiration. A tool adapter should validate those fields again before creating a work order, drafting a message or updating an internal case. If the action exceeds the approved scope, the adapter should refuse it.

Execution still needs a receipt. “Approved” is not “performed.” A work-order request may fail, a draft may never be reviewed, or an update may reach the wrong facility record. Reconcile the execution result to the release record and keep proposal, approval, execution and verification as separate states.

This structure also prevents prose from silently expanding authority. A model may write, “Contact the customer and suspend access until inspection.” If the approved release authorizes only an internal inspection task, the messaging and access-control actions have no executable fields and must not occur.

## A fully fictional portfolio example

Consider Crescent Row Storage, a fictional operator. Every facility, person, system, record, event and outcome in this example is invented.

The fictional company tests an AI-assisted workflow that reviews after-hours gate events. One controlled packet concerns fictional facility CR-04 and contains an event record, a current access schedule, a recently closed gate work order and a note that the camera source is unavailable.

Five repeated runs use the same frozen packet and configuration. Two propose a same-day gate inspection. One proposes monitoring for another event. One recommends asking the regional manager whether the recent repair was verified. One abstains because it cannot confirm whether the closed work order includes an operating readback.

The team does not calculate a 40% vote and release the inspection. It normalizes the runs and sees three material classes plus an abstention. More importantly, the eligibility gate shows that the workflow requires a current readback after gate repair. The case is incomplete.

The fictional reviewer requests the missing readback and holds all automated action. After an authorized employee records current evidence through the existing operating process, the case receives a new input-packet identifier. Prior outputs remain attached to the old packet. The system does not regenerate until one answer looks convenient, and it does not represent the later evidence as though it existed during the first runs.

This example demonstrates the control logic only. It is not a modSTORAGE or Facily.ai deployment, incident, customer result, performance claim or product feature.

## The AI Decision Variance and Release Register

The companion register creates one record for the decision case and one linked row for each repeated run. It captures the frozen input-packet hash, evidence cutoff, model and prompt versions, tool schema, sampling configuration, normalized proposal class, cited evidence, eligibility state, material-difference code, disagreement state, reviewer disposition, released action and execution receipt.

Use four release states:

- **Hold:** required evidence, identity, policy, authority or test coverage is incomplete.
- **Limited:** only a named low-consequence subset may proceed under a bounded scope.
- **Approved:** an authorized reviewer releases one structured action for a defined target and time window.
- **Reconciled:** the approved action has a verified execution receipt and any required operating readback.

The register does not prove model accuracy, facility safety or legal compliance. It does not turn repeated agreement into ground truth. It provides a narrower control: the organization can show what varied, what mattered, who had authority and which single decision—if any—was allowed to reach operations.

## Govern the distance between an answer and an action

AI output variance is manageable when the architecture treats model responses as proposals. Freeze the input packet. Predefine the replication and stopping rule. Normalize the decision fields. Preserve every run. Expose material disagreement. Keep eligibility and authority deterministic. Give the reviewer the variance packet. Release one structured decision and reconcile its execution.

Then three different answers are not a hidden inconsistency. They are observable system behavior inside a controlled decision process.

The dangerous architecture is not the one that admits the model can vary. It is the one that samples once, keeps the most convenient answer and lets that answer become facility fact.

<!-- BODY END -->

## Sources

[^1]: National Institute of Standards and Technology, [*Expanding the AI Evaluation Toolbox with Statistical Models* (NIST AI 800-3)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.800-3.pdf), February 2026, accessed October 14, 2026.
[^2]: National Institute of Standards and Technology, [*Artificial Intelligence Risk Management Framework (AI RMF 1.0)*](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10), January 2023, accessed October 14, 2026.
[^3]: National Institute of Standards and Technology, [*AI RMF Core*](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/), official AIRC presentation of AI RMF 1.0 outcomes, accessed October 14, 2026.
