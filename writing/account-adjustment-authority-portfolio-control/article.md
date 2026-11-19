---
title: "The Credit Posted. Was It a Correction, a Courtesy, or a Policy Exception?"
slug: account-adjustment-authority-portfolio-control
author: Jared Mastroianni
destination: Jared Mastroianni personal authority site
canonical: https://jaredmodstorage.github.io/writing/account-adjustment-authority-portfolio-control/
lane: Midday systems
intended_slot: 2026-11-18 13:00 America/New_York
---

# The Credit Posted. Was It a Correction, a Courtesy, or a Policy Exception?

A portfolio report can show twenty account credits and still tell leadership almost nothing useful. One credit reverses a charge that should never have posted. Another follows a written service-recovery policy. A third is a manager’s discretionary courtesy. A fourth was entered to fix a payment that landed on the wrong account. The ledger may reduce all four to the same negative amount.

They are not the same operating event.

When every adjustment shares one generic label, the portfolio loses the reason, authority and evidence behind the transaction. A facility with disciplined corrections can look identical to a facility making repeated exceptions. A regional manager cannot tell whether a pattern points to training, system configuration, customer experience or an authorization problem. Finance receives a number but not a reliable explanation.

The answer is not a longer free-text note. It is an adjustment control that separates what happened, why it happened, who had authority, what evidence was reviewed and how the posted result was reconciled.

## Start by separating four kinds of change

The first control is classification. I would not allow “credit” to serve as both the transaction type and the business reason. At minimum, distinguish these four classes:

**Correction.** The original account state was wrong. Examples include a duplicate charge, an incorrect effective date or a payment applied to the wrong account. A correction should point to the erroneous source event and the evidence for the corrected state.

**Policy-based adjustment.** A current written rule calls for a defined treatment when stated conditions are met. The record should identify the policy version, qualifying facts and calculation method. The employee is applying a rule, not inventing one.

**Discretionary courtesy.** An authorized person chooses an allowed exception within a stated limit. The record needs the decision maker, authority tier, reason and amount. “Customer upset” is not enough to reconstruct the decision.

**Unresolved adjustment request.** The requested change lacks the evidence, authority or classification needed to post. It belongs in a queue, not in the ledger disguised as a completed event.

These classes do not tell an operator which adjustment is legally required or financially correct. That depends on the agreement, applicable law, current policy and approved accounting treatment. The classes create a portfolio control for routing and evidence; they do not replace legal or accounting review.

## Keep the request, decision, posting and reconciliation separate

One of the easiest ways to lose control is to treat the first request as the final transaction. A customer asks for a credit, a manager agrees, someone posts an amount and the dashboard marks the matter complete. That collapses four different states:

1. **Requested:** someone proposed a change and named the affected account and charge.
2. **Decided:** an authorized person approved, denied or returned the request for more information.
3. **Posted:** the approved transaction appeared in the system of record.
4. **Reconciled:** the posted amount, account, date and reason agree with the approved decision.

A request can be valid and still be denied. A decision can be approved and never post. A transaction can post to the wrong account. A correct posting can still carry the wrong reason code and distort portfolio analysis.

The state model makes those failures visible. It also prevents a screenshot of a zero balance from being treated as proof that the approved adjustment was executed correctly. The balance is an outcome. The control needs the decision and transaction lineage that produced it.

## Build authority around the decision, not the job title

An adjustment policy should answer more than “managers can issue credits.” It should identify which adjustment classes each role may decide, the maximum scope, when a second review is required and which conditions require escalation.

Useful authority dimensions include:

- facility or portfolio scope;
- adjustment class;
- amount or other consequence threshold;
- whether the employee may request, approve, post or reconcile;
- prohibited self-approval combinations;
- temporary delegation and expiration;
- evidence required before a decision; and
- escalation owner when the rule does not fit.

The distinction between requesting, approving and posting matters. In a small operation, one person may perform more than one step. That does not eliminate the need to name the steps and address the resulting risk. A compensating review may be appropriate when complete separation is impractical.

