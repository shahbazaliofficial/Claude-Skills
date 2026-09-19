# Brevo CSV Format & Batching

## Why a CSV handoff

No connected Brevo tool can create or import contacts (the available tools only read contacts/lists, manage templates, and create campaigns). Brevo's own Import feature (Contacts → Import) accepts a CSV and lets the user map columns to attributes during upload, so that's the delivery mechanism until/unless a contact-write tool becomes available.

## Columns

Fixed set, per the user's spec: **Name (if found), Organization name, Contact No., Email, Website, Industry, Country**.

- `Email` is the field Brevo uses as the unique contact identifier during import — every row should have one where possible (a row with no email at all is still deliverable as data, but won't be importable as a Brevo contact for email campaigns, so consider flagging email-less rows separately rather than mixing them into a batch meant for immediate import).
- Leave any other field blank if not found — no placeholder text.

## Matching existing Brevo attributes

Before finalizing headers, call `attributes_get_attributes` to see what custom contact attributes already exist in the account. If equivalents already exist (e.g., an existing `ORGANIZATION`, `PHONE`, `WEBSITE`, `INDUSTRY`, or `COUNTRY` attribute), name the CSV columns to match those exactly (Brevo attribute names are typically uppercase, no spaces) so the user's import mapping is a clean match rather than requiring them to create new attributes or manually remap. If no equivalent exists for a field, use a sensible uppercase attribute-style name (e.g., `ORGANIZATION`, `PHONE`, `WEBSITE`, `INDUSTRY`, `COUNTRY`) and note in the summary that these will need to be created (or mapped) during import — Brevo's import flow allows creating new attributes on the fly.

## Batching

Split results into files of **up to 320 contacts each** — this matches the sending batch size, since each batch becomes its own Brevo list that a campaign will later target.

File naming: something identifiable by search criteria and batch number, e.g. `leads-<search-term-or-industry>-<location>-batch1.csv`, `...batch2.csv`, etc. Keep the same base name across batches from the same search so they're easy to tell apart from other searches.

## Delivering

Save each batch CSV to `/mnt/user-data/outputs/` and present them. In the chat summary, state: total businesses found, how many had a usable email (importable), how many were missing contact info entirely (and were therefore left out or flagged), and how many batches were produced.
