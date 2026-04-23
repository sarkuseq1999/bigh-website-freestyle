# Reference: Seed.com Navbar

**Source:** https://seed.com/ (top navigation)
**Role:** Primary reference for this project's navbar

## What the user loves

The hover interaction on the "Shop" nav item. When the mouse hovers "Shop", a floating dropdown panel reveals the product catalog — each row shows:

- A small **product thumbnail** on the left (jar / container photography)
- The **product code** on the first line (e.g., "DS-01", "DM-02", "AM-02")
- The **product name** on the second line, bolder (e.g., "Daily Synbiotic", "Daily Multivitamin")
- An **optional badge** next to some items (e.g., "Save 25%" green pill on "Daily Essentials Duo")

The dropdown uses a **glassmorphic treatment** — translucent white surface with background blur so the page behind bleeds softly through.

## Observed visual details (from screenshot)

### Top bar
- Minimal horizontal layout
- Left: brand logo ("Seed" wordmark)
- Center-left cluster: nav links ("Shop", "Science", "Learn")
- Right: utility links ("Login", account icon)
- Active nav item ("Shop" in the screenshot) shows a **filled pill background** — the pill shape, not a rectangle
- Other links are plain text, no underline, low chrome

### Hover dropdown panel
- Appears anchored beneath the hovered nav item
- **Light/translucent surface** — appears white-ish with heavy background blur (frosted glass)
- **Subtle rounded corners** on the panel
- **Tight vertical rhythm** — rows are compact, ~60–70px tall, very little wasted space
- **No visible borders** between rows — spacing creates the separation
- Thumbnails are small (~40–48px square), product photography on solid-ish colored fields matching each product's brand color (dark green, gold, white, light green, etc.)
- Product code is **smaller, lighter** than the name — feels like a label/SKU
- Product name is **bolder** — the primary label
- Badge ("Save 25%") is a small green pill, inline with the product name row

## What to adopt for this project's navbar

- ✅ The **hover-reveal product menu** with thumbnail + code + name structure
- ✅ The **glassmorphic panel treatment** (backdrop-blur + translucent background) — already compatible with DESIGN.md's translucent nav language
- ✅ The **pill background on active nav item** — fits DESIGN.md's 980px pill radius convention
- ✅ **Product photography on solid color fields** for thumbnails — already aligned with DESIGN.md
- ✅ The **tight vertical rhythm** inside the dropdown — minimal row height, no borders

## What to adapt (to stay within DESIGN.md)

- DESIGN.md specifies the navbar itself should be **dark translucent glass** (`rgba(0,0,0,0.8)` + `backdrop-filter: saturate(180%) blur(20px)`) — Seed's outer nav appears lighter in the screenshot, but we can keep Seed's dropdown style while our outer bar follows DESIGN.md's dark-glass rule
- DESIGN.md's typography uses SF Pro (fallback Helvetica Neue) — not the font Seed uses
- DESIGN.md's accent color is Apple Blue (`#0071e3`) — if we need a "sale" or "save" badge equivalent, use Apple Blue, not Seed's green

## Products to show in our dropdown

From [public/products/](../public/products/):
1. `advanced-opc-formula.png` — Advanced OPC Formula
2. `deer-horn-reishi.png` — Deer Horn Reishi
3. `green-bee-propolis.png` — Green Bee Propolis
4. `nature-calm.png` — Nature Calm
5. `nuricell.png` — NuriCell
6. `super-green.png` — Super Green
7. `turmerific.png` — Turmerific

We'll need short product codes (equivalent to Seed's "DS-01" style) once the user decides on SKU conventions.

## Screenshot

Save the user's attached screenshot as `seed-navbar.png` in this folder alongside these notes (user action — I can describe the image but can't write image bytes from the chat attachment).
