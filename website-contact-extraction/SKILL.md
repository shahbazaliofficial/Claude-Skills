---
name: website-contact-extraction
description: Extract contact details (phone numbers and emails) from a list of websites and deliver the results as a CSV/Excel file. Use whenever the user provides a list of website URLs (pasted, or in an uploaded Excel/CSV file) and wants their contact info pulled — including phrases like "get the contact details from these sites", "find emails/phone numbers for this list of websites", "extract contact info from these URLs", "build a contact list from these domains", or when they upload a spreadsheet of company URLs and ask for phone/email columns added. This is a bulk lead-gen/data-extraction task, not a single-site lookup — expect a list, not one URL, though the same workflow handles a single site fine too.
---

# Website Contact Extraction

Take a list of website URLs and return a spreadsheet with each site's phone number(s) and email(s), pulled from their contact/about pages (or homepage, if that's where the info lives).

## Workflow

### 1. Get the input list

- **Uploaded Excel/CSV**: read it (the `xlsx` skill's approach applies for reading). Find the column containing URLs — if the file has other columns (company name, etc.), keep them and add the new contact columns alongside.
- **Pasted list**: use as given, one URL per line/entry.

Normalize each URL before fetching (add `https://` if missing, strip trailing whitespace). Keep the original URL/domain as given by the user as the row identifier even if you're redirected elsewhere while fetching.

### 2. Find contact info for each site

For each site, in order (stop as soon as you've found solid contact info):

1. **Fetch the homepage directly** (`web_fetch` — this is fine since the URL came from the user's own list). Many sites list a general email/phone right in the header or footer.
2. **Look for `mailto:` and `tel:` links** in the fetched page content — these are the most reliable signal since the site itself marked them as contact methods, not just text that happens to look like an email/phone.
3. **If the homepage doesn't have enough**, find the contact/about page. Prefer discovering its URL via `web_search` (e.g., `"<domain> contact us"`) so the returned URL is fetchable, rather than guessing a path like `/contact-us` directly — `web_fetch` can only open URLs that already appeared in search results or fetched content, so a guessed path may not be fetchable. Then fetch that discovered contact/about page.
4. **If nothing is found after the above**, mark this site as not found (see step 4) rather than continuing to guess further paths.

See `references/finding-contact-info.md` for extraction patterns (email/phone regex considerations, filtering out junk matches like template placeholder emails or tracking-pixel addresses) and for known limitations (JS-rendered sites, obfuscated emails).

### 3. Extract and dedupe

Pull every genuine email and phone number found across the pages checked for that site. Dedupe (the same email/phone often appears in both header and footer). Combine multiple values into one comma-separated string per field, per the user's format preference — do not fabricate or guess at a value that wasn't actually present on the page.

### 4. Handle sites where nothing is found

Keep the row in the output file, with the Emails/Phone Numbers fields left empty for that site — don't drop the row and don't fill it with a placeholder like "Not Found." Still track the count and reasons (no contact info on any page checked / page didn't load / site blocked fetching) and report that in the chat summary, so the user knows how many came back empty and roughly why.

### 5. Build and deliver the output

Build the result as a CSV or Excel file (match whatever the user's input was, or ask if input was pasted text) with the `xlsx` skill's approach. Columns: the original identifying info (URL/domain, plus any columns that were already in an uploaded file), Emails, Phone Numbers. Save to `/mnt/user-data/outputs/` and present it.

## Notes

- This only works on publicly displayed contact information (a site's own contact/about page) — it's the same kind of extraction a person would do manually, just faster; it does not access anything behind a login or paywall.
- For large lists, process steadily and give the user a sense of progress if it's a long list rather than going silent — a brief "working through N sites" is fine.
- If a site is a single-page app or heavily JS-rendered, `web_fetch` may only see a shell of the page with no visible contact info even though a browser would show it — note this as a likely cause when a well-known company's site turns up nothing.
- Never invent or guess an email/phone number (e.g., pattern-guessing `info@domain.com` because that's common) unless it was actually found on a fetched page.
