# Finding & Extracting Contact Info

## Priority order of signals (most to least reliable)

1. `mailto:` and `tel:` links — the site explicitly marked these as contact methods. Extract the address/number directly from the link target.
2. Email/phone patterns in visible text within a footer, header, or a page whose content is clearly about contacting the company (a "Contact Us" heading, an address block, etc.)
3. Email/phone patterns found elsewhere on the page — usable, but more prone to false positives (see below), so sanity-check these before including them.

## Email pattern considerations

- Standard pattern: `[\w.+-]+@[\w-]+\.[a-zA-Z]{2,}` as a starting point, but review matches rather than trusting the regex blindly.
- Filter out obvious junk: template/placeholder addresses (`email@example.com`, `you@domain.com`, `test@test.com`), addresses embedded in tracking/analytics scripts, image filenames that happen to contain an `@` in a data URI, and addresses on clearly third-party embedded content (e.g., a live-chat widget's own support address, not the company's).
- Obfuscated emails (e.g., "info [at] company [dot] com", or emails rendered only via JavaScript/images to block scrapers) generally won't be recoverable from fetched HTML — if a site's footer clearly references contact info but nothing extractable is found, note that as a possible obfuscation case rather than concluding the site has no email.
- Prefer general/business addresses (info@, contact@, hello@, sales@) when many addresses appear on a page — a page full of individual staff emails (e.g., a team directory) is less useful for the typical "get their contact info" ask unless the user specifically wants individual contacts.

## Phone pattern considerations

- Formats vary widely by country — don't assume a single format. Reasonable starting patterns: sequences of 7-15 digits with optional `+`, spaces, dashes, parentheses, and a country code prefix.
- Filter out obvious non-phone-number digit sequences (zip codes standing alone, years, product SKUs, tracking/analytics IDs).
- If a site lists multiple phone numbers for different departments (sales, support, a specific regional office), include all of them per the comma-separated format — don't try to guess which one is "the" main number unless one is clearly labeled as general/main.

## Where contact info commonly lives

- Homepage header (a phone number is common here) and footer (email and phone both common here)
- A dedicated `/contact`, `/contact-us`, or `/about` page
- Sometimes a `/support` or `/get-in-touch` page for SaaS/service companies
- Regional or store-locator pages for companies with multiple locations (only relevant if the user wants location-specific contacts, not the general company contact)

## When to stop looking

Two pages checked (homepage + one contact/about-type page) is usually enough. If a genuine effort at both turns up nothing usable, mark the site as not found rather than continuing to search more pages — diminishing returns on effort don't justify inventing something to fill the row.
