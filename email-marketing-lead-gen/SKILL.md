---
name: email-marketing-lead-gen
description: Search for businesses matching given criteria (search term, industry, category, location), extract their contact details (phone, email, and lightly-sourced executive contacts) from the web, prepare the data for import into Brevo (already connected), and create/send Brevo email campaigns to the collected leads in batches of up to 320. Use this whenever the user wants to build a prospect list for email marketing — "find me [industry] businesses in [location]", "get leads for a Meta Ads campaign", "build an email list for [category]", or "send a campaign to the leads we found". Always confirm search criteria before searching, always ask which email template to use before creating any campaign, and always get explicit confirmation before scheduling/sending a campaign since that sends real email to real people.
---

# Email Marketing Lead Gen (Search → Extract → Brevo Campaign)

Find businesses matching the user's criteria, extract their contact details, package the results for Brevo import (no direct contact-write tool is available — see the Brevo gap note below), and create/send Brevo email campaigns to the collected leads in batches.

## Workflow

### 1. Get search criteria

Ask for (or confirm from context) whatever's missing: search term, industry, category, location, and any additional instructions. Don't proceed to searching with vague or missing criteria — a well-scoped search saves a lot of wasted extraction effort later.

### 2. Search for matching businesses

Use both, per the confirmed approach:
- **Google Maps** (`places_search`) — best for local/physical businesses matching the industry/category/location.
- **Google Search** (`web_search`) — fallback or complement for online-only businesses, or to fill gaps Maps doesn't cover well.

Combine and dedupe results across both sources before moving to extraction.

### 3. Extract contact details per business

For each business, visit its website/contact page and extract phone number(s) and email(s), plus a lightweight pass for named executive contacts. See `references/search-and-extraction.md` for the extraction priority order, executive-search approach, and what to do when nothing is found (leave fields empty — never fabricate a phone number, email, or guessed executive address).

### 4. Package the data for Brevo

Brevo columns: **Name (if found), Organization name, Contact No., Email, Website, Industry, Country**. Leave any field blank that wasn't actually found — never fill gaps with guesses or placeholders.

**Known gap**: no connected Brevo tool can create or import contacts directly. Deliver the results as a CSV formatted for Brevo's own Import feature, split into files of up to 320 contacts each (batch size matches the sending batch size). See `references/brevo-csv-format.md` for column-header alignment (check existing Brevo custom attributes first so headers match what's already in the account) and file-naming/batching conventions. The user imports each CSV into a new Brevo list themselves.

### 5. Create and send the campaign (only when asked to "start")

This step only runs when the user explicitly asks to start/send a batch — steps 1-4 (search, extract, package) don't imply this step.

1. Confirm which Brevo list this batch was imported into (ask, or check `lists_get_lists` for a recently created list matching the batch).
2. **Always ask which template to use** — list available templates (`templates_get_smtp_templates`) and have the user pick, every single time, even if they picked one recently. Never silently reuse the last template.
3. Confirm the campaign name's "Service name" component (the user said they'll specify this each time) and build the name as `<Service name> - <dd/mm/yyyy>` (today's date).
4. Confirm subject line, sender, and the target list/recipient count with the user before creating anything.
5. Create the campaign via `email_campaign_management_create_email_campaign` targeting that list. See `references/campaign-creation.md` for how sending actually works (there's no dedicated "send now" tool — sending happens via `scheduledAt`) and the confirmation this requires every time, since it dispatches real email to real people.

## Notes

- This only extracts publicly displayed contact information, same as any manual prospecting research — nothing behind a login or paywall.
- If a search returns very few or no matching businesses, say so rather than padding the list with loosely-related results.
- For large batches, work steadily and give the user a sense of progress rather than going silent on a long-running extraction.
- If Brevo gains a contact-import tool in the future, this skill's step 4 should switch to using it directly instead of the CSV handoff — check the Brevo tool list at the start of a session if this comes up.
