# Editorial review scores

Scores use a direct 10-point publication-readiness scale. They are reasoned editorial judgments, not independent external endorsements.

## Review 1 — Architecture and operational consequence

- **Score:** 9.7/10
- **Finding:** The article isolates a subtle failure: accurate source records can still form an impossible composite. It gives the operator a usable architecture—explicit as-of boundary, fact-validity envelopes and identity/validity/completeness/order gates—without claiming a universal distributed snapshot.
- **Strengths:** Freshness and coherence remain separate; local database guarantees are not generalized across providers; failed joins have actionable dispositions.
- **Revision made:** Strengthened the distinction among effective, observation, event, record, retrieval and decision time.

## Review 2 — Claims, sources and originality

- **Score:** 9.6/10
- **Finding:** Five primary or authoritative sources support narrow technical concepts and carry explicit limitations. No standard is used as certification or as proof that the proposed architecture works.
- **Strengths:** Fictional Maple Quay facts reconcile with the CSV; no invented customer, deployment, performance or compliance claim; zero 14-word sentence matches and 0.242% maximum six-word-shingle overlap.
- **Revision made:** Clarified that RFC 3339 governs representation, CloudEvents does not guarantee cross-system ordering, and PostgreSQL transaction behavior is vendor-specific and local.

## Review 3 — Voice, utility and publication quality

- **Score:** 9.7/10
- **Finding:** The opening makes the failure concrete without sensationalism. The state vocabulary and test can be used by an operations or architecture team immediately, while the prose remains readable for a non-specialist leader.
- **Strengths:** Direct headline, mature voice, useful fictional example, compact tool, clear stop condition and restrained disclosure cadence.
- **Revision made:** Added semantic h3 subsections for both the four join tests and three controlled test cases.

## Rendered visual review

- **Score:** 9.6/10
- **Evidence:** Full-page renders visually reviewed at 1280px, 390px and 320px.
- **Passes:** No horizontal overflow; governed image loaded; self-canonical present; 12 article h2 headings, 7 article h3 headings and 5 clickable external-source links detected at every width. Desktop hierarchy, mobile reading width, roundtable image, caption, rail cards, sources and footer remain legible.
- **Contrast:** All audited preview text pairs pass at 4.52:1 or higher; primary body text is 14.15:1 and white-on-navy is 16.50:1.
- **Artifacts:** `render-1280.png`, `render-390.png`, `render-320.png`, `render-audit.json`, `contrast-audit.json` and `preview.html`.
- **Limitation:** Package-preview evidence is not proof of the publisher's live template, deployment or public responsive state.
