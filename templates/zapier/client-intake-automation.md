# Intake new client enquiries from Gmail with Claude into Clio and DocuSign — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Clio / PracticePanther, Gmail / Outlook, DocuSign / PandaDoc.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Gmail — New Email Matching Search (trigger).** An email to the intake address, a website form submission, or a phone note typed into the shared inbox starts intake for that enquiry.
2. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Classify the matter" step of the Client Intake Automation Workflow workflow run by Agentmelt.
   Task: Matter type from the firm's own taxonomy (employment, commercial, family, conveyancing…), urgency, and whether it is within the firm's practice at all.
   
   Rules:
   - Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically.
   - Conflict results are shown with their evidence; a hit blocks the engagement letter until a person clears it.
   - Enquiry content is processed through an API with no data retention and stored only in the firm's own systems.
   - Out-of-scope or conflicted matters get a courteous decline drafted for approval, never an automatic one.
   - Every intake keeps an audit line: received, classified, checked, approved by whom, when.
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
   You are the "Extract the conflict-check facts" step of the Client Intake Automation Workflow workflow run by Agentmelt.
   Task: Names of parties and related entities, addresses, dates, the other side's counsel if named — structured, with the source sentence for each.
   
   Rules:
   - Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically.
   - Conflict results are shown with their evidence; a hit blocks the engagement letter until a person clears it.
   - Enquiry content is processed through an API with no data retention and stored only in the firm's own systems.
   - Out-of-scope or conflicted matters get a courteous decline drafted for approval, never an automatic one.
   - Every intake keeps an audit line: received, classified, checked, approved by whom, when.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

6. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
7. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
8. **Code by Zapier (JavaScript) — Run the conflict check.** Parties checked against the client list, former-client list and adverse-party list in the matter system, with fuzzy matching on names and companies; hits are listed with the matter they came from. Start from `return { ...inputData };` and add the rule.
9. **Gmail — Send Email — Acknowledge.** A same-day acknowledgement to the enquirer from the firm's address: received, who will respond, by when.
10. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the next document" step of the Client Intake Automation Workflow workflow run by Agentmelt.
   Task: Engagement letter from the firm's template for that matter type with fees from the schedule, or a decline where the matter is out of scope or conflicted — variables highlighted.
   
   Rules:
   - Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically.
   - Conflict results are shown with their evidence; a hit blocks the engagement letter until a person clears it.
   - Enquiry content is processed through an API with no data retention and stored only in the firm's own systems.
   - Out-of-scope or conflicted matters get a courteous decline drafted for approval, never an automatic one.
   - Every intake keeps an audit line: received, classified, checked, approved by whom, when.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

11. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
12. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
13. **Slack — Send Channel Message (approval).** Send the summary to your approver with what would be written. Zapier has no wait-for-reply step: with approval mode on, stop the Zap here and re-run the write-back by hand (or from a second Zap triggered by a Slack reaction on the message). With approval mode off, the next step runs immediately.
14. **Filter by Zapier.** Only continue if the stored `approval_mode` is `false`.
15. **Webhooks by Zapier — Custom Request.** POST `https://app.clio.com/api/v4/matters.json` (Clio API; add the API key header). On approval: the matter is created in the practice-management system with the parties and documents, the letter is sent for signature, and the intake is closed.

## Guardrails to keep

- Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically.
- Conflict results are shown with their evidence; a hit blocks the engagement letter until a person clears it.
- Enquiry content is processed through an API with no data retention and stored only in the firm's own systems.
- Out-of-scope or conflicted matters get a courteous decline drafted for approval, never an automatic one.
- Every intake keeps an audit line: received, classified, checked, approved by whom, when.

Full blueprint: https://agentmelt.com/workflows/client-intake-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
