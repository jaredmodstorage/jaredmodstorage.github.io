# Final editorial QA — September 14 evening AI architecture lane

## Decision

**PASS — publication-ready for one governed personal-authority-site handoff.** No publisher, CMS, source repository or Authority Control Room mutation occurred in this run.

## Article identity

- **Title:** *The Same System Should Not Propose, Approve, and Verify: Separation of Duties for Self-Storage AI*
- **Author:** Jared Mastroianni
- **Slug:** `same-system-propose-approve-verify`
- **Destination:** Jared Mastroianni personal authority site only
- **Publisher owner:** Jared Mastroianni
- **Proposed canonical:** `https://jaredmodstorage.github.io/writing/same-system-propose-approve-verify/`
- **Body word count:** 2,041 under the lane-standard rule: count only text between `BODY START` and `BODY END`; exclude numeric footnote markers; count Unicode letter-or-number tokens while retaining internal apostrophes and hyphens.
- **Article SHA-256:** `9094d75f0dfb7c704895d9cbb55ec5a28a60abf1681d4e9725d8f0de1c22ffb2`

## Editorial review

- **Self-storage operator lens — PASS.** The article turns a familiar approval-screen pattern into a facility-specific test across access restrictions, maintenance review, customer communications, account adjustments and emergency gate access without claiming a real deployment.
- **Responsible-AI architecture lens — PASS.** Proposal, authorization, execution, provider receipt, governing readback and reconciliation remain separate. Approval is bound to an immutable decision digest; changed evidence invalidates it; execution uses a narrow disposable credential; the executor cannot certify its own result.
- **Control-design lens — PASS.** The article distinguishes role labels from distinct principals, scales separation to consequence, addresses small-team compensating controls and confines break-glass use through exact scope, expiry and independent follow-up.
- **Voice and claim control — PASS.** The prose is direct, natural and non-promotional. No invented customer, deployment, performance, revenue, occupancy, adoption, certification, award, coverage or recognition claim appears. The scenario, dataset and image are explicitly fictional or AI-generated.
- **Editorial disclosure — PASS.** AI-assisted research and drafting are disclosed, and Jared's approval remains a separate pre-publication gate.

## Practical tool QA

- `ai-decision-separation-register.csv` has 48 unique columns and seven uniform data rows.
- `ADS-BLANK` is one reusable template row with explicit entry prompts.
- `ADS-FIC-001` through `ADS-FIC-006` are six explicitly fictional teaching rows with unique record IDs.
- The tool separates source evidence, model and prompt versions, approval role and independence, approved digest, execution principal and credential, provider receipt, governing readback, verifier independence, reconciliation and break-glass review.
- **Tool SHA-256:** `583d59ed4f5dd336bca43dd5dc864401f989548e73583885a999871bfc465453`

## Source, duplicate and visual QA

- Six primary or authoritative source records map one-to-one to article references 1–6. Every exact registered URL returned HTTP 200 after redirects on September 14, 2026.
- **Source-register SHA-256:** `2f45368909a82ae977bc07c6edc541c8314c35a5436de5bfd16e37d2298552e6`
- Current calendars, public registers, same-day lanes, 72-entry Jared sitemap, 140-entry modSTORAGE post sitemap, 12-item modSTORAGE feed view and active/assigned manuscripts were screened. There is no title, slug, thesis, example or tool collision.
- Across 4,122 other Markdown files, 57 eligible normalized sentences produced zero exact matches. Maximum six-word-shingle overlap was four of 2,090, or 0.191388%.
- Image 054 is a byte-identical 3,840 x 2,560 governed asset and was visually inspected. Its August 30 reuse is disclosed. No author portrait or rejected black-turtleneck treatment appears.
- **Selected image SHA-256:** `4f1b6120c37728d84384ecd711aa9315b7bc44435034a40a1b69dcb48cc96e00`
- Article and tool renders at 1,280, 390 and 320 pixels have zero horizontal overflow, failed images or page errors. The 320-pixel article uses an overlapping continuation capture for complete vertical coverage. The 1,280-pixel article and 320-pixel grouped tool were visually inspected after final copy and CSV validation.

## Final state

The package is publication-ready locally and assigned to one owned destination. No publisher handoff, source-repository mutation, CMS object, deployment, public canonical, sitemap/feed inclusion, search submission, crawling, indexing, ranking, independent coverage, award or recognition is established.
