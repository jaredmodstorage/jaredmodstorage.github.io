# Rendered visual QA — corrected revision

## Result: 9.8/10 — pass

The corrected Markdown was rendered afresh with the governed image at 1280, 390 and 320 pixels. The full desktop and narrowest mobile captures were visually inspected after the technical correction; the 390-pixel render was also measured by the same renderer.

## Verified

- Zero horizontal overflow at all three viewports.
- The exact 3840 × 2560 governed image loaded at every viewport with meaningful alt text.
- Five source links rendered and no link was empty.
- The hero title, deck, byline, actual October 27 date and section hierarchy remain legible.
- The desktop layout retains a stable reading measure; the annotation rail and tool card remain separate from the body.
- At 390 and 320 pixels, side material collapses cleanly, the hero stacks and the article remains readable without sideways scrolling.
- The corrected Harbor Pike intervals and the practical-tool section render without clipping or table overflow.
- One visible hero H1 is followed by a consistent H2 hierarchy.
- The image remains framed as AI-generated editorial art, not documentary evidence.

## Artifacts

- `qa-render/article-1280.png`
- `qa-render/article-390.png`
- `qa-render/article-320.png`
- `qa-render/article-preview.html`
- `qa-render/render-metrics.jsonl`
- `qa-render/render-preview.mjs`

This local render demonstrates editorial-layout readiness. It does not establish repository integration, deployment, public availability or the publisher's final production rendering.
