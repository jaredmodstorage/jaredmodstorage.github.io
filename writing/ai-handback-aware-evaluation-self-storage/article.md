---
title: "The AI Handed the Case Back. Why Did the Benchmark Mark It Wrong?"
author: Jared Mastroianni
intended_slot: 2026-11-18 evening AI architecture
publication_destination: Jared Mastroianni personal authority site
publisher_owner: Master Personal Site Authority
canonical: https://jaredmodstorage.github.io/writing/ai-handback-aware-evaluation-self-storage/
status: publication-ready; publisher handoff intentionally withheld
hero_image: assets/068-unit-design-engineering-review.png
---

<!-- BODY START -->

# The AI Handed the Case Back. Why Did the Benchmark Mark It Wrong?

**By Jared Mastroianni**

*An AI evaluation should reward the system for recognizing when the evidence or authority is insufficient—not force a confident answer that an operator could mistake for a decision.*

Consider an explicitly fictional access case. A customer says the mobile credential stopped working at a multistory facility. The case packet contains a current account record and a recent credential event, but it does not establish which entrance the customer used. One work order says the vehicle gate is under maintenance. Another record shows the building lobby reader is online.

The AI does not choose “access should be allowed” or “access should be denied.” It returns `hold_and_hand_back`. It identifies the unresolved entrance, separates the two asset records, blocks any customer restriction, and asks a named operator to verify the entrance and current maintenance scope.

The workflow behaves responsibly. The benchmark gives it a zero because the answer key contains only `allow` or `deny`.

That evaluation did not discover a model failure. It created one. It rewarded unsupported certainty and penalized the system for respecting an operating boundary.

Self-storage operators building AI into access, maintenance, delinquency, vendor, pricing or customer-service workflows need a different release standard. We should evaluate whether the system answered correctly **when a decision was eligible**, and whether it handed the case back correctly **when a decision was not eligible**. Those are separate capabilities.

## The answer key is part of the architecture

A benchmark is not a neutral scoreboard. Its cases, labels and scoring rules define what the development team will optimize.

If every case requires a binary answer, the benchmark teaches the system that completion matters more than evidence. If a refusal receives the same penalty as a wrong action, the benchmark encourages guessing. If the evaluator ignores operating authority, a model can score well by recommending an action no one authorized it to take.

This is especially dangerous in a facility operation because the missing fact is often the fact that controls the action: the exact facility, entrance, unit, account, asset, time window, governing policy or approving role. A fluent answer can be semantically plausible and still be operationally ineligible.

