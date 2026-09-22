# Extract supplier invoices from Gmail with Claude and post them to Xero for approval — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus NetSuite / Xero / QuickBooks / Sage, Slack / email, Google Drive / S3.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Gmail — New Email Matching Search (trigger).** New attachments to ap@ start the run; supplier portals and scanned batches are polled hourly.
2. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Extract fields" step of the Invoice Processing Automation workflow run by Agentmelt.
   Task: Supplier, invoice number, dates, line items, quantities, unit prices, tax, totals, PO reference and bank details, with a confidence per field. Multi-page and multi-currency handled.
   
   Rules:
   - Bank-detail changes never post automatically; they trigger a verification call with the supplier.
   - Auto-approval applies only to PO-matched invoices within tolerance and policy limits; everything else has a named approver.
   - Duplicates are blocked before posting, not caught at month end.
   - Low-confidence extractions are reviewed by a person before matching.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

3. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
4. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
5. **Code by Zapier (JavaScript) — Validate and detect duplicates.** Totals foot, tax is arithmetically right, supplier exists (or is flagged as new), bank details match the master (change = fraud alert), and no invoice with the same supplier + number + amount exists. Start from `return { ...inputData };` and add the rule.
6. **Webhooks by Zapier — Custom Request.** GET `https://api.xero.com/api.xro/2.0/PurchaseOrders?where=PurchaseOrderNumber%3D%3D%22…%22` (Xero API; add the API key header). Three-way match against the ERP: PO lines, quantities received, prices within tolerance.
7. **Code by Zapier (JavaScript) — Route exceptions and approvals.** Clean matches auto-approve within policy limits; mismatches go to the buyer with the specific difference; non-PO invoices go to the cost-centre owner; new suppliers go to procurement for onboarding. Start from `return { ...inputData };` and add the rule.
8. **Slack — Send Channel Message (approval).** Send the summary to your approver with what would be written. Zapier has no wait-for-reply step: with approval mode on, stop the Zap here and re-run the write-back by hand (or from a second Zap triggered by a Slack reaction on the message). With approval mode off, the next step runs immediately.
9. **Filter by Zapier.** Only continue if the stored `approval_mode` is `false`.
10. **Xero — Create Bill — Post to the ERP.** Approved invoices are created in NetSuite, Xero, QuickBooks, Sage or SAP with coding, attachments and the approval trail; payment runs pick them up.
11. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Supplier status replies" step of the Invoice Processing Automation workflow run by Agentmelt.
   Task: Supplier emails asking about payment status are answered from the ERP data (received, approved, scheduled for date) so AP stops fielding calls.
   
   Rules:
   - Bank-detail changes never post automatically; they trigger a verification call with the supplier.
   - Auto-approval applies only to PO-matched invoices within tolerance and policy limits; everything else has a named approver.
   - Duplicates are blocked before posting, not caught at month end.
   - Low-confidence extractions are reviewed by a person before matching.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

12. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
13. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.

## Guardrails to keep

- Bank-detail changes never post automatically; they trigger a verification call with the supplier.
- Auto-approval applies only to PO-matched invoices within tolerance and policy limits; everything else has a named approver.
- Duplicates are blocked before posting, not caught at month end.
- Low-confidence extractions are reviewed by a person before matching.

Full blueprint: https://agentmelt.com/workflows/invoice-processing-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
