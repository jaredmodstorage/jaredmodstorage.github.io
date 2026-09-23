# Same Name, Different Customer: A No-Guessing Rule for Linking Records Across Self-Storage Sites

**Deck:** A familiar name can identify a candidate for review. It cannot establish that two facility records describe the same person, authorize a link, or permit one record to overwrite another.

By Jared Mastroianni

Two self-storage facilities can hold customer records for “Alex Morgan.” The names match. The email addresses look similar. The street addresses once matched. A portfolio system may rank the pair as a likely duplicate.

That is a useful lead. It is not an identity decision.

Cross-site record linking becomes risky when a probability is treated as permission. A false link can expose one customer’s information to another, connect the wrong balance or access history, misdirect a collection action, or cause an employee to discuss the wrong agreement. A missed link can leave a legitimate customer repeating information and make portfolio support harder. The answer is neither “merge everything” nor “never connect anything.” It is a controlled review that separates evidence, purpose, scope and downstream authority.

The operating rule is simple: **a possible match may open a review; only sufficient governed evidence can close it.** Even a confirmed same-person decision does not automatically authorize a destructive merge or any change to contracts, access, payments or notices.

## Separate the three questions

A reliable process asks three questions in order.

1. **Do the records describe the same person?** This is the identity question.
2. **May the records be linked for the stated operating purpose?** This is the authority and privacy question.
3. **What may the link change?** This is the action-scope question.

These questions are related, but they are not interchangeable. A customer can be the same person at two facilities while holding separate agreements, payment methods, access credentials and authorized-user lists. A portfolio may be permitted to show a support representative that both records exist without being permitted to combine financial histories. A confirmed relationship may improve navigation while leaving every source record intact.

The process therefore needs two distinct outputs: an identity decision and an allowed-use decision. “Same person” is not shorthand for “merge,” “share everything” or “act everywhere.”

## Start with minimum necessary evidence

