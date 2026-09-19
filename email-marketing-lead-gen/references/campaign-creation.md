# Campaign Creation & Sending

## No "send now" tool — sending works via scheduling

`email_campaign_management_create_email_campaign` creates a campaign in **draft status by default**. There is no separate send-now tool in the connected Brevo toolset. The way to actually dispatch a campaign is to set `scheduledAt` to a near-immediate UTC timestamp (e.g., a few minutes from the moment of creation) — Brevo will send it automatically at that time without further action.

This means "send now" is really "schedule for right now" — treat it with the same weight as an immediate send, because it is one. Never set `scheduledAt` without the user's explicit go-ahead in that specific message (not a general standing instruction from earlier in the conversation) — this dispatches real email to every contact in the target list.

## Before creating any campaign (every time)

1. **Template — always ask fresh.** Call `templates_get_smtp_templates`, show the available options (name/subject/id), and have the user pick. Even if they used a template last time, ask again — never silently default to the previous choice.
2. **Confirm the target list and recipient count.** Use `lists_get_lists` (and `lists_get_list` for a specific list's contact count) to confirm which list this batch corresponds to and how many contacts are in it — surface the count to the user before proceeding.
3. **Confirm subject line and sender.** If the user hasn't specified a subject, ask — don't invent marketing copy unprompted for something about to be sent to real prospects. Confirm sender via `senders_get_senders` if not already established.
4. **Confirm the campaign name.** Format: `<Service name> - <dd/mm/yyyy>`, using today's date. The user specified they'll give the "Service name" each time — ask if it wasn't given with this request.

## Creating the campaign

Call `email_campaign_management_create_email_campaign` with:
- `name`: the confirmed `<Service name> - <dd/mm/yyyy>` string
- `sender`: confirmed sender
- `subject`: confirmed subject
- `templateId`: the chosen template's ID
- `recipients`: the target list ID
- `scheduledAt`: only set once the user has explicitly confirmed they want this batch sent now — omit it to leave the campaign as a draft in Brevo for the user to review/send manually instead, if that's what they'd prefer for a given batch.

## After creating

Report back the campaign name, target list, recipient count, template used, and whether it was scheduled to send or left as a draft. If scheduled, state the send time clearly (convert to a timezone the user will recognize, not just raw UTC) so there's no ambiguity about when real emails go out.
