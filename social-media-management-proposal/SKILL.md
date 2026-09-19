---
name: social-media-management-proposal
description: Build a polished, client-facing Social Media Management proposal — a multi-page visual PDF (built as a designed slide deck) covering platform strategy, content strategy, deliverables/scope, pricing, timeline, and expected results. Use whenever the user wants to pitch, propose, or present a social media management plan to a client or prospect — "make a social media proposal for [client]", "pitch deck for social media management", "SMM proposal", "content strategy proposal", "client presentation for social media services", or turning a social media plan/pricing into something presentable or client-ready. Scope varies widely by client (organic-only, paid-only, full-service, specific platforms) — always run the client interview first, including scope of service, and never assume details or section structure. Broader/adjacent to meta-ads-proposal (Meta-ads-specific); use this one when the ask covers social media management generally or spans multiple platforms/services.
---

# Social Media Management Client Proposal

Turn a client's social media management needs into a polished, multi-page, client-presentable deliverable — built as a designed slide deck and delivered as PDF (plus the editable source).

This is content generation for a specific client pitch, not data analysis. Every proposal is different — always interview first, including what "social media management" even means for this client (scope varies enormously: some want organic content only, some want full-service including paid social and influencer work).

## Workflow

### 1. Interview the user

Never assume scope, platforms, or structure — ask what's missing (don't re-ask what the user already gave you). At minimum you need:

- **Client & context**: client/brand name, industry, and their current situation (why they're looking at social media management now — no presence, inconsistent posting, wrong platforms, need to scale, etc.)
- **Scope of service**: what's actually included — organic content/posting, community management, paid social, influencer/creator partnerships, analytics/reporting, or some combination. This changes almost every downstream section, so confirm it explicitly.
- **Platforms**: which platforms (Instagram, TikTok, LinkedIn, Facebook, X, YouTube, Pinterest, etc.) — client preference, or does Claude need to recommend based on the objective/audience/industry?
- **Objectives**: brand awareness, community growth, engagement, lead gen, driving sales, etc.
- **Budget & pricing model**: retainer, package tiers, or project-based — and the number(s) to work with.
- **Timeline**: contract length, launch date if known.
- **Branding**: brand colors, logo, or existing deck/template to match.
- **Section structure**: confirm which sections to include — see the default flow below, but treat it as a starting point the user can add to, cut, or reorder, and ask rather than assume when it's not obvious from context.

See `references/interview-and-content.md` for the full question set and guidance on generating the Platform Strategy, Content Strategy, and Projections sections from what the user gives you.

Don't proceed to building until you have at least client context, scope of service, and objectives — those shape almost everything else.

### 2. Draft the content outline first

Before building slides, write out the section-by-section content (headlines + key points per section) and confirm it with the user, or proceed directly if they've clearly said "just build it." This catches misunderstandings before time is spent on visual design.

Default section flow (confirm with the user each time — scope and structure both vary by client):

1. Cover / Intro
2. Client Situation / Challenge
3. Objectives
4. Platform Strategy (which platforms, and why)
5. Content Strategy / Pillars
6. Posting Cadence & Sample Calendar
7. Deliverables & Scope (be explicit about what's included/excluded — this prevents scope-creep disputes later)
8. Pricing Packages / Tiers
9. Timeline
10. Expected Results
11. Next Steps / CTA

Adjust freely per client — e.g., a paid-social-inclusive proposal needs a budget/channel breakdown slide (can mirror the approach in `meta-ads-proposal`); an organic-only proposal doesn't.

### 3. Build the deck

Use the `pptx` skill to build this as an actual PowerPoint deck (via `pptxgenjs`) — that's the right tool for a designed, multi-slide visual document, and it gives the client an editable file too. Read the `pptx` skill's guidance before building, especially the pptxgenjs gotchas.

Design notes specific to this proposal type:
- Vary layouts per section — don't put every section on a title+bullets slide. A content calendar/cadence section benefits from a visual weekly-grid layout; a pricing section benefits from a tiered-package comparison layout, not a plain table.
- Apply the client's brand colors if given (read `frontend-design` for general visual polish if no brand style is given).
- Keep slide count driven by content, not a fixed number — each slide should earn its place.
- Deliverables & Scope and Pricing Packages are the slides clients scrutinize most for what's actually included — be precise and unambiguous here, not just visually polished.

### 4. Export to PDF and deliver

Convert the finished deck to PDF with `scripts/office/soffice.py --headless --convert-to pdf` (from the pptx skill) since the deliverable is a presentable PDF. Save both the `.pdf` (primary, for viewing/sending to the client) and the `.pptx` (editable source) to `/mnt/user-data/outputs/` and present both — lead with the PDF.

## Notes

- If the user later asks to revise ("change the pricing tiers", "add TikTok", "swap the case study slide"), edit the existing deck (per the `pptx` skill's edit workflow) rather than rebuilding from scratch, then re-export to PDF.
- Never present projected results (follower growth, engagement rate, reach estimates) as guarantees — frame them clearly as estimates, and say so explicitly in the deck itself (a small disclaimer line), not just in chat.
- If the proposal includes a paid social component, the budget/projections approach from `meta-ads-proposal` applies to that portion — reuse that logic rather than reinventing it.
- If the user hasn't given brand colors/logo, ask once if they have brand assets to match; if not, proceed with a clean, professional default look rather than blocking on it.
