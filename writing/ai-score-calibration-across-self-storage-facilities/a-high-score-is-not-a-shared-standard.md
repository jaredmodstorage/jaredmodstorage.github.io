# A High Score Is Not a Shared Standard: How Self-Storage Teams Should Calibrate AI Across Facilities

**Deck:** Before one AI threshold controls staffing, maintenance, collections or customer communication, an operator needs to know what the score means at each facility.

**By Jared Mastroianni**

A portfolio review shows two self-storage facilities with the same AI score: 0.82. At the first site, the score points to a work order that is likely to reopen within two weeks. At the second, it points to a task that is merely more urgent than the others in that site's queue.

The numbers look comparable. They may not even mean the same thing.

An AI score is often treated as a portable fact. It is placed beside a facility name, sorted from high to low and converted into a common threshold. The clean dashboard creates the impression that 0.82 at one property carries the same meaning, evidence and consequence as 0.82 everywhere else.

That assumption is safe only when the portfolio has proved it.

A useful score needs a calibration record: the decision it supports, the outcome it predicts, the population and period used to test it, the model and feature version, the observed error pattern, the threshold, and the owner who can release or stop the resulting action. Without that record, a portfolio may be ranking interface numbers rather than comparable operating risk.

## Begin With the Decision, Not the Decimal

The first question is not whether the score is high. It is what the score is allowed to do.

A maintenance-priority score might reorder a manager's review queue. A collections score might determine which accounts receive an internal review. A customer-message classifier might route a draft to an employee. A safety-related signal might only create an observation request for qualified personnel. Those are different uses with different costs when the model is wrong.

Google's machine-learning guidance explains that precision, recall and accuracy change with the classification threshold, and that the useful metric depends on the costs, benefits and risks of the problem.[^1] Its thresholding guide separately shows that a raw probability becomes an operating class only after a threshold is chosen.[^2] These are educational materials, not self-storage rules. They establish a practical point: a score does not choose its own action.

Record the permitted decision and consequence before reviewing model performance. “Prioritize for manager review” is materially different from “send a customer message,” “dispatch a vendor” or “change access.” If the action is not named, the number has no defensible operating boundary.

## Define the Outcome the Model Is Trying to Predict

The same label can hide different events.

Consider **repeat service**. One facility may count any new work order on the same unit within 14 days. Another may count only a reopening of the original ticket. A third may exclude vendor callbacks, tenant-caused conditions or administrative duplicates. Each definition could be locally deliberate. They cannot support one portfolio score until the differences are exposed and resolved.

The outcome record should name:

- the positive event;
- the unit of analysis, such as a unit, work order, account, message or facility-day;
- the observation window;
- exclusions and cancellations;
- who establishes the final label; and
- how corrections are applied after the fact.

This is the ground-truth contract. It does not prove that the label is perfect. It makes the intended meaning testable. When two sites use different definitions, the honest state is **not comparable**, not an averaged compromise.

## Test the Population Behind the Score

Even a shared label can behave differently across facilities. A climate pattern, unit mix, access configuration, staffing model, customer-contact channel, vendor process or local operating rule can change the population seen by the model. A rare event at one site may be common enough to evaluate at another. A new property may have too little settled history for a local conclusion.

NIST's Artificial Intelligence Risk Management Framework describes trustworthy AI in terms that include validity, reliability, transparency and accountability, and it treats risk management as voluntary, use-case specific and continuous.[^3] The framework's Measure function calls for performance or assurance criteria to be demonstrated under conditions similar to deployment settings and informed by domain experts.[^4] It does not certify a model or prescribe a facility threshold.

For a portfolio review, preserve the test population for each facility or relevant site group:

- start and end dates;
- number of eligible records;
- number of confirmed positive and negative outcomes;
- excluded, unresolved and corrected records;
- feature coverage;
- major operating conditions; and
- the latest period that was not used to fit the model.

Small or unstable samples belong in an **insufficient evidence** state. They should not be forced into a green score simply because a dashboard expects one number per facility.

## Separate Ranking From Probability

Some models are good at ordering cases without producing probabilities that can be read literally. A score of 0.82 may mean “higher than most other cases” rather than “an 82 percent chance of the event.”

The scikit-learn probability-calibration guide defines a well-calibrated binary classifier as one where cases receiving a predicted probability near 0.8 produce the positive event about 80 percent of the time. It also explains that calibration should be evaluated on data separate from the data used to fit the model.[^5] That documentation describes software methods, not a universal operating requirement or proof that any particular model is calibrated.

The operator does not need to choose a calibration algorithm. The operator does need an answer to a simpler question: is the number a probability, a rank, a distance from a boundary, a rules score or a vendor-defined index?

If the answer is unknown, display the number as an opaque score and restrict its use. Do not add a percent sign. Do not tell a manager that the event is “82 percent likely.” Do not compare it across facilities until the score meaning and evaluation evidence are aligned.

## Put the Threshold Beside Its Error Costs

A threshold converts a score into work. That conversion needs an owner.

Suppose an AI-assisted maintenance queue has two possible mistakes. A false positive sends a manager to review a work order that would not have reopened. A false negative leaves a likely repeat problem lower in the queue. The costs are not equal, and they may change with the consequence.

