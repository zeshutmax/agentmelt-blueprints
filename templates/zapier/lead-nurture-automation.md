# Nurture real estate leads from Follow Up Boss signals with Claude and Gmail — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Slack.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Schedule by Zapier (trigger).** A new listing in the CRM or MLS feed, a rate change from your lender's feed, an anniversary or birthday in the CRM, or a lead going quiet for N days each start a run for the leads they affect.
2. **Code by Zapier (JavaScript) — Match leads to the signal.** A listing matches a lead when area, price band and beds fit; a rate move matches leads whose budget was near the edge; an anniversary matches one person. Start from `return { ...inputData };` and add the rule.
3. **Code by Zapier (JavaScript) — Check the guardrails.** Skip anyone contacted in the last 14 days, anyone who unsubscribed, anyone with an open conversation, and anyone whose CRM stage is 'active' — the agent is already talking to them. Start from `return { ...inputData };` and add the rule.
4. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the message" step of the Lead Nurture Automation Workflow workflow run by Agentmelt.
   Task: Two to four sentences in the agent's voice that name the reason, reference what the lead said last time, and ask one question. Fair-housing wordlist applied.
   
   Rules:
   - No message without a reason the lead would recognise; the model cannot invent one.
   - Frequency cap: at most one touch per lead per 14 days, at most three per quarter.
   - Anyone in an active conversation or an active CRM stage is excluded automatically.
   - Unsubscribe and STOP are honoured on the first word; suppression is written to the CRM.
   - Fair-housing language check on every draft; flagged drafts cannot be sent.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

5. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
6. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
7. **Slack — Send Channel Message (approval).** Send the summary to your approver with what would be written. Zapier has no wait-for-reply step: with approval mode on, stop the Zap here and re-run the write-back by hand (or from a second Zap triggered by a Slack reaction on the message). With approval mode off, the next step runs immediately.
8. **Filter by Zapier.** Only continue if the stored `approval_mode` is `false`.
9. **Gmail — Send Email — Send and log.** Sent from the agent's own address, threaded where a thread exists; the CRM gets a note and the 'last touched' date.
10. **Gmail — New Email Matching Search (trigger) — Stop on reply.** A reply ends the sequence for that person and forwards the thread to the agent with the lead's history in three lines.
11. **Google Sheets — Create Spreadsheet Row — Report.** Monthly: touches sent by reason, replies, showings and listings that came from a nurture touch, so the agent sees what a reason is worth.

## Guardrails to keep

- No message without a reason the lead would recognise; the model cannot invent one.
- Frequency cap: at most one touch per lead per 14 days, at most three per quarter.
- Anyone in an active conversation or an active CRM stage is excluded automatically.
- Unsubscribe and STOP are honoured on the first word; suppression is written to the CRM.
- Fair-housing language check on every draft; flagged drafts cannot be sent.

Full blueprint: https://agentmelt.com/workflows/lead-nurture-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