The [2025 U.S. Government Accountability Office Green Book](https://www.gao.gov/products/gao-25-107721) is written as federal internal-control guidance, not as a self-storage accounting standard. Its control principles are still useful reference points: assign responsibility and authority, design controls in response to risk, consider segregation of duties, document policies and use quality information. A storage operator must adapt those ideas to its own systems, contracts, laws and professional advice rather than claim Green Book compliance.

## Make every posted adjustment reconstructable

If a reviewer cannot reconstruct the event later, the portfolio has a number without an operating record. A sufficient record should answer:

- What account, facility and original charge were affected?
- What type of adjustment was requested?
- Which facts and source records supported the request?
- Which policy version or authority rule governed the decision?
- Who requested, approved, posted and reconciled the transaction?
- When did each state change occur?
- What amount and effective date were approved?
- What amount and effective date actually posted?
- Did the posting succeed, fail or require reversal?
- What customer communication, if any, was approved and delivered through the proper channel?

NIST Special Publication 800-53 is a security and privacy control catalog, not billing guidance. Its [current control resources](https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/downloads) provide a helpful audit-record pattern: record what occurred, when and where it occurred, its source and outcome, and the identities associated with it. That pattern is a sound minimum for consequential operational events, provided the record avoids unnecessary personal information and follows the organization’s retention and privacy rules.

Free text can supplement this record, but it should not carry the fields needed for routing or comparison. If “duplicate charge,” “service recovery” and “manager courtesy” exist only in prose, the portfolio will spend its review time interpreting notes instead of managing exceptions.

## Govern reason codes like operating definitions

Reason codes tend to multiply. One facility selects “billing error.” Another uses “customer service.” A third chooses “other” and writes the real reason in a note. The portfolio then compares categories that do not mean the same thing.

Each governed reason code needs:

- a plain-language definition;
- the adjustment classes in which it is allowed;
- required evidence;
- authority tier;
- effective date and retirement date;
- code owner;
- examples of what belongs and what does not; and
- a mapping rule for legacy local codes.

Do not rewrite historical transactions when a code definition changes. Retain the code and definition version that governed at the time, then use an explicit mapping for current analysis. If an old code cannot be mapped confidently, mark it unknown. A visible unknown is safer than a clean but invented classification.

The same rule applies when facilities join a portfolio. Local codes should enter a mapping queue. They should not silently inherit the nearest corporate category. Until reviewed, their adjustments can remain available for account servicing while being excluded from cross-facility reason comparisons.

## Reconcile the decision to the ledger

Approval is not the end of the process. The portfolio needs a comparison between what was approved and what actually posted.

For each approved request, test:

| Control question | Expected evidence |
| --- | --- |
| Did the transaction post to the intended account and facility? | Account, facility and transaction identifiers match the approval. |
| Did the amount and effective date match? | Approved and posted values reconcile or an explained variance exists. |
| Was the correct governed reason used? | Reason code and version agree with the decision class. |
| Was the transaction posted once? | One final transaction or a documented reversal-and-repost chain. |
| Was the account state reviewed afterward? | Timestamped readback from the system of record. |
| Did required communication occur? | Approved channel, template or message record without unnecessary sensitive content. |

Exceptions should route by type. A wrong account is different from a missing approver. A duplicate posting is different from an outdated policy version. A single “failed” bucket hides the team that must act next.

The [NIST Cybersecurity Framework 2.0](https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20) emphasizes establishing and communicating roles, responsibilities and authorities as part of governance. It does not prescribe an adjustment workflow. The useful operating lesson is that responsibility must be explicit enough to act on and verify, not merely implied by organization charts.

## Review patterns without turning them into accusations

A portfolio review should surface patterns for investigation, not declare motive or fault from a count. Useful views include adjustments by class, reason, facility, requester, approver, amount band, policy version and reconciliation status. Also track aging for unposted approvals, unreconciled postings and requests awaiting evidence.

Interpret those views carefully. A higher correction count might reflect a system issue, stronger detection, a recent migration or a change in coding practice. A lower courtesy count might reflect tighter policy, missing records or inconsistent use of “other.” The data identifies where to ask better questions. It does not prove why the pattern exists.

Denominators matter as well. Comparing raw adjustment counts across a 300-account facility and a 3,000-account facility is rarely useful. Choose a denominator that fits the question, preserve its source and period, and do not convert association into causation.

## A fictional portfolio example

The following scenario is explicitly fictional. The company, facilities, people and figures are invented for illustration.

Northline Storage Group reviews 41 account adjustments from three facilities. The ledger initially labels all 41 as “credits.” The control review separates 18 corrections, 12 policy-based adjustments, seven discretionary courtesies and four unresolved requests that should not have been reported as posted credits.

One correction points to a duplicate charge and reconciles cleanly. Two policy-based adjustments reference a retired policy version and enter a review queue. A courtesy credit was approved within the manager’s amount limit but posted to the wrong facility. Another transaction was both approved and reconciled by the same person; the portfolio’s control design requires an independent weekly review for that staffing configuration, and the review evidence is missing.

The portfolio does not call those findings fraud, loss or customer harm. It records specific control states: policy-version exception, facility mismatch and missing compensating review. Each exception receives an owner, deadline and resolution test.

That precision makes the operating response possible. It also protects people from conclusions the evidence does not support.

## The practical tool: Portfolio Adjustment Authority Matrix and Review Queue

Use the companion **Portfolio Adjustment Authority Matrix and Review Queue** in two linked parts.

The authority matrix defines, by role and adjustment class, who may request, approve, post and reconcile; applicable limits; required evidence; prohibited combinations; delegation rules; and escalation owners.

The review queue records each request from proposal through reconciliation. It captures the facility, account and source transaction identifiers; classification; governed reason and version; requested and approved values; decision authority; posted transaction; reconciliation result; exception type; owner; due date; evidence link; and final state.

The tool does not decide whether an adjustment is legally required, contractually allowed or properly classified for accounting. Those determinations belong to the organization’s approved policies and qualified reviewers. The tool makes the operating chain visible so the right reviewer receives a complete record.

A portfolio adjustment is complete only when its purpose is classified, its authority is verified, its evidence is retained, the approved transaction posts correctly and the result is reconciled. Anything less is not a finished credit. It is an unresolved control state wearing a dollar amount.

[^1]: U.S. Government Accountability Office, *Standards for Internal Control in the Federal Government*, GAO-25-107721, published May 15, 2025 and effective beginning with fiscal year 2026: https://www.gao.gov/products/gao-25-107721
[^2]: National Institute of Standards and Technology, SP 800-53 Rev. 5 current control resources, including AU-3 and AC-6: https://csrc.nist.gov/Projects/risk-management/sp800-53-controls/downloads
[^3]: National Institute of Standards and Technology, *Cybersecurity Framework 2.0*, published February 26, 2024: https://www.nist.gov/publications/nist-cybersecurity-framework-csf-20