For a low-risk review queue, the portfolio might tolerate more false positives to find more possible problems. For a customer-facing communication, access change or safety-related escalation, the release rule may require different evidence and mandatory human authority. The model score should not silently broaden the action.

NIST Special Publication 1270 notes that bias can enter across technical and human processes and can produce harmful outcomes even without harmful intent.[^6] The publication is broad and not a finding about self-storage. It reinforces why a portfolio should inspect who and what is helped, delayed, over-selected or missed by a threshold rather than relying on one average metric.

Record, for each permitted use:

- threshold and model version;
- precision, recall or other relevant measures at that threshold;
- false-positive and false-negative consequences;
- groups or site conditions reviewed;
- human review requirement;
- release owner; and
- rollback or stop condition.

## A Fictional Nine-Site Review

The following example is fictional and demonstrates the method only.

Ridgefield Storage Group tests a model that prioritizes completed maintenance work orders for possible repeat service within 14 days. The output is advisory; a manager reviews the underlying work order before any assignment changes.

At the portfolio meeting, three facilities appear to have many scores above 0.80. The calibration review finds three different problems.

At Site A, **repeat service** includes every later work order on the same unit, even when the issue is unrelated. The label contract is not aligned with the other sites.

At Site B, the model version is current, but the last evaluation period includes only a small number of confirmed repeat events. The evidence is insufficient for a site-specific threshold.

At Site C, scores rank work correctly enough for review, but the values were never tested as probabilities. A score of 0.82 cannot be described as an 82 percent likelihood.

The team does not manufacture one portfolio result. Site A returns to label reconciliation. Site B remains in shadow review while more outcomes mature. Site C may use the score for bounded queue ordering, but the interface removes probability language. The other six sites continue only under their recorded model, threshold and human-review rules.

No deployment, customer result, performance improvement or model accuracy is claimed. Every facility, score, threshold and outcome in the example is fictional.

## Use a Site-Level Calibration Record

A calibration review can fit into one operating table. The companion checklist for this article contains 12 gates, from decision scope through correction and revalidation.

At minimum, each row should preserve:

1. **Decision and consequence:** What can the score change?
2. **Outcome contract:** What exact event is positive, over what window?
3. **Population:** Which records and operating conditions were evaluated?
4. **Model identity:** Which model, features and version produced the score?
5. **Score meaning:** Probability, rank, rules score or another defined output?
6. **Threshold evidence:** Which measures apply at the chosen cut point?
7. **Local sufficiency:** Is there enough settled evidence for this site or group?
8. **Human authority:** Who reviews and who can release the action?
9. **Channel language:** Does the interface describe the score accurately?
10. **Drift trigger:** What change forces revalidation?
11. **Correction path:** How are labels, thresholds and prior decisions corrected?
12. **Stop state:** What makes the score advisory-only, shadow-only or unavailable?

The record should be revalidated after a model or feature change, a label-definition change, a material shift in operating conditions, a threshold change, a sustained performance change or a correction that affects the evaluation set. Routine reports that do not use model scores to compare facilities or trigger consequential work do not need this control.

## Make the Portfolio Earn the Shared Threshold

One threshold across every facility may eventually be appropriate. It should be the result of evidence, not the default created by a dashboard.

The portfolio has earned a shared threshold when the decision, outcome, population, model version, score meaning, evaluation window, error costs and release authority are aligned—or when documented grouping evidence supports the remaining differences. Until then, the interface should preserve the narrower truth: locally calibrated, ranking-only, insufficient evidence, shadow review, or not comparable.

That restraint does not make AI less useful. It keeps a clean number from outrunning its meaning.

---

**Proposed slug:** `ai-score-calibration-across-self-storage-facilities`

**Publication state:** Complete local draft. No WordPress object, upload, schedule, publication, search submission, indexing, coverage or recognition exists for this package.

[^1]: Google for Developers, “Classification: Accuracy, recall, precision, and related metrics,” current page checked September 1, 2026. https://developers.google.com/machine-learning/crash-course/classification/accuracy-precision-recall
[^2]: Google for Developers, “Thresholds and the confusion matrix,” current page checked September 1, 2026. https://developers.google.com/machine-learning/crash-course/classification/thresholding
[^3]: National Institute of Standards and Technology, *Artificial Intelligence Risk Management Framework (AI RMF 1.0)*, NIST AI 100-1, January 2023; current publication page checked September 1, 2026. NIST states that AI RMF 1.0 is being revised. https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-ai-rmf-10
[^4]: NIST AI Resource Center, “AI RMF Core,” current page checked September 1, 2026. https://airc.nist.gov/airmf-resources/airmf/5-sec-core/
[^5]: scikit-learn, “Probability calibration,” stable documentation checked September 1, 2026. https://scikit-learn.org/stable/modules/calibration.html
[^6]: National Institute of Standards and Technology, *Towards a Standard for Identifying and Managing Bias in Artificial Intelligence*, NIST SP 1270, March 2022; publication page checked September 1, 2026. https://www.nist.gov/publications/towards-standard-identifying-and-managing-bias-artificial-intelligence
