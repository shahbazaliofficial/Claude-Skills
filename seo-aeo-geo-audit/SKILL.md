---
name: seo-aeo-geo-audit
description: Audit a website's SEO (traditional search), AEO (Answer Engine Optimization — snippets, answer boxes), and GEO (Generative Engine Optimization — visibility/citation in ChatGPT, Perplexity, Google AI Overviews) health, and deliver either a drill-down dashboard artifact or a client-presentable report. Use whenever the user wants a site's search or AI-visibility health reviewed — "audit my site's SEO", "SEO audit", "AEO audit", "GEO audit", "how visible are we in AI search/ChatGPT/Perplexity", "are we being cited by AI", "site audit", "technical SEO review", "on-page SEO check", "is our content optimized for AI search" — or when given a URL for a health check, a crawl export, or an ask to connect an SEO tool. Trigger even for just "SEO" or just "AI search visibility" — cover the relevant pillar(s), asking only if genuinely unclear. Different from meta-ads-account-analysis/google-search-console-analysis (traffic performance) — this is a site health/readiness audit, not a performance report.
---

# SEO / AEO / GEO Website Audit

Audit a website across three pillars — traditional SEO, AEO (answer-engine readiness), and GEO (generative/AI-engine visibility) — and deliver either a drill-down dashboard artifact or a client-presentable report, depending on the use case.

## Workflow

### 1. Get the site and scope

Ask for (or confirm from context): the site URL, and whether this covers the whole site or specific pages/sections. Confirm which pillar(s) matter if the user's ask is narrow (e.g., "check our AI visibility" is GEO-only — don't run a full technical crawl unless asked). Default to all three if the request is general ("audit our SEO", "how's our site doing").

### 2. Gather data — combine sources as needed

- **Live crawl**: Use `web_fetch` on the homepage and a sample of key pages (main nav pages, top-traffic pages if known) to check on-page elements directly — titles, meta descriptions, headers, schema markup, robots.txt, sitemap.xml. This works for most sites but won't fully render heavy client-side JS — note that limitation if the site appears JS-rendered.
- **Connector/API**: Check for connected SEO tools (Ahrefs, Semrush, Ubersuggest are common). These cover technical site-audit crawls, keyword rankings, backlinks, and — importantly for GEO — AI citation/brand-visibility data that a live crawl can't get (e.g., Ahrefs' `brand-radar-*` and `site-explorer-ai-responses-count`, Ubersuggest's `brand_visibility_overview`/`brand_prompts`, and Ahrefs/Semrush/Ubersuggest `site_audit`/`site-audit-*`/`pagespeed_audit` for technical issues). If nothing suitable is connected and the user wants this depth, use `search_mcp_registry` + `suggest_connectors`.
- **Uploaded export**: A crawl export (e.g., Screaming Frog, or an export from a connected tool) — parse like any tabular file.

See `references/data-sources.md` for which tools cover which pillar and how to combine them without duplicating work.

### 3. Run the audit across three pillars

See `references/audit-framework.md` for the full checklist per pillar and a severity/effort framework for prioritizing findings. In brief:

- **Technical SEO** — crawlability & indexability (robots.txt, sitemap, canonical tags), site speed/Core Web Vitals, mobile-friendliness, HTTPS, structured data presence, broken links/redirects, duplicate content.
- **On-page/Content SEO** — title tags, meta descriptions, header structure (H1/H2 hierarchy), keyword targeting, internal linking, content depth, image alt text.
- **AEO (answer-engine readiness)** — content structured to directly answer questions (clear definitions, FAQ sections, concise answer-first paragraphs), FAQ/HowTo schema markup, featured-snippet-worthy formatting.
- **GEO (generative/AI-engine visibility)** — actual citation/visibility data where available (does the brand get cited in AI-generated answers, and for what), plus readiness signals (clear factual statements, structured data, authoritative sourcing, content that's easy for an LLM to extract and attribute) even where citation data itself isn't available.

Don't blend the three pillars into one score — they're different audiences (search crawlers, answer-box algorithms, LLMs) and a site can be strong in one and weak in another; keep findings organized by pillar.

Prioritize findings by severity (Critical/High/Medium/Low) and effort (quick win vs. long-term fix) — see the framework doc — rather than presenting an undifferentiated list of issues.

### 4. Choose the output format

Ask which format fits the use case (or infer from context — e.g., "for the client" implies a report):

- **Dashboard artifact** — a single-file HTML dashboard, drill-down structure (site overview → pillar breakdown → page-level detail), following the same pattern as `meta-ads-account-analysis`/`google-analytics-account-analysis`/`google-search-console-analysis`. See `references/output-formats.md`.
- **Client-presentable report** — a designed slide deck exported to PDF, following the same pattern as `meta-ads-proposal` (build via the `pptx` skill, export via `soffice.py --convert-to pdf`, deliver both PDF and editable `.pptx`). See `references/output-formats.md`.

### 5. Summarize in chat

Regardless of output format, give a short prose summary: overall health per pillar, and the top 3-5 priority actions (favor quick wins that unblock bigger wins). Don't restate every finding in text — the artifact/report is the detail.

## Notes

- If the site is large, audit a representative sample of pages (homepage, main templates/page types, top pages) rather than attempting exhaustive page-by-page coverage, and say what was and wasn't covered.
- GEO is a newer, less standardized field than SEO — be honest that AI-citation data is often partial or unavailable, and separate "confirmed visibility data" from "readiness signals we're inferring" in the findings.
- Never fabricate ranking positions, citation counts, or Core Web Vitals scores — if a metric wasn't available from any source, say so rather than estimating it silently.
