---
name: meta-ads-proposal
description: Build a polished, client-facing Meta Ads (Facebook/Instagram) proposal deliverable — a multi-page visual PDF (built as a designed slide deck) covering strategy, audience, budget, timeline, and projected results. Use this whenever the user wants to pitch, propose, or present a Meta/Facebook/Instagram ads plan to a client or prospect — including phrases like "make a proposal for [client]", "pitch deck for meta ads", "client presentation for our ads plan", "proposal for a Facebook ads campaign", or requests to turn a strategy/budget into something presentable, professional, or client-ready. This is a different job from analyzing an existing account's performance (see the meta-ads-account-analysis skill for that) — this skill is for proposing new or planned work, before or instead of running it. Always run the client interview first; never generate a proposal from assumed details.
---

# Meta Ads Client Proposal

Turn a strategy/budget/plan into a polished, multi-page, client-presentable deliverable — built as a designed slide deck and delivered as PDF (plus the editable source).

This is content generation for a specific client pitch, not data analysis. Every proposal is different — always interview first.

## Workflow

### 1. Interview the user

Content varies per client — never assume. Ask what's missing (don't re-ask what the user already gave you in this message). At minimum you need:

- **Client & context**: client/brand name, industry, and their current situation or challenge (why they need this campaign).
- **Objectives**: what the campaign is meant to achieve (awareness, leads, sales, app installs, etc.) — this determines which metrics matter in the Projections section.
- **Budget**: total or monthly budget, and campaign duration/timeline if known.
- **Target audience**: who they're trying to reach, if the user has a point of view — otherwise Claude can propose one based on the objective/industry and flag it as a recommendation to validate with the client.
- **Branding**: any brand colors, logo, or existing deck/template to match — a proposal that doesn't look like it belongs to the client's brand reads as generic.
- **Optional sections**: whether to include a "Why Us" / agency credibility section (off by default — only include it if the user asks or supplies the content for it).

See `references/interview-and-content.md` for the full question set and guidance on generating the Strategy, Audience, and Projections sections from what the user gives you.

Don't proceed to building until you have at least client context, objective, and budget — those three shape almost everything else.

### 2. Draft the content outline first

Before building slides, write out the section-by-section content (headlines + key points per section) and confirm it with the user, or proceed directly if they've clearly said "just build it." This catches misunderstandings before time is spent on visual design.

Default section flow (adjust per client — this is a starting point, not a rigid template):

1. Cover / Intro
2. Client Situation / Challenge
3. Objectives
4. Proposed Strategy
5. Target Audience
6. Budget & Channel Breakdown
7. Timeline / Phasing
8. Expected Results / Projections
9. Next Steps / Investment & CTA

("Why Us" / agency credibility slides go between Projections and Next Steps if included.)

### 3. Build the deck

Use the `pptx` skill to build this as an actual PowerPoint deck (via `pptxgenjs`) — that's the right tool for a designed, multi-slide visual document, and it gives the client an editable file too. Read the `pptx` skill's guidance before building, especially the pptxgenjs gotchas.

Design notes specific to a client proposal:
- This needs to look like a real agency pitch deck, not a bullet-point report — vary layouts per section (don't put every section on a title+bullets slide), use real charts for budget/channel breakdown and projections, and apply the client's brand colors if given (read `frontend-design` for general visual polish if no brand style is given).
- Keep slide count driven by content, not a fixed number — "as many as needed to show the solution well," per section above, but each slide should earn its place (don't pad).
- Budget & Channel Breakdown and Expected Results are the slides clients scrutinize most — give them real charts (pie/bar for channel split, bar/line for projections), not just a table of numbers.

### 4. Export to PDF and deliver

Convert the finished deck to PDF with `scripts/office/soffice.py --headless --convert-to pdf` (from the pptx skill) since the deliverable is a presentable PDF. Save both the `.pdf` (primary, for viewing/sending to the client) and the `.pptx` (editable source, in case the user wants to tweak it) to `/mnt/user-data/outputs/` and present both — lead with the PDF.

## Notes

- If the user later asks to revise ("change the budget to $10k", "add a case study slide"), edit the existing deck (per the `pptx` skill's edit workflow) rather than rebuilding from scratch, then re-export to PDF.
- Never present projected results (reach, CPA, ROAS estimates) as guarantees — frame them clearly as estimates based on the stated budget/industry, and say so explicitly in the deck itself (a small disclaimer line), not just in chat.
- If the user hasn't given brand colors/logo, ask once if they have brand assets to match; if not, proceed with a clean, professional default look rather than blocking on it.