The [National Institute of Standards and Technology’s digital identity guidance](https://pages.nist.gov/800-63-4/sp800-63a.html) separates identity resolution, evidence validation and identity verification. It also says personal information processing should be limited to the minimum necessary for the transaction. That publication governs digital identity services; it is not a self-storage customer-merging standard. Its separation of tasks is still useful: finding a candidate, checking evidence and reaching a decision are different events.

For a self-storage portfolio, a candidate may arise from a shared name, contact detail, mailing address or internal reference. None of those alone should become a silent match rule. Names repeat. Telephone numbers are reassigned. Households share addresses. Email aliases resemble one another. Data imports copy old values. Staff correct spelling at one facility but not another.

The review should use the least information that can answer the stated question. It should not collect a Social Security number, payment-card detail, government document or other sensitive data merely because two records look similar. The [Federal Trade Commission’s business guidance](https://www.ftc.gov/business-guidance/resources/protecting-personal-information-guide-business) advises companies not to keep sensitive consumer information without a legitimate business need and to limit access to it. That guidance is general; applicable contracts, law and approved company policy still control the real workflow.

Useful evidence can include a stable customer-controlled reference already created through an approved process, confirmation through a validated contact channel, or a governed source that the operator is authorized to consult. The reviewer records the evidence reference and limitation—not a copy of every underlying personal detail.

## A candidate score is not a conclusion

Matching software may calculate similarity across fields. That can help prioritize a queue, but the score needs an explicit boundary.

A name-and-address match can be persuasive for one purpose and inadequate for another. A high score can still connect a parent and adult child, two former residents of the same apartment, or the old and new holders of a recycled telephone number. A low score can separate one person whose name, phone and address all changed.

The score should therefore answer only: **Which pairs deserve controlled review first?** It should not answer: **Which records may be combined?**

Automation must preserve an unknown state. When evidence conflicts or remains incomplete, the correct result is **insufficient evidence** or **link withheld**, not a forced yes or no. That state prevents a missing fact from silently becoming a positive match.

## Use a small, exact state vocabulary

A portfolio review can be managed with a compact set of states:

- **Unreviewed:** no governed assessment has occurred.
- **Candidate:** a defined rule identified records for review.
- **Confirmed same person:** sufficient evidence supports the identity decision for the stated purpose.
- **Confirmed different people:** sufficient evidence shows the records should remain separate.
- **Insufficient evidence:** the available evidence cannot support either conclusion.
- **Link withheld:** an identity conclusion may exist, but authority, privacy or scope does not permit the proposed link.
- **Correction open:** a prior decision or downstream use requires review and remediation.

Every decision should carry a version, reviewer role, time, purpose, evidence references, known conflicts, permitted scope and correction route. Earlier states remain visible. A correction supersedes a decision; it does not erase the record of why the original action occurred.

## Link without collapsing the source records

The safest default is a non-destructive link. Each facility keeps its source record and stable identifier. A separate portfolio record states that two source records were reviewed and, when supported, describes the relationship and the uses permitted.

This distinction protects operational meaning. Person identity is not the same as:

- contract party or authorized user;
- access credential holder;
- unit occupant;
- payment-account owner;
- notice recipient;
- lien or collection subject; or
- marketing consent.

Each of those claims needs its own source, authority and effective state. A person-level link can help an authorized employee find the right records. It cannot manufacture a cross-facility authorization that the underlying agreements do not contain.

Destructive merging should require a separate, higher-control process. It must identify the surviving record, retained source identifiers, field-level precedence, reversible backup, downstream dependencies, approval owner and readback evidence. If the team cannot explain how to undo the change, it is not ready to collapse records.

## A fictional two-site review

Consider an entirely fictional portfolio with Harbor Ridge East and Harbor Ridge North. Each facility has a record for “Alex Morgan.” The first record uses `ALEX.MORGAN@example.test`; the second uses `alexmorgan@example.test`. Both list the same fictional apartment building from different years.

The system creates candidate `CRM-FIC-204`. The queue shows a strong name similarity, a similar-looking email and historical address overlap. It does not join the records.

An authorized reviewer first confirms the operating purpose: allow the central support team to locate all active facility relationships when a customer requests help. The reviewer checks the minimum governed references. One validated contact channel reaches Alex Morgan at Harbor Ridge East. A separate validated contact reaches a different Alex Morgan at Harbor Ridge North. The shared address is a large apartment building, and the email strings belong to separate accounts.

The decision is **confirmed different people**. The candidate is closed, the source records remain separate, and no customer attribute is copied between them. The portfolio also records why the similarity rule generated the candidate so the model can be evaluated without rewriting the historical decision.

Every person, facility, identifier, address, contact detail and decision in this example is fictional. The example shows the control sequence, not a real match rate, customer event or product capability.

## Put an owner on every consequential use

A cross-site link should name who owns the identity decision and who owns each downstream use. Those roles may differ.

Operations may own support navigation. Privacy or legal leadership may define permitted data use. Accounting may control customer-balance treatment. Facility leaders may control access and authorized-user changes. Information technology may own the technical link and correction propagation.

The link record should state which audience can see it and which actions remain held. “Portfolio use” is too vague. An allowed scope might be: “central support may view the existence of both records after authenticating the customer; contracts, access, balances, notices and marketing permissions remain facility-specific.”

That sentence is operationally stronger than a generic “duplicate resolved” flag because it tells the next employee what the decision does and does not permit.

## Revalidate when the facts or use change

A correct link can become stale. A customer changes a phone number. A facility migrates systems. A record is reassigned after a business acquisition. The portfolio adds a new use that was never part of the original decision.

Revalidation should occur when:

- a material identifier or governed source changes;
- evidence conflicts with the current conclusion;
- a new facility record joins the candidate group;
- the proposed audience or operating purpose expands;
- a customer disputes the relationship;
- a system migration changes identifiers or precedence; or
- a downstream action fails readback.

The [NIST Privacy Framework](https://www.nist.gov/privacy-framework) is a voluntary tool for managing privacy risk. It does not certify a self-storage linkage process. Its risk-management framing supports a practical point: a technically accurate relationship can still create privacy risk when used outside its recorded purpose or audience.

## A practical portfolio sequence

At the next portfolio review, use this order:

1. **Name the purpose.** State the exact decision or customer-support need.
2. **Open a candidate.** Record why the pair was surfaced; hold automated merging and consequential action.
3. **Minimize the evidence.** Use only approved references necessary for the decision.
4. **Validate conflicts.** Preserve facts that disagree instead of averaging them away.
5. **Decide identity.** Choose one exact state, including insufficient evidence when appropriate.
6. **Authorize scope.** Record audience, allowed use and actions that remain prohibited.
7. **Read back effects.** Confirm source records, contracts, access, balances and notices did not change outside scope.
8. **Keep correction open.** Give the customer and staff a route to dispute or repair the relationship.

The accompanying **Cross-Site Customer Record Link Review** provides a decision view, a detailed append-only register and field guidance. Its examples are fictional and intentionally exclude real personal information.

The portfolio standard is not perfect matching. It is controlled uncertainty. A system may propose that two records belong together. The operator must still establish the identity conclusion, the permission to link and the exact actions the link authorizes. When the evidence cannot carry that weight, the responsible answer is not a guess. It is a visible hold.

---

## Operator tool

Download the **Cross-Site Customer Record Link Review** as an XLSX workbook or CSV register. A responsive, passive HTML reference presents the same fictional review sequence for browser use.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai. His work focuses on facility operations, multi-location systems, data governance and responsible artificial intelligence.

## Production note

This article and its operator tool were produced with AI assistance under human direction and review. The governed editorial image is AI-generated and is not documentary evidence of a real customer, facility or identity decision.
