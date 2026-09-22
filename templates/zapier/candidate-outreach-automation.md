# Send personalized candidate outreach from Greenhouse projects with Claude and Gmail — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Greenhouse / Lever / Ashby, Gmail / Outlook, Google Sheets.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** A candidate added to a sourcing project in the ATS or a row added to the outreach sheet starts a sequence for that person.
2. **Clearbit — Find Person — Research.** Public profile, company page, recent talks or posts, open-source or portfolio work — three to five facts, with sources.
3. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Pick the hook" step of the Candidate Outreach Automation workflow run by Agentmelt.
   Task: One specific, recent, professional thing the candidate did that relates to the role. Not their title, not their employer's tagline.
   
   Rules:
   - Only public, professional information is used; nothing personal, nothing inferred about protected characteristics.
   - Sending limits: 40 new messages a day per mailbox, spaced, so the recruiter's domain reputation is protected.
   - Every message is sent from a person's address and signed by that person; replies go to them.
   - Opt-out language in every message; an opt-out suppresses the candidate across all roles.
   - Follow-ups stop on any reply, including 'not now', which is logged as a future-contact date.
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
   You are the "Draft the message" step of the Candidate Outreach Automation workflow run by Agentmelt.
   Task: Under 90 words: the hook, why the role is relevant to it, one question. Plain text, no tracking pixels, no 'I hope this finds you well'.
   
   Rules:
   - Only public, professional information is used; nothing personal, nothing inferred about protected characteristics.
   - Sending limits: 40 new messages a day per mailbox, spaced, so the recruiter's domain reputation is protected.
   - Every message is sent from a person's address and signed by that person; replies go to them.
   - Opt-out language in every message; an opt-out suppresses the candidate across all roles.
   - Follow-ups stop on any reply, including 'not now', which is logged as a future-contact date.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

7. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
8. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
9. **Gmail — Send Email — Send from the recruiter.** From the recruiter's own address, spaced to stay under daily limits; the ATS gets the message logged against the candidate.
10. **Delay by Zapier — Delay For — Follow up twice.** Day 4 and day 10, each a different angle (the team, the problem, the timing), each shorter than the last.
11. **Gmail — New Email Matching Search (trigger) — Stop on reply.** Any reply ends the sequence and forwards the thread with the research to the recruiter; an out-of-office pauses it.
12. **Google Sheets — Create Spreadsheet Row — Measure.** Per role: sent, replied, positive, interviews — by hook type, so the recruiter learns which angles work for which roles.

## Guardrails to keep

- Only public, professional information is used; nothing personal, nothing inferred about protected characteristics.
- Sending limits: 40 new messages a day per mailbox, spaced, so the recruiter's domain reputation is protected.
- Every message is sent from a person's address and signed by that person; replies go to them.
- Opt-out language in every message; an opt-out suppresses the candidate across all roles.
- Follow-ups stop on any reply, including 'not now', which is logged as a future-contact date.

Full blueprint: https://agentmelt.com/workflows/candidate-outreach-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
