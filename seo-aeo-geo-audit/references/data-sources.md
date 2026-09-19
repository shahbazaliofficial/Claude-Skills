# Data Sources

## Live crawl (`web_fetch`)

Fetch the homepage and a handful of key pages directly. Good for on-page and basic technical checks:

- Title tag, meta description, H1/H2 structure — read straight from the HTML.
- `robots.txt` and `sitemap.xml` — fetch these paths directly to check they exist and aren't blocking important content.
- Structured data — look for `<script type="application/ld+json">` blocks (schema.org markup: Organization, FAQPage, HowTo, Article, Product, etc.).
- Canonical tags, meta robots tags (noindex/nofollow).
- Basic mobile-friendliness signals (viewport meta tag presence).

Limitations: `web_fetch` gets server-rendered HTML — heavily client-side-rendered (JS-framework) sites may not show their real content this way. If the fetched HTML looks sparse relative to what the site visibly shows, note that as a limitation rather than concluding the page has thin content. Can't measure real-world page speed/Core Web Vitals this way — that needs a connector or the user's own data.

## Connector / API

Check for connected SEO/marketing tools. Common ones and what they cover:

- **Ahrefs** (if connected): `site-audit-issues`, `site-audit-page-content`, `site-audit-page-explorer` for technical crawl issues; `site-explorer-organic-keywords`, `site-explorer-top-pages` for on-page/content performance context; `brand-radar-ai-responses`, `brand-radar-citations-overview-entities`, `brand-radar-mentions-overview-entities`, `site-explorer-ai-responses-count` for GEO — actual AI-citation and brand-visibility data.
- **Semrush** (if connected): `site_audit` for technical issues; `organic_research` for keyword/content performance context.
- **Ubersuggest** (if connected): `site_audit`, `site_audit_pages`, `site_audit_results`, `pagespeed_audit` for technical issues including real speed data; `brand_visibility_overview`, `brand_prompts`, `brand_config` for GEO — AI Search Visibility data (how often the brand is surfaced in AI answers, and for which prompts/topics).

If nothing suitable is connected and the user wants this depth (especially for GEO, where live-crawl data can't substitute), use `search_mcp_registry` with keywords like `["SEO", "site audit", "AI search visibility"]`, then `suggest_connectors`.

## Uploaded export

A crawl export (Screaming Frog, Sitebulb, or a connector's own export) — parse like any tabular file. These typically cover technical + on-page fields (status codes, titles, meta, word count, etc.) at full-site scale, which is more thorough than a live-crawl sample — prefer this when available for the technical/on-page pillars. They generally don't include GEO/AI-citation data, which still needs a connector or is simply unavailable.

## Combining sources without duplicating work

- Technical SEO: prefer an uploaded crawl export or connector site-audit tool if available (full-site coverage); fall back to a live-crawl sample of key pages otherwise.
- On-page/Content SEO: same as above — export/connector for scale, live crawl for spot-checks or when nothing else is available.
- AEO: mostly assessed from the content itself (live crawl or export) — structure, schema, answer-formatting — this pillar rarely needs a connector.
- GEO: connector data (Ahrefs brand-radar / Ubersuggest brand-visibility) is the only source for actual citation/visibility numbers. Without a connector, GEO findings are readiness signals only (inferred from content structure) — say so explicitly rather than implying visibility was measured.
