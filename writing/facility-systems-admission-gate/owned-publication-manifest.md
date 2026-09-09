# Owned publication manifest

## Release target

- Route: `/writing/facility-systems-admission-gate/`
- Canonical: `https://jaredmodstorage.github.io/writing/facility-systems-admission-gate/`
- Publisher: Jared Mastroianni personal authority site
- Schema: `TechArticle` and `BreadcrumbList`
- Author: Jared Mastroianni
- State: package prepared for one publisher handoff; no public mutation yet

## Required public package

- `a-login-is-not-an-admission.md`
- `facility-systems-admission-gate.csv`
- `052-ai-development-ai-engineering-design-review.png`

## Page presentation

- Use the governed title and description in `destination-assignment.md`.
- Place the governed image after the byline with the exact alt and caption in `image-notes.md`.
- Present the CSV as a downloadable operator tool and render one fictional row as a grouped field guide.
- Preserve source notes and the fictional-data disclaimer.

## Release gates

1. Reconfirm the canonical is absent from the live site and current sitemap immediately before mutation.
2. Verify article, CSV and image hashes against `checksums.sha256`.
3. Build and test source locally; verify structured data and all internal/download links.
4. Commit source with a clean rollback parent.
5. Deploy once through the existing Pages route.
6. Read back the canonical, byline, metadata, image, download and sitemap/feed delta at 1440, 390 and 320 pixels.
7. Freeze exact source, deployment, rollback and provider-run identities separately.
8. Do not equate live publication with indexing, coverage or recognition.

