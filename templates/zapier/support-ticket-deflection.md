# Answer Zendesk tickets from your help centre with Claude and escalate the rest — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Zendesk / Intercom / Freshdesk, Pinecone / Supabase / Qdrant, HubSpot / Stripe.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** Zendesk, Intercom, Freshdesk, Help Scout or HubSpot posts each new conversation. Email-only teams use a Gmail or Outlook trigger on the support inbox.
2. **HubSpot — Find Contact — Fetch customer context.** Plan, recent orders or invoices, open tickets and account status from your CRM or billing system, so the answer is specific, not generic.
3. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Classify and prioritise" step of the Support Ticket Deflection Workflow workflow run by Agentmelt.
   Task: Category (billing, access, how-to, bug, cancellation…), sentiment and urgency. Cancellation and complaint categories skip deflection and go straight to a person.
   
   Rules:
   - The agent answers only from your knowledge base and cites the source; no general-knowledge answers.
   - Cancellations, complaints, legal, security and anything with strong negative sentiment always go to a person.
   - Automated answers are marked, and a customer reply reopens the ticket to a human immediately.
   - The confidence threshold is set from measured reopen rates, not by feel, and reviewed weekly.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

4. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
5. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
6. **Webhooks by Zapier — Custom Request — Retrieve knowledge.** Help-centre articles, macros and product docs, chunked and embedded, refreshed nightly.
7. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Draft the answer with a confidence score" step of the Support Ticket Deflection Workflow workflow run by Agentmelt.
   Task: The agent answers only from retrieved passages, cites the article, and reports a confidence score. Questions the knowledge base does not cover get low confidence by design.
   
   Rules:
   - The agent answers only from your knowledge base and cites the source; no general-knowledge answers.
   - Cancellations, complaints, legal, security and anything with strong negative sentiment always go to a person.
   - Automated answers are marked, and a customer reply reopens the ticket to a human immediately.
   - The confidence threshold is set from measured reopen rates, not by feel, and reviewed weekly.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

8. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
9. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
10. **Code by Zapier (JavaScript) — Resolve or route.** High confidence and a deflectable category: send the answer and mark the ticket solved-pending (reopens if the customer replies). Start from `return { ...inputData };` and add the rule.
11. **Zendesk — Update Ticket — Send and log.** Reply through the help desk so it appears in the normal conversation history with an “answered by assistant” tag agents can filter.
12. **Schedule by Zapier (trigger) — Learn from reopens.** Daily: tickets reopened after an automated answer are collected for review; the failing questions become new articles or corrections, and the confidence threshold is tuned from the data.

## Guardrails to keep

- The agent answers only from your knowledge base and cites the source; no general-knowledge answers.
- Cancellations, complaints, legal, security and anything with strong negative sentiment always go to a person.
- Automated answers are marked, and a customer reply reopens the ticket to a human immediately.
- The confidence threshold is set from measured reopen rates, not by feel, and reviewed weekly.

Full blueprint: https://agentmelt.com/workflows/support-ticket-deflection/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
