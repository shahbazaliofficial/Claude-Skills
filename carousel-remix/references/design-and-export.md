# Design & Export

## Target dimensions

Ask which platform if not already stated — dimensions differ and using the wrong one means the user has to redo it:

- **LinkedIn document carousel**: 1080×1350 px (4:5 portrait) is the safe standard; 1080×1080 (square) also works if the user prefers it.
- **Instagram carousel**: 1080×1350 px (4:5 portrait) is standard and shows largest in-feed; 1080×1080 (square) is the other common choice.

Confirm which one if the user hasn't specified, rather than defaulting silently — square vs. portrait changes the whole layout.

## Brand theme inputs

Before building, have (or ask for): primary/accent colors (hex if possible), font preference (or a style direction like "bold sans-serif" / "elegant serif" if no specific font), logo file if it should appear on slides, and general style direction (bold/minimal/playful/corporate). Read the `frontend-design` skill for general visual polish principles regardless of the specific theme given.

## Build pipeline

Use the `pptx` skill's `pptxgenjs` approach to build the deck, but with a **custom slide size matching the target aspect ratio** rather than a standard 16:9/4:3 presentation size — set `defineLayout` with a width/height in inches that matches the target aspect ratio (e.g., for 1080×1350 px / 4:5, an 8in × 10in custom layout keeps the same ratio). The exact inch values don't need to match the pixel count — the final resize step (below) fixes the precise pixel dimensions.

Steps:
1. Build the deck (one slide per carousel slide, same count as the source) using `pptxgenjs` per the `pptx` skill's conventions, with the custom layout size set once at the top.
2. Convert to PDF: `scripts/office/soffice.py --headless --convert-to pdf <file>.pptx` (per the `pptx` skill).
3. Split the PDF into one image per page: `pdftoppm -png -r 300 <file>.pdf slide` (produces `slide-1.png`, `slide-2.png`, ... at high resolution).
4. Resize each output image to the exact target pixel dimensions: `convert slide-N.png -resize 1080x1350! slide-N-final.png` (the trailing `!` forces exact dimensions rather than preserving aspect ratio — safe here since the custom layout was already set to the matching ratio, so no distortion occurs).
5. Rename sequentially (`slide-01.png`, `slide-02.png`, ...) and save to `/mnt/user-data/outputs/`.

## Layout variation by slide role

Avoid making every slide the same template with different text — vary layout by the role identified in extraction:

- **Cover/hook**: largest, boldest typography on the slide; minimal supporting text; strongest visual presence of the brand (logo, accent color block, etc.)
- **Point slides**: consistent supporting layout (e.g., number/icon + heading + short body) so the series feels cohesive, but with enough visual rhythm (alternating alignment, accent placement) that it doesn't feel like a single repeated template
- **List/framework slides**: give numbered/bulleted content room to breathe — don't cram a 5-point list into a layout designed for one big idea
- **Proof/stat slides**: make the number or claim the visual focal point, larger than surrounding text
- **CTA/closing**: visually distinct as "the end" (e.g., different background treatment) so it reads clearly as the close of the carousel, not just another point slide

## What NOT to do

- Don't reuse the source's specific graphic treatment (its exact layout grid, iconography, or illustration style) — use the *user's* visual language throughout, informed only by structural lessons (see the SKILL.md note on this).
- Don't skip the resize step — PDF-to-PNG conversion at a given DPI won't land on exact target pixel dimensions by default, and off-size images can get cropped oddly when uploaded to LinkedIn/Instagram.
- Don't vary the brand color palette per slide beyond what the theme specifies — consistency across the carousel is part of what makes it read as a cohesive branded post.