The [NIST AI Risk Management Framework Core](https://airc.nist.gov/airmf-resources/airmf/5-sec-core/) calls for testing before deployment and regularly in operation, documenting limitations beyond development conditions, interpreting output in context, and demonstrating that a system can fail safely when it operates beyond its knowledge limits. It also says measurement should be informed by domain experts and relevant actors. That voluntary, cross-sector framework does not prescribe a self-storage benchmark or this gate. It does support the underlying discipline: context and knowledge limits belong inside the evaluation, not in a disclaimer after release.

## Separate five questions that one accuracy score hides

Before scoring the wording of an answer, an evaluator should ask five questions in order.

1. **Was the evidence eligible?** Were the required subjects identified, sources current enough, fields complete, and conflicts resolved for this decision class?
2. **Did the system have decision authority?** Was it permitted to recommend, draft, route, or act—or only to summarize?
3. **Did it choose the right output class?** The correct class may be `answer`, `bounded_summary`, `hold_and_hand_back`, or `system_error`.
4. **Was the output correct within that class?** An eligible answer must be substantively correct. A handback must stop the right action for the right reason.
5. **Could the operator restart the work safely?** The output should identify what is known, what is missing, who owns the next step, and what evidence permits re-entry.

An evaluation that begins at question four can mark an ineligible answer correct. It can also mark a correct handback wrong because the evaluator never represented handback as an acceptable result.

## Make disposition a first-class label

The gold record for each test case should include an expected disposition before it includes an expected answer. At minimum, I would use four classes:

- `answer`: the required evidence and authority are present;
- `bounded_summary`: the system may describe verified facts but may not resolve the decision;
- `hold_and_hand_back`: the workflow must stop a defined action and transfer the unresolved case;
- `system_error`: the evaluation cannot determine a business disposition because a required technical component failed.

That classification keeps three very different events from collapsing into “no answer.” A model may deliberately decline because the evidence is insufficient. A policy gate may block an otherwise valid recommendation because the model lacks authority. Or the connector may fail before the model receives the evidence. Each needs a different owner, retry rule and release consequence.

Do not let a generic phrase such as “I can’t help with that” pass as a handback. A safe disposition is useful only when it preserves the work.

## Build the benchmark around evidence conditions

Most evaluation sets overrepresent clean, complete cases because they are easier to label. Operations do not arrive that way. A release set should deliberately include:

- a required field that is missing;
- a source that is stale for the proposed action;
- two current sources that conflict;
- the right fact attached to the wrong facility or asset;
- a valid exception whose scope does not cover the current case;
- a tool or connector that is unavailable;
- an operator request that exceeds the requester’s authority;
- a policy version that changed after the case was assembled; and
- a case that becomes eligible only after new evidence is added.

Use matched pairs. One case should contain enough evidence for a decision; its partner should remove or alter one controlling field. The expected output class should change. This tests whether the system recognizes the decision boundary rather than merely reproducing familiar language.

The [NIST Generative AI Profile](https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence) recommends setting minimum performance or assurance thresholds for deployment approval and considering unreliable decision-making, invalid output and system dependencies in risk tiers. It is voluntary, cross-sector guidance, not a certification or a storage-specific release rule. The practical implication is still valuable: go/no-go criteria should cover the risks that matter in the actual workflow.

## Score handback as a capability, not a consolation prize

One aggregate “accuracy” number is too blunt for a consequential workflow. The release report should show at least these measures separately:

| Measure | What it asks | Release concern |
|---|---|---|
| Eligible-case answer correctness | When a decision was permitted, was the answer correct? | Wrong operating conclusion |
| Correct handback rate | When the case required handback, did the system choose it? | Forced answer under insufficient evidence |
| False handback rate | When evidence and authority were sufficient, did the system stop unnecessarily? | Avoidable operational friction |
| Unsafe action rate | Did any ineligible case produce an action or authoritative recommendation? | Customer, facility or financial harm |
| Handback completeness | Did the output preserve known facts, unknowns, reason, owner and blocked action? | Abandoned or ambiguous work |
| Re-entry readiness | Did the output state what evidence or authority allows the case to resume? | Repeated loops and manual reconstruction |

This does not mean every dimension should be averaged into a generous composite. Some are hard gates. One unauthorized action in a high-consequence access set may block release even if the average score is high. A model that answers clean cases beautifully but invents certainty when evidence is missing is not ready for that route.

[NIST AI 800-3](https://www.nist.gov/publications/expanding-ai-evaluation-toolbox-statistical-models) distinguishes performance on a fixed benchmark from performance across a broader population of similar items and argues that evaluators should define the measurement target and disclose assumptions. The report analyzes statistical estimation and uncertainty; it does not define handback scoring or validate this tool. Its narrower lesson applies: say precisely what the metric measures. “Ninety-four percent accurate” is not meaningful if the test design hid every case in which the system should have stopped.

## Require a complete handback packet

A passing handback should contain six elements:

1. **Known facts:** only the eligible facts the system can support.
2. **Unknown or conflicting facts:** the exact gap, not a vague low-confidence statement.
3. **Reason for stopping:** the governing evidence, policy or authority condition.
4. **Blocked action:** what the system did not release, change or communicate.
5. **Named next owner and step:** the role that can resolve the gap and the required task.
6. **Re-entry condition:** the new evidence, approval or restored service needed before rerun.

Completeness matters because refusal can be operationally unsafe in a quieter way. A system that stops but strands the case creates delay, repeated investigation and opportunities for someone to bypass the control. The goal is not maximum abstention. The goal is the right disposition with a usable path forward.

The evaluation should also reject fabricated handoff facts. If the benchmark does not identify an assigned person or due time, the system should not invent one to make the packet look complete. It can name an approved role or mark the assignment as required.

## Test the return path, not only the stop

Handback-aware evaluation needs a second phase. Add the missing entrance identifier, resolve the work-order scope, restore the failed connector, or supply the authorized approval. Then rerun the case under a new evaluation event linked to the original.

The test should confirm that the system:

- recognizes the controlling change;
- does not carry the old hold forward as if nothing changed;
- does not erase the earlier handback;
- reevaluates the case under the current model, prompt, policy and evidence versions; and
- produces only the output class now permitted.

This is how an operator learns whether the architecture can recover. A system that stops safely but cannot resume safely will eventually invite manual workarounds.

## A fictional release case

Return to the fictional access case. The benchmark record identifies the expected disposition as `hold_and_hand_back`. Required known facts are the active account and the two asset-specific records. The missing field is `entrance_id`. The prohibited output is any instruction to deny account access, change a credential, or tell the customer the entire facility is unavailable.

In the first run, the model selects handback but says only, “More information is needed.” It passes the disposition gate and fails the completeness gate. The operator would still have to reconstruct the case.

In the second run, the system identifies the unresolved entrance, distinguishes the lobby reader from the vehicle gate, preserves the current account fact, blocks credential changes, assigns verification to the fictional facility-operations role, and states that a confirmed entrance ID plus current asset state permits re-entry. That is a passing handback.

The benchmark then supplies a fictional observation tying the incident to the lobby reader and a current record showing that reader online. The new run may now produce a bounded troubleshooting response under the fictional policy. The original handback remains in the trace.

Nothing in this example represents a real customer, facility, deployment, model result or performance improvement. It demonstrates the evaluation contract.

## Release the workflow the benchmark actually tested

The final release gate should bind the test results to the model version, prompt version, tool set, evidence schema, policy version, parser, route table and action permissions that will enter production. A passing model score does not cover a later parser change that turns `hold_and_hand_back` into a blank, or a workflow change that allows a held case to trigger a customer message.

Re-run the handback set when any of those components changes. Keep the failed cases. Record approved limitations. Monitor production for answers issued under missing evidence, unnecessary handbacks, incomplete packets and actions after a hold. Production observations should improve the benchmark without being presented as facility results unless the evidence supports that claim.

The companion **Handback-Aware Evaluation and Release Gate** turns this approach into a case-level record and a release decision. It is designed to make the evaluator answer a harder question than “Did the model produce the expected sentence?”

The real question is: **Did the system know when it was allowed to decide, when it had to stop, and how to return the work to an operator without losing the case?**

That is not a softer standard. It is a more operationally honest one.

<!-- BODY END -->
