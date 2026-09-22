# Write real estate listing descriptions with Claude from Follow Up Boss — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Follow Up Boss / kvCORE, Mailchimp / Constant Contact, Buffer / Meta API.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** Follow Up Boss, kvCORE, a Google Form, or a change in the MLS feed for the agent's listings starts the run.
2. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Describe the photos" step of the Real Estate Listing Description Automation workflow run by Agentmelt.
   Task: A vision-capable model describes each photo (kitchen with quartz island, west-facing deck, finished basement) so the copy references what buyers will actually see.
   
   Rules:
   - Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit.
   - Facts in the copy are checked against the listing data — no invented square footage or school ratings.
   - The agent approves every asset; nothing publishes automatically.
   - Brokerage disclaimers and MLS-required phrases are inserted, not left to the model.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

3. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
4. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
5. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the MLS description" step of the Real Estate Listing Description Automation workflow run by Agentmelt.
   Task: Within the MLS character limit, in the agent's voice, leading with the strongest feature, with a fair-housing compliance check for protected-class language.
   
   Rules:
   - Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit.
   - Facts in the copy are checked against the listing data — no invented square footage or school ratings.
   - The agent approves every asset; nothing publishes automatically.
   - Brokerage disclaimers and MLS-required phrases are inserted, not left to the model.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

6. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
7. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
8. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the derivatives" step of the Real Estate Listing Description Automation workflow run by Agentmelt.
   Task: Instagram and Facebook captions, a 'just listed' story script, a buyer-list email with the three best photos, and a 60-second virtual-tour narration script.
   
   Rules:
   - Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit.
   - Facts in the copy are checked against the listing data — no invented square footage or school ratings.
   - The agent approves every asset; nothing publishes automatically.
   - Brokerage disclaimers and MLS-required phrases are inserted, not left to the model.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

9. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
10. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
11. **Code by Zapier (JavaScript) — Compliance and brand check.** Fair-housing wordlist, brokerage disclaimer, required MLS phrases, and price/feature consistency against the source data. Start from `return { ...inputData };` and add the rule.
12. **Slack — Send Channel Message (approval).** Send the summary to your approver with what would be written. Zapier has no wait-for-reply step: with approval mode on, stop the Zap here and re-run the write-back by hand (or from a second Zap triggered by a Slack reaction on the message). With approval mode off, the next step runs immediately.
13. **Filter by Zapier.** Only continue if the stored `approval_mode` is `false`.
14. **Facebook Pages — Create Page Post — Publish.** MLS description to the CRM/MLS field, social posts scheduled, the email queued in the ESP to the buyer segment matching price band and area.
15. **Google Sheets — Create Spreadsheet Row — Track.** Every listing's assets, approval time and (from the CRM) showings and days on market, so the brokerage can compare marketed vs unmarketed listings.

## Guardrails to keep

- Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit.
- Facts in the copy are checked against the listing data — no invented square footage or school ratings.
- The agent approves every asset; nothing publishes automatically.
- Brokerage disclaimers and MLS-required phrases are inserted, not left to the model.

Full blueprint: https://agentmelt.com/workflows/listing-description-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
