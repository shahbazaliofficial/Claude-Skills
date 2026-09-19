---
name: carousel-remix
description: Take a LinkedIn or Instagram carousel from another creator, rewrite its content into something noticeably better (same structure/flow, same slide count, genuinely original wording), and design it into a fresh set of slide images using the user's own brand/design theme. Use this whenever the user shares a carousel (as screenshots, pasted text, or a link) and wants it "remixed", "rewritten", "recreated with my branding", turned into their own carousel post, or asks to redesign someone else's post/slides in their own style. Output is a ready-to-upload set of individual slide images sized for the target platform. Always confirm platform (LinkedIn vs. Instagram) and the design theme (fixed base theme vs. a tweak for this post) before building.
---

# Carousel Remix

Turn someone else's carousel into the user's own: same slide count and structural flow, meaningfully better writing, and a fresh visual design in the user's branding — delivered as individual slide images ready to upload.

This is a content + design remix, not a copy. The rewritten content must be genuinely original — see the copyright note below, which matters more here than in most tasks since the output is published as the user's own work.

## Workflow

### 1. Get the source carousel

Accept whichever form the user provides:
- **Screenshots/images**: read them directly (they're visible in context once uploaded). If text is cut off, small, or ambiguous, say what's unclear rather than guessing.
- **Pasted text**: use as-is.
- **A link**: try `web_fetch`. LinkedIn/Instagram posts are frequently behind a login wall and won't fetch — if that happens, ask the user to paste the text or share screenshots instead rather than retrying the link repeatedly.

### 2. Extract structure, not wording

Read through the source and identify, per slide: its role in the narrative (hook/cover, context or problem statement, individual points, a stat or proof slide, list items, CTA/closing, etc.) and the core idea it's conveying — not its exact sentences. See `references/content-extraction.md` for how to break this down cleanly and why this step matters for originality.

Confirm the slide count from the source — the output must match it exactly.

### 3. Confirm platform and design theme before building

Ask (don't assume) if not already given in this message:
- **Platform**: LinkedIn or Instagram — this sets the target image dimensions (see `references/design-and-export.md`).
- **Design theme**: does this post use the standard/base theme, or are there tweaks for this one (different accent color, different topic-specific imagery, etc.)? If no base theme has been established yet in this conversation, ask for the essentials: brand colors (hex if available), font preference, logo (if they want it on slides), and general style (bold/minimal/playful/corporate).

### 4. Rewrite the content

Write fresh copy for each slide that follows the same structural role and flow as the source but is a genuine improvement — stronger hook, clearer point, more persuasive phrasing — and is not a close paraphrase of the original. See `references/rewriting-guidelines.md` for what "noticeably better" means in practice and how to keep it original rather than a thin reword.

Share the rewritten copy with the user before or alongside building the visuals if there's any doubt about tone/direction — cheap to fix text, more effort to redo finished slide designs.

### 5. Design and build the slides

Build the carousel as a slide deck sized to the target platform's dimensions, applying the confirmed brand theme, then export each slide as a standalone image. See `references/design-and-export.md` for the exact build/export pipeline (custom-dimension deck → PDF → per-slide PNGs → resize to exact target pixels) and for varying layout by slide role so it doesn't look like the same template repeated N times.

### 6. Deliver

Save the numbered slide images (e.g., `slide-01.png`, `slide-02.png`, ...) to `/mnt/user-data/outputs/` and present them in order. Default deliverable is the image set, as that's what's needed to post — mention that the editable source deck exists if the user wants to tweak something themselves, but don't present it as the primary deliverable unless asked.

## Copyright & originality note

The source carousel is someone else's work — the goal is inspiration from structure and topic, not reproduction. Never carry over the original's specific sentences or close paraphrases of them (same phrasing/sentence structure with a few words swapped is still reproduction, not a rewrite). The rewritten content should be something the user could confidently call their own original take on the topic. If a source slide is mostly a specific quote, statistic, or claim attributed to someone, keep the underlying fact but express it in fully original wording, and don't present someone else's specific framework/proprietary methodology as the user's own without attribution if it's clearly branded as theirs (e.g., a named 5-step system with a distinctive name).

## Notes

- If the user wants to reuse a previously-established theme across multiple carousels, keep it consistent rather than re-deriving it each time — but still confirm per-post whether this one needs a tweak, since they said theme may vary post to post.
- If slide count is high (10+), keep per-slide text tight — carousel slides are skimmed, not read like an article; each slide should carry one clear idea.
- If the source's visual style is doing something structurally smart (e.g., a strong numbered-list format, a clear before/after layout), that structural pattern can inform the design — just execute it in the user's own visual language (colors/fonts/logo), not a visual copy of the original's specific graphic treatment.
