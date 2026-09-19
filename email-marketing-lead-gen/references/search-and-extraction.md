# Search & Extraction

## Searching

- `places_search` (Google Maps): build queries from the criteria, e.g. "accounting firms in Dubai" or combining category + location directly. Use `location_bias_lat`/`location_bias_lng` if the location is a specific city/area and results need tightening. Pull enough results to cover the ask, running multiple queries for broad categories rather than relying on one query's default result count.
- `web_search`: use for online-only businesses, or categories Maps doesn't index well (e.g. purely digital services, niche B2B). Also useful as a fallback when Maps returns thin results for a category.
- Dedupe across both sources by domain/business name before extraction — the same business often surfaces from both.

## Contact extraction (per business)

Same priority order as general contact extraction:
1. `mailto:`/`tel:` links on the homepage or contact page — most reliable.
2. Footer/header text and a dedicated contact/about page (discover its URL via `web_search` if not linked directly from the homepage, since `web_fetch` needs a URL that already appeared in search/fetch results).
3. General page text as a last resort — sanity-check matches (filter template placeholders, tracking-script addresses, non-phone digit sequences).

Two fetches (homepage + one contact/about page) is usually enough per business. Move on rather than exhaustively crawling a site that isn't giving up contact info.

## Executive contact search (keep lightweight)

The goal is a named person's email if it's genuinely available — not a research project per business:
- Check the site's Team/About/Leadership page if one is linked from the homepage (already covered by the contact-page fetch in most cases).
- One `web_search` for something like `"<company> founder"` or `"<company> CEO"` if the site itself didn't surface a name — only if this is quick; don't chain multiple searches per business.
- Only include an executive's email if it was actually found stated somewhere (on the site, in a search snippet, etc.). **Never guess or construct an executive's email from a pattern** (e.g., inferring `john@company.com` because other emails at that domain follow `firstname@company.com`) — an inferred address is not a found one, and sending to a guessed address is exactly the kind of thing that damages deliverability and reputation.
- If no named executive turns up quickly, leave the Name field blank and move on — the general contact email/phone is still useful data.

## When nothing is found

Leave the relevant field(s) blank in the output. Don't skip the business entirely just because the executive-name search came up empty — a business with only a general email/phone is still a usable row.
