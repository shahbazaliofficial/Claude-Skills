# Audit Framework

## Pillar checklists

### Technical SEO
- Indexability: robots.txt not blocking important paths, no accidental sitewide `noindex`, sitemap.xml present and matches actual site structure
- HTTPS everywhere, no mixed-content issues
- Site speed / Core Web Vitals (LCP, INP, CLS) where measurable
- Mobile-friendliness (viewport tag, responsive layout)
- Canonical tags set correctly (no conflicting or missing canonicals on key pages)
- Broken links (4xx) and redirect chains/loops
- Duplicate content (multiple URLs serving near-identical content without canonicalization)
- Structured data validity (schema present and error-free, not just present)

### On-page / Content SEO
- Title tags: unique per page, reasonable length, include the page's target topic without stuffing
- Meta descriptions: present, unique, compelling (they don't affect ranking but affect CTR)
- Header hierarchy: one H1 per page, logical H2/H3 nesting (not skipped or purely decorative)
- Keyword targeting: does the page's content actually address the topic it's trying to rank for, without obvious over-optimization
- Internal linking: important pages reachable within a few clicks, relevant contextual links between related content
- Content depth/quality: does the page substantively answer what someone searching that topic would want, or is it thin
- Image alt text: present and descriptive on meaningful images (not just present for present's sake)

### AEO (Answer Engine Optimization)
- Direct-answer formatting: key questions answered in a clear, extractable sentence or two near the top of relevant content, not buried in prose
- FAQ sections with matching FAQPage schema where genuinely applicable (don't recommend FAQ schema on pages without real FAQ content)
- HowTo schema on genuinely step-by-step content
- Clear, scannable structure (lists, tables, short paragraphs) that a snippet/answer-box algorithm can lift cleanly
- Definitional clarity: if the page is the kind of resource that should define a term or concept, does it do so plainly

### GEO (Generative Engine Optimization)
- Confirmed visibility data (if a connector provides it): is the brand/site cited in AI-generated answers, for which prompts/topics, and how does that compare to competitors
- Readiness signals (assessable from content alone, if no citation data is available):
  - Clear, factual, well-sourced statements an LLM could confidently extract and attribute
  - Structured data that helps machines understand entities (Organization, Product, Article schema with author/date)
  - Authoritative signals: author bylines, publish/update dates, citations of sources
  - Content that answers a question comprehensively in one place, rather than requiring the reader to piece it together across pages

Keep "confirmed visibility data" and "inferred readiness signals" visually and textually separate in the output — they're different confidence levels.

## Prioritization

Score each finding on two axes and present findings sorted by this, not just by pillar order:

- **Severity**: Critical (actively harming visibility — e.g., accidental noindex, broken canonical) / High (meaningfully limiting performance) / Medium (worth fixing, not urgent) / Low (minor polish)
- **Effort**: Quick win (small technical/content fix) / Larger effort (content overhaul, schema implementation across many pages, site restructuring)

Lead the findings/recommendations with **Critical + Quick win** and **High + Quick win** items — these are the highest-leverage fixes. Larger-effort items still get listed, just framed as longer-term roadmap items rather than immediate to-dos.
