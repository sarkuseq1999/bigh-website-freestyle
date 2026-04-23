# Design References

Drop anything that inspires you for this project's UI/UX into this folder. Claude scans this folder before doing any new design work.

## What goes here

| File type | What it represents |
|-----------|--------------------|
| `*.png` / `*.jpg` / `*.webp` | Screenshots, mockups, exported images of designs you like |
| `*.md` (sibling to an image) | Notes about that image — what you like, what you don't, what to copy, what to ignore |
| `links.md` | URLs to live sites you want Claude to fetch and analyze |

## Naming convention

Use descriptive, hyphenated names that hint at what the reference is:

- `apple-product-page.png` ✅
- `linear-pricing-cards.jpg` ✅
- `stripe-nav-hover.png` ✅
- `screenshot.png` ❌ (too vague)
- `IMG_1234.png` ❌ (no hint of content)

## Pairing images with notes

If you want to tell Claude *why* a reference matters, drop a markdown file next to the image with the **same base name**:

```
apple-product-page.png       ← the screenshot
apple-product-page.md        ← your notes:
                               "Love the alternating black/gray sections.
                                Use this rhythm. Ignore the nav blur — too heavy."
```

Without notes, Claude will infer; with notes, Claude follows your direction.

## Aesthetic spec vs. inspiration

- **DESIGN.md** (project root) — the binding rules every UI must follow (colors, typography, spacing)
- **design-references/** (this folder) — raw inspiration that *informs* the spec but is not itself binding

If a reference here contradicts DESIGN.md, DESIGN.md wins. To change the spec, update DESIGN.md.
