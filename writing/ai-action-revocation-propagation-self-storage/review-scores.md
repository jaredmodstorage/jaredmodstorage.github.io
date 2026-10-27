# Editorial review scores

All scores use a direct 10-point publication-readiness scale. They are editorial judgments, not independent external endorsements.

## Review 1 — Architecture and operator consequence

- **Score:** 9.7/10
- **Finding:** The article identifies a real systems boundary without turning the model into the whole system. It connects versioned authorization, queues, workers, connectors, target receipts and physical or human consequences in a sequence an operator can audit.
- **Strengths:** The commit-boundary distinction is operationally precise; `unknown` is protected from being mislabeled; the fictional two-race example reconciles with the tool and data.
- **Revision made:** Clarified that cancellation is the operator request while revocation is the durable control state; separated pre-commit prevention from post-commit recovery.

## Review 2 — Claims, sources and originality

- **Score:** 9.6/10
- **Finding:** Technical claims are bounded to five current primary or authoritative sources, with direct links and explicit limitations. Standards are used for their actual scope rather than as borrowed certification.
- **Strengths:** Every scenario detail is labeled fictional; no customer, deployment, product, performance, compliance or endorsement claim appears; the title, thesis, example and tool are distinct from the public and local corpus.
- **Revision made:** Added explicit limits that OpenTelemetry context is not authorization and CloudEvents does not define business revocation semantics.

## Review 3 — Voice, utility and publication quality

- **Score:** 9.7/10
- **Finding:** The writing is direct, mature and useful to an operator, architect or technical leader. It avoids generic AI commentary and turns a narrow failure mode into a concrete test.
- **Strengths:** Strong opening, clean state vocabulary, practical checklist, separate CSV implementation record, restrained disclosure cadence and a decisive conclusion.
- **Revision made:** Added semantic h3 subsections for the queued, executing-before-commit and at-or-after-commit cases so the implementation section scans well on production pages.

## Rendered visual review

- **Score:** 9.6/10
- **Evidence:** Full-page renders reviewed at 1280px, 390px and 320px.
- **Passes:** No horizontal overflow; image loaded at every width; canonical present; 11 semantic h2 headings, 3 semantic h3 headings and 5 clickable external source links detected at every width. Desktop hierarchy, mobile line length, caption, rail card, source list and footer remained legible.
- **Artifacts:** `render-1280.png`, `render-390.png`, `render-320.png`, `render-audit.json` and `preview.html`.
- **Limitation:** This is package-preview evidence, not proof of the publisher's live template, deployment or public responsive state.
