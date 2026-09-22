# Reply to new real estate leads in minutes with Claude, Follow Up Boss and Twilio — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Twilio.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** A lead email from Zillow or Realtor.com, a website form submission, or a new person appearing in Follow Up Boss or kvCORE starts the run.
2. **Webhooks by Zapier — Custom Request.** GET `https://api.followupboss.com/v1/people?email=…&includeTrash=false` (Follow Up Boss API; add the API key header). Existing record, past conversations, stage, and any notes — so the reply does not treat a past client like a stranger.
3. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Qualify" step of the Speed-to-Lead Automation workflow run by Agentmelt.
   Task: Timeline, pre-approval, price band and intent from the enquiry text; 'hot' only when the timeline is near and something specific is named. Nothing is inferred beyond the text.
   
   Rules:
   - Quiet hours: nothing sent 9 pm–8 am in the lead's time zone; messages queue until morning.
   - One question per message; the second message asks the next question, never both at once.
   - SMS only with a number the lead gave on a form; STOP honoured on the first word and written to the CRM.
   - Fair-housing language check on every draft; flagged drafts cannot be sent.
   - Approval mode for the first week: drafts go to the agent for a tap before sending.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

4. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
5. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
6. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the first reply" step of the Speed-to-Lead Automation workflow run by Agentmelt.
   Task: Two to four sentences in the agent's voice, referencing the property or page, with exactly one question. Fair-housing wordlist applied.
   
   Rules:
   - Quiet hours: nothing sent 9 pm–8 am in the lead's time zone; messages queue until morning.
   - One question per message; the second message asks the next question, never both at once.
   - SMS only with a number the lead gave on a form; STOP honoured on the first word and written to the CRM.
   - Fair-housing language check on every draft; flagged drafts cannot be sent.
   - Approval mode for the first week: drafts go to the agent for a tap before sending.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

7. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
8. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
9. **Code by Zapier (JavaScript) — Check quiet hours and consent.** Holds the message until quiet hours end in the lead's time zone; checks that a phone number came with consent before any SMS; skips leads who opted out. Start from `return { ...inputData };` and add the rule.
10. **Gmail — Send Email — Send the reply.** From the agent's own address, threaded to the lead's email where there is one; SMS as an optional second channel.
11. **Webhooks by Zapier — Custom Request.** POST `https://api.followupboss.com/v1/events` (Follow Up Boss API; add the API key header). Note and stage written to the CRM; hot leads text the agent a three-line summary with the number to call.
12. **Delay by Zapier — Delay For — Follow up on silence.** Two days without a reply: one nudge that offers two showing slots or asks what they are after.

## Guardrails to keep

- Quiet hours: nothing sent 9 pm–8 am in the lead's time zone; messages queue until morning.
- One question per message; the second message asks the next question, never both at once.
- SMS only with a number the lead gave on a form; STOP honoured on the first word and written to the CRM.
- Fair-housing language check on every draft; flagged drafts cannot be sent.
- Approval mode for the first week: drafts go to the agent for a tap before sending.

Full blueprint: https://agentmelt.com/workflows/speed-to-lead-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
