# Draft monthly client reports from Xero with Claude in Google Docs — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Xero / QuickBooks / Sage, Google Docs / Word, Gmail / Outlook.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** On the day you set after month-end close — or when an accountant asks for a client by name — the pack for that client is built.
2. **Webhooks by Zapier — Custom Request.** GET `https://api.xero.com/api.xro/2.0/Reports/ProfitAndLoss?fromDate=…&toDate=…` (Xero API; add the API key header). Trial balance, P&L, balance sheet, cash and aged receivables from Xero, QuickBooks or Sage for the period, prior period and prior year.
3. **Code by Zapier (JavaScript) — Check the close.** Unreconciled bank lines, unposted drafts, suspense balances: if the close is not clean, the pack waits and the accountant is told what is open. Start from `return { ...inputData };` and add the rule.
4. **Code by Zapier (JavaScript) — Compute the comparisons.** Against budget, prior month and prior year; margins, cash runway, debtor days; the client's own KPIs from their settings. Start from `return { ...inputData };` and add the rule.
5. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Find the variances that matter" step of the Client Reporting Automation workflow run by Agentmelt.
   Task: Ranks movements by size and by whether they are one-off, timing or trend, and names the three a client should hear about — with the evidence lines.
   
   Rules:
   - No pack is drafted on an unclean close; the workflow reports what is open instead.
   - The narrative can only cite movements present in the numbers; causes are stated as 'appears to be' unless the ledger shows them.
   - Every pack is approved by the accountant before it reaches a client.
   - Numbers in the narrative are checked against the tables before the draft is shown.
   - Client data stays in the ledger and the client folder; model calls use an API with no data retention.
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
   You are the "Draft the narrative" step of the Client Reporting Automation workflow run by Agentmelt.
   Task: In the practice's style from past packs: what happened, why, what to watch — two to four paragraphs and the partner's questions, never invented causes.
   
   Rules:
   - No pack is drafted on an unclean close; the workflow reports what is open instead.
   - The narrative can only cite movements present in the numbers; causes are stated as 'appears to be' unless the ledger shows them.
   - Every pack is approved by the accountant before it reaches a client.
   - Numbers in the narrative are checked against the tables before the draft is shown.
   - Client data stays in the ledger and the client folder; model calls use an API with no data retention.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

9. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
10. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
11. **Google Docs — Create Document from Text — Assemble the pack.** The practice's template filled: tables, charts, narrative, KPIs, with the client's branding where used; PDF and editable versions.
12. **Slack — Send Channel Message (approval).** Send the summary to your approver with what would be written. Zapier has no wait-for-reply step: with approval mode on, stop the Zap here and re-run the write-back by hand (or from a second Zap triggered by a Slack reaction on the message). With approval mode off, the next step runs immediately.
13. **Filter by Zapier.** Only continue if the stored `approval_mode` is `false`.
14. **Gmail — Send Email — Deliver and log.** Sent to the client from the accountant's address on approval, with a short cover note; the pack is filed in the client's folder and logged.

## Guardrails to keep

- No pack is drafted on an unclean close; the workflow reports what is open instead.
- The narrative can only cite movements present in the numbers; causes are stated as 'appears to be' unless the ledger shows them.
- Every pack is approved by the accountant before it reaches a client.
- Numbers in the narrative are checked against the tables before the draft is shown.
- Client data stays in the ledger and the client folder; model calls use an API with no data retention.

Full blueprint: https://agentmelt.com/workflows/client-reporting-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
