# Owned publication manifest

## Release target

- Route: `/writing/when-guardrails-disagree/`
- Canonical: `https://jaredmodstorage.github.io/writing/when-guardrails-disagree/`
- Publisher: Jared Mastroianni personal authority site only
- Publisher owner: Jared Mastroianni
- Schema: `TechArticle`, `ImageObject` and `BreadcrumbList`
- Author: Jared Mastroianni
- State: publication-ready local package only; no publisher handoff or public mutation
- Excluded owned publisher: modSTORAGE WordPress blog must reject the same complete article, title, slug, body and practical tool as a duplicate

## Required public package

- `when-guardrails-disagree.md`
- `policy-decision-reconciliation-register.csv`
- `source-register.csv`
- `052-ai-development-ai-engineering-design-review.png`
- `image-notes.md`

## Presentation requirements

- Preserve the title, deck, byline, editorial disclosure and exact source limitations.
- Place the governed image after the byline with the exact alt text and caption from `image-notes.md`.
- Present the CSV as a downloadable operator tool and preserve the template and fictional-row labels.
- Preserve `PERMIT`, `DENY`, `INDETERMINATE`, `NOT_APPLICABLE` and the authored `REVIEW` extension as different states.
- Do not describe the proposed decision lattice as XACML compliance, a product feature, deployment, standard, audit, certification, legal conclusion or measured operating result.

## Separate release gates

1. Reconfirm the title, route, slug, Alder Bend example and register are absent immediately before any publisher mutation.
2. Verify every governed hash against `checksums.sha256`.
3. Build and test the source locally; verify structured data, internal links, source links, download and image.
4. Commit source with a known rollback parent.
5. Deploy once through the established personal-authority-site workflow.
6. Read back the canonical, H1, byline, disclosure, image, download, metadata, sitemap and feed at desktop and mobile widths.
7. Record source, deployment, rollback and provider-run identities separately.
8. Keep publication, crawling, indexing, ranking, coverage and recognition as separate states.

