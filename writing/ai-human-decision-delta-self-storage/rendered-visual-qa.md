# Rendered visual QA

## Evidence reviewed

- `qa-render/article-1280.png`
- `qa-render/article-390.png`
- `qa-render/article-320.png`
- `qa-render/render-metrics.jsonl`
- `qa-render/article-preview.html`

## Automated observations

| Viewport | Horizontal overflow | Loaded governed image | Empty links | Source links | Full-page height |
|---|---:|---|---:|---:|---:|
| 1280 px | 0 px | 3840 × 2560 | 0 | 4 | 7,899 px |
| 390 px | 0 px | 3840 × 2560 | 0 | 4 | 12,304 px |
| 320 px | 0 px | 3840 × 2560 | 0 | 4 | 14,099 px |

## Visual inspection

- Desktop composition is balanced: the editorial image, title block, left architecture rail, main article and practical-tool note remain visually distinct.
- The 390 px and 320 px layouts collapse to one column without clipping, hidden body text or horizontal overflow.
- Heading hierarchy remains legible at all sizes; paragraphs, lists, source notes, author block and disclosure remain readable.
- The image is not stretched, its governed crop is preserved and the exact alt text is present.
- Navy, white, gold and blue treatments maintain strong visual separation. Links remain underlined and are not distinguished by color alone.
- The historical slot is not presented as the publication date; the visible byline date is October 27, 2026.
- No rejected black-turtleneck portrait or author-profile treatment appears.

## Score

**9.7/10 — pass.** The render is polished, responsive and publication-ready. Final production QA must still verify the publisher's actual template, canonical, assets, metadata, links, sitemap/feed inclusion and responsive behavior after integration.
