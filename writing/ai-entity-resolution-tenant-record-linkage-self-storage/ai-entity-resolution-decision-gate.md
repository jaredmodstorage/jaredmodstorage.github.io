# AI Entity-Resolution Decision Gate

Use this gate when an AI or rules service proposes that two self-storage records refer to the same person or organization. Complete it before a proposed relationship can change access, money, communications, account history or another operating state.

## Decision sequence

1. Identify both source records by source system, facility, local ID and observed version.
2. State the permitted purpose and consequence class for this review.
3. Record the candidate-generation rule, feature-set version, model or rules version and threshold meaning.
4. Separate exact agreements, normalized agreements, conflicts, missing values, reused values and stale evidence.
5. Choose one state: candidate, limited link, reject, request evidence, refer or merge.
6. Record the reviewer role, authority source, reason code, decision time and evidence references.
7. List allowed effects and prohibited effects. A link does not inherit access, consent, balance or communication authority unless policy expressly allows it.
8. Record the reversal method and every downstream dependency that consumes the relationship.
9. Set expiration, revalidation triggers, monitoring owner and correction route.

## Decision rules

- A score is never the only evidence recorded.
- Missing values are not treated as agreements.
- Reused phone numbers, emails and addresses are surfaced as ambiguity, not hidden inside a score.
- Identity resolution does not establish that the present person owns the identity or is authorized for the requested action.
- A material conflict invokes the approved hold or handback rule regardless of aggregate score.
- Source records remain intact unless a separately authorized merge procedure governs their disposition.
- A rejected pair can be recorded as known different people for a scoped rule version without falsifying either source record.
- A wrong link must be reversible, and its dependent effects must be discoverable.

The blank CSV is a template. The fictional example demonstrates structure only. It does not prescribe evidence, thresholds, legal requirements or vendor behavior.
