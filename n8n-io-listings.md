# n8n.io listing copy

One block per template. Paste the title and description into the n8n creator form; the tags are the ones n8n accepts most often.

## Spend Analysis

**Title:** Spend Analysis (AI + approval step)

**Description:**

AI spend analysis (spend analytics) uses machine learning to classify every invoice and purchase-order line into a category taxonomy, normalise supplier names, and build the spend cube — supplier × category × business unit × time — that procurement needs to find savings. Run as an n8n workflow it refreshes monthly instead of once a year, and an AI agent writes the opportunity summaries a category manager would otherwise spend a week producing.

**How it works**

1. Extract AP and PO lines
2. Normalise suppliers
3. Classify each line
4. Learn from corrections
5. Build the spend cube
6. Detect opportunities
7. Write the opportunity briefs
8. Publish and track

**Guardrails built in:** Classification below the confidence threshold is reviewed by a person before it enters the cube. Supplier merges are logged and reversible; tax-ID matches are the only automatic merges. The AI agent drafts briefs; savings are only reported as realised when finance confirms them.

**Works with:** Claude, Postgres / BigQuery, Looker / Power BI / Metabase, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/spend-analysis/

**Tags:** Supply chain & procurement, AI, Approval, Claude, Postgres / BigQuery, Looker / Power BI / Metabase

**Sources:** Google Cloud — BigQuery documentation — https://cloud.google.com/bigquery/docs; UNGM — United Nations Standard Products and Services Code (UNSPSC) — https://www.ungm.org/Public/UNSPSC; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Demand Forecasting

**Title:** Demand Forecasting (AI + approval step)

**Description:**

AI demand forecasting combines your sales history with the signals a spreadsheet cannot hold — promotions, price changes, weather, holidays, marketing spend, web traffic — and produces a forecast per SKU per location per week with an error band. The workflow below runs that model on a schedule in n8n, and uses an AI agent only where it helps: explaining exceptions to planners and drafting the weekly forecast review.

**How it works**

1. Pull sales history
2. Pull the signals
3. Clean and align
4. Run the forecasting model
5. Score last week's forecast
6. Write forecasts to the planning system
7. Explain the exceptions
8. Publish the weekly review

**Guardrails built in:** The model forecasts; the agent explains. No language model touches a number that goes into replenishment. Every run scores the previous run's accuracy so drift is visible within a week. Planner overrides are captured and evaluated against the model, not silently overwritten.

**Works with:** LightGBM / Chronos / TimesFM / TimeGPT, BigQuery / Snowflake / Postgres, Claude, Google Sheets / planning tool

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/demand-forecasting/

**Tags:** Supply chain & procurement, AI, Approval, LightGBM / Chronos / TimesFM / TimeGPT, BigQuery / Snowflake / Postgres, Claude

**Sources:** Amazon Science — Chronos forecasting models — https://github.com/amazon-science/chronos-forecasting; LightGBM — documentation — https://lightgbm.readthedocs.io/; Nixtla — TimeGPT documentation — https://docs.nixtla.io/

---

## Employee Onboarding

**Title:** Employee Onboarding (AI + approval step)

**Description:**

Employee onboarding automation turns the offer-accepted moment into a workflow: the HRIS fires an event, the workflow creates the checklist by role, requests accounts from IT, schedules training, sends the welcome sequence, and an AI agent answers the new hire's policy questions from your handbook. HR watches a dashboard instead of chasing tasks.

**How it works**

1. Receive the new-hire event
2. Build the checklist for this role
3. Create the tracking board
4. Request accounts and equipment
5. Send documents for signature
6. Schedule the first two weeks
7. Run the welcome sequence
8. Answer policy questions
9. Chase overdue tasks and check in

**Guardrails built in:** The AI agent answers only from the handbook and cites the page; it refuses pay, performance and grievance topics and routes them to HR. Account provisioning is requested, never executed, by the workflow — IT approves in their own tool. Personal data stays in the HRIS; the workflow passes identifiers, not copies of documents.

**Works with:** BambooHR / Rippling / Workday, Notion / Jira / Google Sheets, DocuSign / PandaDoc, Claude, Slack / Microsoft Teams

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/employee-onboarding-automation/

**Tags:** HR, AI, Approval, BambooHR / Rippling / Workday, Notion / Jira / Google Sheets, DocuSign / PandaDoc

**Sources:** BambooHR — API documentation — https://documentation.bamboohr.com/docs; DocuSign — eSignature REST API — https://developers.docusign.com/docs/esign-rest-api/; Slack — API documentation — https://api.slack.com/docs

---

## Automated Code Review

**Title:** Automated Code Review (AI + approval step)

**Description:**

Automated code review adds a consistent first pass to every pull request: the workflow reads the diff with the surrounding context, checks it against your written standards and the linked issue, posts inline comments only for concrete problems (bugs, security, missing tests, breaking changes), classifies the PR's risk, and writes the summary a human reviewer reads before opening the files. Reviewers spend their time on design, not on the things a checklist catches.

**How it works**

1. Receive the PR event
2. Fetch the diff and context
3. Run static checks
4. Analyse the change
5. Filter to what matters
6. Post inline comments and summary
7. Label and route
8. Learn from resolutions

**Guardrails built in:** The workflow never approves or merges; it reviews and labels. A human approval remains required. Comments are posted only for concrete findings with reasoning; style nits go to the summary or nowhere. Code is sent to the model provider under your data-processing terms; repositories can be excluded, and self-hosted models are an option for sensitive code.

**Works with:** Claude, GitHub / GitLab, CI (GitHub Actions, GitLab CI), Linear / Jira

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/automated-code-review/

**Tags:** Engineering, AI, Approval, Claude, GitHub / GitLab, CI (GitHub Actions, GitLab CI)

**Sources:** GitHub — REST API: pull request reviews — https://docs.github.com/en/rest/pulls/reviews; GitHub — Actions documentation — https://docs.github.com/en/actions; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Expansion Opportunity Detection

**Title:** Expansion Opportunity Detection (AI + approval step)

**Description:**

Expansion revenue is the cheapest growth there is, and most of it is missed because the signals live in product analytics no CSM has time to read. The workflow pulls usage, seat counts, feature adoption, plan-limit proximity and buying signals for every account, scores expansion readiness weekly, and gives each CSM a short ranked list with the recommended play and a drafted opening message.

**How it works**

1. Pull usage and account data
2. Pull engagement and buying signals
3. Compute the readiness score
4. Match to a play
5. Draft the opener
6. Route to the owner
7. Track outcomes by signal

**Guardrails built in:** Scores explain themselves — each account shows the signals behind it. Accounts with an open escalation, a churn-risk flag or a renewal within 30 days are excluded or routed to a different play. The agent drafts openers; CSMs send them. No automated upsell emails.

**Works with:** Amplitude / Mixpanel / Pendo, HubSpot / Salesforce, Claude, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/expansion-opportunity-detection/

**Tags:** Customer success, AI, Approval, Amplitude / Mixpanel / Pendo, HubSpot / Salesforce, Claude

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Amplitude — API reference — https://amplitude.com/docs/apis; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Unit Test Generation

**Title:** Unit Test Generation (AI + approval step)

**Description:**

Test generation is where AI coding agents earn their keep with the least risk: the output is verified by running it. The workflow watches pull requests, finds the changed functions without tests, generates tests in the repo's conventions, runs them in CI, discards anything that fails or adds no coverage, and opens a companion PR with the survivors for the engineer to review. Coverage goes up on exactly the code that is changing.

**How it works**

1. Receive the PR and diff
2. Find untested changed functions
3. Assemble context
4. Generate tests
5. Run in CI
6. Keep what passes and adds coverage
7. Open the companion PR
8. Learn from reviews

**Guardrails built in:** Generated tests are proposed in a separate PR; nothing merges without an engineer's review. Only tests that pass, are not flaky, and add coverage are proposed — the run is the filter. The agent cannot modify source code, only add test files.

**Works with:** Claude, GitHub Actions / GitLab CI, Jest / pytest / Go test / JUnit

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/unit-test-generation/

**Tags:** Engineering, AI, Approval, Claude, GitHub Actions / GitLab CI, Jest / pytest / Go test / JUnit

**Sources:** GitHub — Actions documentation — https://docs.github.com/en/actions; Jest — Getting started — https://jestjs.io/docs/getting-started; pytest — documentation — https://docs.pytest.org/

---

## Inventory Optimization

**Title:** Inventory Optimization (AI + approval step)

**Description:**

Inventory optimization is the step after forecasting: turning a forecast and its error band into reorder points, safety stock and order quantities per SKU-location, then generating the purchase suggestions a buyer approves. The workflow recomputes the parameters weekly from actual forecast error and supplier lead-time performance instead of the static min/max most ERPs still use.

**How it works**

1. Read forecasts and error
2. Read inventory and open orders
3. Measure supplier lead times
4. Compute safety stock and reorder points
5. Classify SKUs
6. Generate purchase suggestions
7. Explain parameter changes
8. Publish to buyers and the ERP

**Guardrails built in:** Draft POs only — a buyer approves before anything is sent to a supplier. Parameter changes above a threshold are explained and can be frozen per SKU. Service-level targets are set by finance and operations together, and the achieved level is reported weekly.

**Works with:** ERP / WMS (NetSuite, SAP B1, Cin7, Fishbowl), Claude, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/inventory-optimization/

**Tags:** Supply chain & procurement, AI, Approval, ERP / WMS (NetSuite, SAP B1, Cin7, Fishbowl), Claude, Google Sheets

**Sources:** Oracle — NetSuite documentation — https://docs.oracle.com/en/cloud/saas/netsuite/index.html; ASCM — supply chain standards and body of knowledge — https://www.ascm.org/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Social Listening & Response

**Title:** Social Listening & Response (AI + approval step)

**Description:**

Social listening produces a firehose nobody reads. The workflow reads it: mentions of your brand, competitors and category from X, LinkedIn, Reddit, review sites, YouTube comments and news are collected hourly, classified by intent (buying question, complaint, praise, support request, competitor comparison, PR risk) and sentiment, and turned into actions — a drafted reply for approval, a lead for sales, a ticket for support, or an alert for whoever handles risk.

**How it works**

1. Collect mentions
2. De-duplicate and filter
3. Classify intent and sentiment
4. Draft the response
5. Route by category
6. Approve and post
7. Log everything
8. Weekly listening report

**Guardrails built in:** Nothing is posted publicly without human approval; the agent drafts. Complaints are acknowledged publicly and resolved privately — the agent never debates in public. PR-risk classifications bypass drafting and go straight to a person.

**Works with:** Brand24 / Mention / platform APIs, Claude, Slack, HubSpot + Zendesk

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/social-listening-response/

**Tags:** Marketing, AI, Approval, Brand24 / Mention / platform APIs, Claude, Slack

**Sources:** Meta — Graph API — https://developers.facebook.com/docs/graph-api/; X — Developer platform overview — https://docs.x.com/overview; Slack — API documentation — https://api.slack.com/docs

---

## Employee Offboarding

**Title:** Employee Offboarding (AI + approval step)

**Description:**

Offboarding automation makes the last day as controlled as the first. When the HRIS marks a termination, the workflow opens the access-revocation tickets with a deadline, schedules the equipment return, generates the exit checklist for the manager, sends the exit survey, and confirms every step closed — so no account survives the person who used it.

**How it works**

1. Receive the termination record
2. Assemble the leaver's access map
3. Open revocation tickets with deadlines
4. Schedule equipment return
5. Generate the knowledge-transfer checklist
6. Hand off to finance and payroll
7. Send the exit survey
8. Confirm closure

**Guardrails built in:** The workflow requests revocation; IT executes it. Nothing is deleted automatically. Involuntary exits skip the welcome-style messaging and trigger same-day revocation tickets. The knowledge-transfer draft never includes compensation or performance data.

**Works with:** Okta / Entra ID / Google Workspace, Jira Service Management / ServiceNow, Claude, Typeform / Google Forms

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/employee-offboarding-automation/

**Tags:** HR, AI, Approval, Okta / Entra ID / Google Workspace, Jira Service Management / ServiceNow, Claude

**Sources:** Okta — API reference — https://developer.okta.com/docs/reference/; Google — Workspace Admin SDK — https://developers.google.com/workspace/admin; Atlassian — Jira Service Management Cloud REST API — https://developer.atlassian.com/cloud/jira/service-desk/rest/

---

## Insurance Underwriting Intake

**Title:** Insurance Underwriting Intake (AI + approval step)

**Description:**

Underwriters spend most of their day assembling files, not underwriting. The workflow takes broker submissions as they arrive — emails with ACORD forms, loss runs, schedules of values, spreadsheets — extracts the data, checks completeness, pulls third-party data, runs appetite and rating rules, and delivers a decision-ready file with the open questions listed. Clear-cut declines are answered the same day; underwriters spend their time on the risks that need judgement.

**How it works**

1. Capture and classify attachments
2. Extract application data
3. Check completeness
4. Pull third-party data
5. Apply appetite rules
6. Indicative rating
7. Assemble the file and questions
8. Queue and track

**Guardrails built in:** No binding decisions are automated; the workflow triages and prepares. Declines outside appetite are drafted and sent after a human click unless the carrier chooses to automate below a threshold. Every extracted field carries confidence; low-confidence fields are highlighted for verification before rating. Appetite and rating rules are versioned and owned by underwriting management, not embedded in prompts.

**Works with:** Claude, Policy admin / workbench (Duck Creek, Guidewire, Applied, or in-house), Third-party data providers, Outlook / Gmail

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/insurance-underwriting-intake/

**Tags:** Insurance, AI, Approval, Claude, Policy admin / workbench (Duck Creek, Guidewire, Applied, or in-house), Third-party data providers

**Sources:** ACORD — Standards and architecture — https://www.acord.org/standards-architecture; NAIC — model laws and regulations — https://content.naic.org/model-laws; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Financial Reconciliation

**Title:** Financial Reconciliation (AI + approval step)

**Description:**

Reconciliation is matching: bank lines to ledger entries, processor payouts to invoices, intercompany balances to each other. Almost all of it is deterministic, and the part that is not — explaining why a break exists — is what the AI agent does. The workflow runs daily, so month-end becomes a short list of unexplained items instead of a week of matching.

**How it works**

1. Pull the three sides
2. Match deterministically
3. Classify the breaks
4. Explain the unknowns
5. Route for approval
6. Post approved entries
7. Maintain the reconciliation file
8. Close-readiness report

**Guardrails built in:** Nothing posts to the ledger without an accountant's approval; auto-matching only marks, it does not create entries. The agent explains; it never proposes an amount that is not derivable from the data. Every posted entry carries the match evidence and approver for audit.

**Works with:** Claude, NetSuite / Xero / QuickBooks, Stripe / Adyen + Plaid

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/financial-reconciliation-automation/

**Tags:** Finance & accounting, AI, Approval, Claude, NetSuite / Xero / QuickBooks, Stripe / Adyen + Plaid

**Sources:** Stripe — Balance transactions API — https://docs.stripe.com/api/balance_transactions; Plaid — Transactions — https://plaid.com/docs/transactions/; Xero — Developer documentation — https://developer.xero.com/documentation/

---

## Email Triage

**Title:** Email Triage (AI + approval step)

**Description:**

Email triage automation turns an inbox into a queue with decisions already made: every incoming message is classified (needs reply, FYI, task, meeting request, newsletter, spam), routine replies are drafted for approval, tasks and deadlines are extracted into your task tool, and what reaches the person is a short list ranked by urgency. It runs on shared inboxes (info@, sales@, ops@) and executive inboxes alike.

**How it works**

1. Receive and de-duplicate
2. Classify
3. Fetch context
4. Extract tasks and dates
5. Draft routine replies
6. Route
7. Approve and send
8. Daily digest

**Guardrails built in:** Drafts require approval by default; auto-send is enabled per category by the inbox owner and logged. Complaints, legal, HR and anything from unknown senders with attachments go to a person unread by the agent's reply logic. The agent never invents facts about availability, pricing or commitments; it drafts from the context fetched or asks.

**Works with:** Gmail / Outlook, Claude, Asana / Linear / Notion, Slack

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/email-triage-automation/

**Tags:** Operations, AI, Approval, Gmail / Outlook, Claude, Asana / Linear / Notion

**Sources:** Google — Gmail API guides — https://developers.google.com/workspace/gmail/api/guides; Microsoft Graph — Outlook mail API overview — https://learn.microsoft.com/en-us/graph/api/resources/mail-api-overview; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Support Ticket Deflection

**Title:** Support Ticket Deflection (AI + approval step)

**Description:**

Ticket deflection means resolving the questions your help centre already answers — password resets, invoice copies, “how do I…” — before they reach an agent, and giving agents the rest with a summary, a category and a priority. The workflow sits between your inbox or chat and your help desk: an AI agent answers from the knowledge base with citations when it is confident, and escalates cleanly when it is not.

**How it works**

1. Receive the ticket
2. Fetch customer context
3. Classify and prioritise
4. Retrieve knowledge
5. Draft the answer with a confidence score
6. Resolve or route
7. Send and log
8. Learn from reopens

**Guardrails built in:** The agent answers only from your knowledge base and cites the source; no general-knowledge answers. Cancellations, complaints, legal, security and anything with strong negative sentiment always go to a person. Automated answers are marked, and a customer reply reopens the ticket to a human immediately.

**Works with:** Zendesk / Intercom / Freshdesk, Claude, Pinecone / Supabase / Qdrant, HubSpot / Stripe

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/support-ticket-deflection/

**Tags:** Customer support, AI, Approval, Zendesk / Intercom / Freshdesk, Claude, Pinecone / Supabase / Qdrant

**Sources:** Zendesk — API reference — https://developer.zendesk.com/api-reference/; Intercom — Developer docs — https://developers.intercom.com/docs; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Document & Proposal Generation

**Title:** Document & Proposal Generation (AI + approval step)

**Description:**

Proposals, RFP responses, statements of work and recurring reports are assembled from the same components every time: the client's details, the scope, the relevant past answers, the pricing rules, the boilerplate. The workflow assembles them — pulling the record from the CRM, matching the request to your answer library, drafting each section in your template and flagging what a person must decide — so the writer starts at 70% instead of zero.

**How it works**

1. Receive the request
2. Pull the client record
3. Parse the RFP or brief
4. Retrieve past answers and case material
5. Draft each section
6. Consistency and compliance check
7. Produce the document
8. Route for review and learn

**Guardrails built in:** Every reused answer is sourced to the document it came from; the writer can see what was adapted. Commitments the rules forbid (uncapped liability, guaranteed outcomes) are blocked, not merely flagged. Pricing comes from rules and rate cards; the agent cannot invent a number.

**Works with:** Claude, Pinecone / Supabase, Google Docs / Microsoft Word, HubSpot / Salesforce

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/document-generation-automation/

**Tags:** Operations, AI, Approval, Claude, Pinecone / Supabase, Google Docs / Microsoft Word

**Sources:** Google — Docs API overview — https://developers.google.com/workspace/docs/api; Microsoft Graph — overview — https://learn.microsoft.com/en-us/graph/overview; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview

---

## Subscription & Dunning

**Title:** Subscription & Dunning (AI + approval step)

**Description:**

Involuntary churn — customers lost to a failed card, not a decision — is usually the largest churn line a subscription business never looks at. The workflow watches billing events, runs a retry schedule tuned to card decline codes, sends dunning messages written for the specific failure, handles plan changes and cancellation requests with the right offer, and reports recovered revenue weekly.

**How it works**

1. Receive the billing event
2. Choose the retry strategy
3. Draft the dunning message
4. Send across the sequence
5. Handle plan changes and pauses
6. Cancellation intercept
7. Alert finance and the owner
8. Weekly recovery report

**Guardrails built in:** Retry schedules respect card-network rules and the provider's limits. Save offers come only from the finance-approved set; the agent picks, it does not invent discounts. Customers who ask to cancel and decline the offer are cancelled promptly — no dark patterns.

**Works with:** Stripe / Chargebee / Recurly, Claude, Gmail + Twilio + Intercom, Slack + Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/subscription-dunning-automation/

**Tags:** Finance & accounting, AI, Approval, Stripe / Chargebee / Recurly, Claude, Gmail + Twilio + Intercom

**Sources:** Stripe — Smart Retries — https://docs.stripe.com/billing/revenue-recovery/smart-retries; Chargebee — Dunning — https://www.chargebee.com/docs/2.0/dunning.html; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Logistics Optimization

**Title:** Logistics Optimization (AI + approval step)

**Description:**

Logistics optimization at the operational level means two things: choosing the right carrier and service for each shipment, and knowing about delays before customers do. The workflow rates every order across your carrier contracts, picks the cheapest service that meets the promised date, books it, then watches tracking events and uses an AI agent to draft customer updates and carrier claims when something slips.

**How it works**

1. Receive the shipment
2. Rate across carriers
3. Select the service
4. Book and label
5. Track in flight
6. Detect and explain delays
7. Notify and escalate
8. Audit carrier invoices

**Guardrails built in:** Customer messages for orders above a value threshold are approved by a person before sending. Carrier selection rules (customer or product overrides) always win over cost. Claims are drafted, not filed, until the logistics lead confirms.

**Works with:** EasyPost / Shippo / carrier APIs, Claude, Gmail / Zendesk, Google Sheets / Postgres

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/logistics-optimization/

**Tags:** Supply chain & procurement, AI, Approval, EasyPost / Shippo / carrier APIs, Claude, Gmail / Zendesk

**Sources:** EasyPost — API documentation — https://docs.easypost.com/; Shippo — API documentation — https://docs.goshippo.com/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Proactive Customer Outreach

**Title:** Proactive Customer Outreach (AI + approval step)

**Description:**

Proactive outreach flips support from reactive to preventive: the workflow monitors the events that reliably lead to a ticket or a cancellation — a failed payment, a spike in errors, a feature never activated, a delayed shipment — and sends the right message before the customer has to ask. An AI agent personalises each message from the customer's actual context; a person approves anything sensitive.

**How it works**

1. Receive or detect the signal
2. Load the customer's context
3. Decide whether to reach out
4. Draft the message
5. Approve if sensitive
6. Send on the right channel
7. Log and watch the response
8. Report what it prevented

**Guardrails built in:** Frequency cap: one proactive message per customer per week across all scenarios. Sensitive scenarios require a human click; the agent never sends about money or churn risk unattended. Every message links to one action and is sent from a real inbox that receives replies.

**Works with:** Stripe / Chargebee, Segment / PostHog / Mixpanel, Claude, HubSpot / Intercom

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/proactive-customer-outreach/

**Tags:** Customer support, AI, Approval, Stripe / Chargebee, Segment / PostHog / Mixpanel, Claude

**Sources:** Stripe — Webhooks — https://docs.stripe.com/webhooks; Segment — Documentation — https://segment.com/docs/; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Customer Onboarding

**Title:** Customer Onboarding (AI + approval step)

**Description:**

Customers who activate in the first two weeks stay; customers who stall churn. The workflow tracks each new customer against your activation milestones, sends a specific nudge when progress stops (not a scheduled drip), answers setup questions from your documentation with an AI agent, and hands the account to a CSM only when the signals say a person is needed.

**How it works**

1. Register the new account
2. Track milestones from product events
3. Detect stalls
4. Send the right nudge
5. Answer setup questions
6. Escalate to a person
7. Celebrate activation and hand over
8. Report the funnel

**Guardrails built in:** Nudges are sent only on stalls, with a cap of one per milestone; no message for customers making progress. The setup-question agent answers from documentation with citations and escalates unknowns. High-value accounts get a person on the first stall, not the third.

**Works with:** Segment / Mixpanel / PostHog, Claude, HubSpot / Intercom

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-onboarding-automation/

**Tags:** Customer success, AI, Approval, Segment / Mixpanel / PostHog, Claude, HubSpot / Intercom

**Sources:** Segment — Documentation — https://segment.com/docs/; Intercom — Developer docs — https://developers.intercom.com/docs; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview

---

## Supplier Risk Monitoring

**Title:** Supplier Risk Monitoring (AI + approval step)

**Description:**

Supplier risk monitoring replaces the annual supplier survey with a continuous score. The workflow pulls financial health, news, delivery performance and geographic risk for every critical supplier, computes a risk score per supplier per week, and when a score crosses a threshold an AI agent reads the evidence and drafts the brief: what changed, what it affects, what to do.

**How it works**

1. Load the supplier portfolio
2. Pull financial signals
3. Pull news and events
4. Measure delivery performance
5. Classify and weight signals
6. Compute the composite score
7. Draft the risk brief
8. Alert and track

**Guardrails built in:** Scores are explainable: every alert lists the signals and weights that produced it. News is classified for relevance and severity before it affects a score; a single article never triggers an alert on its own. The agent recommends; procurement decides and records the action.

**Works with:** D&B / Creditsafe / Coface, News API / GDELT, Claude, Slack + Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/supplier-risk-monitoring/

**Tags:** Supply chain & procurement, AI, Approval, D&B / Creditsafe / Coface, News API / GDELT, Claude

**Sources:** GDELT Project — global news event data — https://www.gdeltproject.org/; Dun & Bradstreet — Direct+ API documentation — https://directplus.documentation.dnb.com/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Prior Authorization

**Title:** Prior Authorization (AI + approval step)

**Description:**

Prior authorization is a documentation-assembly problem with a deadline. The workflow checks each order against payer rules to see whether auth is required, gathers the supporting documentation from the EHR, has an AI agent draft the medical-necessity summary against the payer's published criteria, submits through the portal or fax with a person's click, tracks the status, and drafts the appeal when a denial comes back. Staff handle exceptions and clinical judgement; the paperwork runs itself.

**How it works**

1. Detect auth requirement
2. Gather documentation
3. Check completeness against criteria
4. Draft the medical-necessity summary
5. Submit
6. Track status
7. Draft appeals
8. Report

**Guardrails built in:** Every submission and appeal is reviewed and signed by a clinician or authorised staff member; nothing is sent automatically. PHI stays within HIPAA-covered infrastructure (self-hosted n8n or a covered cloud, model API under a BAA); the model sees the minimum necessary. The summary maps documentation to criteria; it never asserts clinical facts that are not in the record.

**Works with:** n8n (self-hosted), Claude (under BAA), EHR (Epic, athenahealth, eClinicalWorks…), Availity / payer portals

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/prior-authorization-automation/

**Tags:** Operations, AI, Approval, n8n (self-hosted), Claude (under BAA), EHR (Epic, athenahealth, eClinicalWorks…)

**Sources:** CMS — Interoperability and Prior Authorization Final Rule (CMS-0057-F) — https://www.cms.gov/priorities/key-initiatives/burden-reduction/interoperability/policies-and-regulations/cms-interoperability-and-prior-authorization-final-rule-cms-0057-f; HHS — HIPAA for professionals — https://www.hhs.gov/hipaa/for-professionals/index.html; Availity — payer connectivity — https://www.availity.com/

---

## Customer Health Scoring

**Title:** Customer Health Scoring (AI + approval step)

**Description:**

A customer health score is only useful if it moves before the customer leaves and tells the CSM what to do. The workflow computes one score per account every week from usage trend, support experience, billing behaviour, engagement and sentiment, alerts on drops with the cause, and has an AI agent draft the check-in — so the CSM's day starts with the accounts that need them.

**How it works**

1. Collect the components
2. Score each component
3. Analyse ticket sentiment
4. Compute score and trend
5. Detect drops and thresholds
6. Draft the intervention
7. Alert the owner and update the CRM
8. Calibrate quarterly

**Guardrails built in:** Scores show their components; no black-box number. Alerts are suppressed for accounts already in a save play, so CSMs are not double-pinged. Outreach is drafted for a person to send; nothing goes to the customer automatically.

**Works with:** Mixpanel / Amplitude / PostHog, Zendesk / Intercom, Claude, HubSpot / Salesforce

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-health-scoring/

**Tags:** Customer success, AI, Approval, Mixpanel / Amplitude / PostHog, Zendesk / Intercom, Claude

**Sources:** Mixpanel — API reference — https://developer.mixpanel.com/reference/overview; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Zendesk — API reference — https://developer.zendesk.com/api-reference/

---

## Insurance Claims Intake

**Title:** Insurance Claims Intake (AI + approval step)

**Description:**

First notice of loss arrives by phone, email, portal and app, and the first day is spent creating the record, verifying coverage and deciding who handles it. The workflow captures the claim from any channel, extracts the facts, verifies the policy and coverage, triages severity and fraud indicators, fast-tracks simple claims toward settlement, and assigns complex ones to the right adjuster with a complete file and an acknowledgement already sent to the claimant.

**How it works**

1. Capture the notice
2. Extract the facts
3. Verify policy and coverage
4. Triage severity and complexity
5. Screen fraud indicators
6. Route
7. Acknowledge the claimant
8. Create the file and assign

**Guardrails built in:** Coverage determinations and claim decisions are made by adjusters; the workflow verifies and summarises. Fraud indicators are flagged with evidence for SIU review, never used to deny or delay a claim automatically. Claimant communications are approved by a person for complex or injury claims.

**Works with:** Claude, Claims system (Guidewire ClaimCenter, Duck Creek, Snapsheet, in-house), Policy admin, Telephony (Five9, Talkdesk)

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/insurance-claims-intake/

**Tags:** Insurance, AI, Approval, Claude, Claims system (Guidewire ClaimCenter, Duck Creek, Snapsheet, in-house), Policy admin

**Sources:** ACORD — Standards and architecture — https://www.acord.org/standards-architecture; NAIC — model laws and regulations — https://content.naic.org/model-laws; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Payroll

**Title:** Payroll (AI + approval step)

**Description:**

Payroll automation does not replace your payroll provider — it removes the week of spreadsheet reconciliation before every run. the workflow pulls hours, leave and changes from their source systems, validates them against policy, uses an AI review step to flag anomalies in plain language, and pushes an approved, clean file to Gusto, ADP, Rippling or Deel.

**How it works**

1. Collect period inputs
2. Normalise into one employee ledger
3. Validate against policy
4. Anomaly review
5. Send the exceptions report
6. Wait for approval
7. Push the run to the provider
8. Reconcile after the run

**Guardrails built in:** The workflow never submits without an explicit human approval; the Wait node is the control. The AI step annotates only; it has no write access to amounts. Every submitted file is stored with a hash and the approver's identity for audit.

**Works with:** Gusto / ADP / Rippling / Deel, Claude, Slack, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/payroll-automation/

**Tags:** HR, AI, Approval, Gusto / ADP / Rippling / Deel, Claude, Slack

**Sources:** Gusto — API documentation — https://docs.gusto.com/; IRS — Publication 15, Employer's Tax Guide — https://www.irs.gov/publications/p15; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Security Alert Triage

**Title:** Security Alert Triage (AI + approval step)

**Description:**

Security teams drown in alerts, most of them benign. The workflow takes each alert from the SIEM or EDR, enriches it — asset owner, user context, threat intel, recent related events — scores it against your rules and known-benign patterns, auto-closes the noise with a documented reason, and gives analysts a ranked queue where each alert already has the timeline, the enrichment and a suggested first action.

**How it works**

1. Receive and normalise the alert
2. Enrich entities
3. Correlate with recent activity
4. Score and classify
5. Analyst-style assessment
6. Auto-close or queue
7. Notify and escalate
8. Weekly tuning report

**Guardrails built in:** The workflow never takes containment actions (isolate host, disable user) on its own; it recommends and a human executes, or a separate approved playbook runs with explicit authorisation. Auto-closed alerts keep the full enrichment and reason and are sampled weekly for false-negative review. Critical patterns bypass scoring and page immediately.

**Works with:** Claude, Splunk / Sentinel / CrowdStrike, VirusTotal / AbuseIPDB / MISP, Slack / PagerDuty

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/security-alert-triage/

**Tags:** Security & IT, AI, Approval, Claude, Splunk / Sentinel / CrowdStrike, VirusTotal / AbuseIPDB / MISP

**Sources:** MITRE ATT&CK — https://attack.mitre.org/; NIST SP 800-61 Rev. 3 — Incident response recommendations — https://csrc.nist.gov/pubs/sp/800/61/r3/final; VirusTotal — API reference — https://docs.virustotal.com/reference/overview

---

## Competitor Monitoring

**Title:** Competitor Monitoring (AI + approval step)

**Description:**

Competitor intelligence is usually a slide someone made once. The workflow watches the sources that actually reveal a competitor's moves — pricing pages, changelogs and release notes, job postings, app-store and G2 reviews, ad libraries, press — detects material changes rather than noise, and has an AI agent write a weekly brief: what changed, what it suggests about their strategy, and what your team should do about it.

**How it works**

1. Snapshot monitored pages
2. Collect feeds
3. Detect material changes
4. Classify and assess
5. Instant alerts for pricing
6. Write the weekly brief
7. Update battle cards
8. Distribute and log

**Guardrails built in:** Only public sources are monitored; no login walls, no scraping in violation of terms. Assessments are labelled as inference and tied to the evidence snapshot. Pricing alerts include the raw before/after so nobody acts on a misparse.

**Works with:** Claude, Browserless / Firecrawl, Notion + Slack

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/competitor-monitoring/

**Tags:** Marketing, AI, Approval, Claude, Browserless / Firecrawl, Notion + Slack

**Sources:** Firecrawl — documentation — https://docs.firecrawl.dev/introduction; IETF RFC 9309 — Robots Exclusion Protocol — https://www.rfc-editor.org/rfc/rfc9309; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Content Repurposing

**Title:** Content Repurposing (AI + approval step)

**Description:**

Content repurposing is the most-sold automation workflow because the input is already made: a podcast episode, a webinar, a founder interview. The workflow transcribes it, extracts the structure and the quotable moments, drafts every derivative asset in your voice — show notes, a blog post, five LinkedIn posts, an X thread, a newsletter section, clip timestamps for the editor — and puts them in a review board and the scheduler within 24 hours.

**How it works**

1. Transcribe
2. Extract structure
3. Draft the long-form
4. Draft the short-form
5. Clip list for the editor
6. Review board
7. Schedule approved assets
8. Report performance back

**Guardrails built in:** Nothing publishes without approval on the review board. Quotes are verbatim from the transcript with timestamps; the agent cannot invent a quote. Claims extracted from the episode are attributed to the speaker, not stated as fact by the brand.

**Works with:** Deepgram / AssemblyAI, Claude, Notion, Buffer / Hootsuite / CMS

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/content-repurposing-automation/

**Tags:** Marketing, AI, Approval, Deepgram / AssemblyAI, Claude, Notion

**Sources:** Deepgram — documentation — https://developers.deepgram.com/home; AssemblyAI — documentation — https://www.assemblyai.com/docs; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Customer Win-Back

**Title:** Customer Win-Back (AI + approval step)

**Description:**

Most win-back email is a discount blasted at everyone who ever cancelled. The workflow segments churned customers by exit reason and value, waits for a trigger that makes a return plausible — a feature they asked for shipped, their season started, a pricing change — and sends a specific message with one approved offer. Reactivations are tracked to the segment and trigger so you learn what actually brings people back.

**How it works**

1. Build the churned segment
2. Classify the reason
3. Match triggers to segments
4. Draft the message
5. Approve high-value sends
6. Send and route replies
7. Track reactivation

**Guardrails built in:** Excluded segments (business closed, requested no contact, poor fit) never receive win-back messages. One win-back message per account per quarter unless they reply. Offers come only from the approved set; the agent picks, it never invents a discount.

**Works with:** Claude, Stripe / Chargebee + HubSpot, Gmail / Customer.io

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-win-back-automation/

**Tags:** Customer success, AI, Approval, Claude, Stripe / Chargebee + HubSpot, Gmail / Customer.io

**Sources:** Stripe — Subscriptions API — https://docs.stripe.com/api/subscriptions; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Appointment Reminder

**Title:** Appointment Reminder (AI + approval step)

**Description:**

Appointment reminders are the highest-return automation a practice or service business can run: a reminder sequence with two-way confirmation on SMS, email and voice, reschedule handling in the same thread, and a waitlist that fills cancelled slots automatically. The AI agent's job is small and specific — understanding free-text replies (“can we do Thursday instead?”) and drafting the reply — while the workflow runs the cadence.

**How it works**

1. Pull upcoming appointments
2. Decide the cadence and channel
3. Send the reminder
4. Understand replies
5. Book reschedules from real availability
6. Fill cancellations from the waitlist
7. Update the record and the desk
8. Report weekly

**Guardrails built in:** Only patients with recorded consent for SMS or automated calls are messaged; opt-out words stop the sequence immediately. Messages contain no clinical detail — appointment type, time and location only — to stay within HIPAA-safe messaging practice. Reschedules are booked only into real availability; the agent never promises a slot it cannot see.

**Works with:** Twilio, Claude, Scheduling system (Dentrix, Cliniko, Acuity, Calendly…)

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/appointment-reminders-automation/

**Tags:** Operations, AI, Approval, Twilio, Claude, Scheduling system (Dentrix, Cliniko, Acuity, Calendly…)

**Sources:** FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## KYC/AML Monitoring

**Title:** KYC/AML Monitoring (AI + approval step)

**Description:**

Compliance teams drown in screening hits, most of them false positives, each needing a documented decision. The workflow runs screening at onboarding and on a schedule against sanctions, PEP and adverse-media sources, applies your rules to transactions, assembles each alert into a case with the evidence, and has an AI agent draft the case narrative — the analyst decides, and every decision is logged in the form regulators expect.

**How it works**

1. Screen the customer
2. Pre-assess matches
3. Evaluate transactions
4. Build the case
5. Route to the analyst
6. Record the decision
7. Continuous re-screening
8. Regulatory reporting

**Guardrails built in:** No case is closed without an analyst's recorded decision; the agent drafts, never decides. Sanctions matches always reach a senior analyst regardless of the draft assessment. Every decision is logged in a tamper-evident store with actor, rationale and timestamp.

**Works with:** n8n (self-hosted), Claude, ComplyAdvantage / Dow Jones / OpenSanctions, Postgres

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/kyc-aml-monitoring/

**Tags:** Finance & accounting, AI, Approval, n8n (self-hosted), Claude, ComplyAdvantage / Dow Jones / OpenSanctions

**Sources:** FATF — The FATF Recommendations — https://www.fatf-gafi.org/en/publications/Fatfrecommendations/Fatf-recommendations.html; OpenSanctions — documentation — https://www.opensanctions.org/docs/; FinCEN — Financial Crimes Enforcement Network — https://www.fincen.gov/

---

## Inbound Lead Qualification

**Title:** Inbound Lead Qualification (AI + approval step)

**Description:**

Speed to lead is the most reliable lever in inbound sales, and most teams take hours. The workflow enriches each form submission the second it arrives, scores it against your ideal customer profile, sends a personalised first reply that asks the one qualifying question, and routes hot leads to the right rep in Slack with everything they need to call — while nurturing the rest automatically.

**How it works**

1. Receive the submission
2. Enrich
3. Score against the ICP
4. Read the message
5. Route
6. Notify the rep with context
7. Update the CRM
8. Follow up on silence

**Guardrails built in:** The first reply commits to nothing: no pricing, no availability, no promises — it acknowledges and asks. Free-mail and suspicious submissions are never enriched with paid credits. Reps can override routing; overrides are logged and feed the threshold review.

**Works with:** Clay / Apollo / Clearbit, Claude, HubSpot / Salesforce, Slack + Calendly

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/inbound-lead-qualification/

**Tags:** Sales, AI, Approval, Clay / Apollo / Clearbit, Claude, HubSpot / Salesforce

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Calendly — API documentation — https://developer.calendly.com/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Data Migration

**Title:** Data Migration (AI + approval step)

**Description:**

Migrations fail on mapping and validation, not on moving bytes. The workflow profiles the source, proposes the field mapping with an AI agent that reads both schemas and sample values, lets a person confirm it, applies transformation rules, validates on samples with a reconciliation report, dry-runs, and performs the cutover in batches with a rollback path. The spreadsheet of field mappings becomes a versioned artefact and the migration becomes repeatable.

**How it works**

1. Profile the source
2. Propose the mapping
3. Confirm the mapping
4. Apply transformations
5. Validate
6. Dry run
7. Cut over in batches
8. Reconcile and hand over

**Guardrails built in:** No phase runs without an explicit trigger; cutover requires a dry run that passed. The mapping is confirmed by a person; the agent proposes with confidence, it does not decide. The source is read-only during cutover and a tested rollback exists before the first production batch.

**Works with:** Claude, Postgres / BigQuery, Target APIs (HubSpot, Salesforce, Zendesk…)

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/data-migration-automation/

**Tags:** Engineering, AI, Approval, Claude, Postgres / BigQuery, Target APIs (HubSpot, Salesforce, Zendesk…)

**Sources:** PostgreSQL — documentation — https://www.postgresql.org/docs/; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Cold Outbound

**Title:** Cold Outbound (AI + approval step)

**Description:**

An outbound sales agent does the research and writing a good SDR would do for each prospect, at a volume a person cannot sustain, inside limits that protect your domain. The workflow builds the list from your ICP, researches each account (site, news, hiring, tech), writes a first line and a short email grounded in that research, sequences with reply and bounce detection, and routes replies to a rep.

**How it works**

1. Build the batch
2. Research each account
3. Write the first line and email
4. Quality gate
5. Load into the sequencer
6. Detect replies and classify
7. Hand to a rep
8. Report by angle and segment

**Guardrails built in:** Daily volume per mailbox is capped and warm-up is respected; the workflow never sends outside the sequencer's limits. Emails that fail the specificity check are not sent; generic filler is worse than silence. Any human reply stops the sequence immediately; unsubscribes are honoured across all lists.

**Works with:** Claude, Apollo / Clay, Instantly / Smartlead / Lemlist, HubSpot / Salesforce

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/cold-outbound-sequencing/

**Tags:** Sales, AI, Approval, Claude, Apollo / Clay, Instantly / Smartlead / Lemlist

**Sources:** Google — Email sender guidelines — https://support.google.com/a/answer/81126; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business; Apollo.io — API documentation — https://docs.apollo.io/

---

## Weekly Reporting

**Title:** Weekly Reporting (AI + approval step)

**Description:**

Every team produces a weekly report from the same queries and the same template, and someone spends Monday morning assembling it. The workflow runs the queries, computes the week-over-week and target deltas, has an AI agent draft the narrative — what moved, why, what to watch — from the numbers and last week's report, and posts it for a one-click approval. The person who used to assemble it now edits three sentences.

**How it works**

1. Run the metric queries
2. Assemble the metrics table
3. Pull context
4. Draft the narrative
5. Render the report
6. Approve
7. Distribute
8. Maintain the catalogue

**Guardrails built in:** Every number in the narrative must appear in the metrics table; the agent cannot introduce figures. Causal claims are phrased as likely and tied to a context event; where no event exists the narrative says the cause is unknown. The report is approved by its owner before distribution.

**Works with:** Claude, BigQuery / Snowflake / Postgres, Google Docs + Slack

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/weekly-reporting-automation/

**Tags:** Operations, AI, Approval, Claude, BigQuery / Snowflake / Postgres, Google Docs + Slack

**Sources:** Google Cloud — BigQuery documentation — https://cloud.google.com/bigquery/docs; Google — Docs API overview — https://developers.google.com/workspace/docs/api; Slack — API documentation — https://api.slack.com/docs

---

## Real Estate Listing

**Title:** Real Estate Listing (AI + approval step)

**Description:**

Every listing needs the same set of marketing assets and every agent writes them from scratch or not at all. The workflow takes the listing data and photos, drafts the MLS description within character limits and fair-housing rules, produces the social posts, the email to the buyer list and a virtual-tour script, and puts them in front of the agent for a two-minute review. About three hours saved per listing, every listing.

**How it works**

1. Receive the listing
2. Describe the photos
3. Draft the MLS description
4. Draft the derivatives
5. Compliance and brand check
6. Review and approve
7. Publish
8. Track

**Guardrails built in:** Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit. Facts in the copy are checked against the listing data — no invented square footage or school ratings. The agent approves every asset; nothing publishes automatically.

**Works with:** Claude, Follow Up Boss / kvCORE, Mailchimp / Constant Contact, Buffer / Meta API

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/listing-description-automation/

**Tags:** Marketing, AI, Approval, Claude, Follow Up Boss / kvCORE, Mailchimp / Constant Contact

**Sources:** U.S. Department of Justice — The Fair Housing Act — https://www.justice.gov/crt/fair-housing-act-1; Follow Up Boss — API documentation — https://docs.followupboss.com/; Meta — Graph API — https://developers.facebook.com/docs/graph-api/

---

## IT Helpdesk

**Title:** IT Helpdesk (AI + approval step)

**Description:**

Level-1 IT is repetitive by definition: password resets, access to a shared drive, a licence for a tool, 'how do I connect to the VPN'. The workflow handles those through a Slack or Teams bot and the ticket system — answering from your IT knowledge base, executing approved self-service actions through the identity provider and MDM with the right approvals, and creating well-formed tickets for everything else. IT staff handle problems, not requests.

**How it works**

1. Receive the request
2. Classify the request
3. Answer from the knowledge base
4. Self-service actions with approval
5. Execute through the systems
6. Create or update the ticket
7. Route unresolved requests
8. Improve the knowledge base

**Guardrails built in:** Identity is taken from the chat platform's SSO, never from the message; sensitive actions require a fresh MFA step. Access grants always require manager (or app owner) approval recorded in the ticket; privileged groups are excluded from self-service. Every automated action is logged with requester, approver and timestamp for audit.

**Works with:** Claude, Okta / Entra ID / Google Workspace, Jamf / Intune, Jira Service Management / Freshservice

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/it-helpdesk-automation/

**Tags:** Security & IT, AI, Approval, Claude, Okta / Entra ID / Google Workspace, Jamf / Intune

**Sources:** Okta — API reference — https://developer.okta.com/docs/reference/; Microsoft Graph — overview — https://learn.microsoft.com/en-us/graph/overview; Jamf — developer portal — https://developer.jamf.com/

---

## Purchase Order

**Title:** Purchase Order (AI + approval step)

**Description:**

Purchase requests arrive by email, get approved in a thread nobody can find later, and become POs by re-keying. The workflow takes the request from a form or Slack, has an AI agent complete and normalise it (the right category, the preferred supplier, the budget line), checks budget and policy, routes approvals by amount and category with reminders, creates the PO in the ERP, sends it to the supplier and tracks receipt — with a full audit trail.

**How it works**

1. Receive the request
2. Normalise and complete
3. Check budget and policy
4. Route approvals
5. Create the PO
6. Send to the supplier
7. Track receipt
8. Report committed spend

**Guardrails built in:** No PO is created without the approvals the policy matrix requires; the workflow enforces, it does not decide. Supplier suggestions come from the approved catalogue; new suppliers go through onboarding first. Budget checks use live data; over-budget requests are flagged, not blocked silently.

**Works with:** Claude, NetSuite / Dynamics / Xero, Slack

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/purchase-order-automation/

**Tags:** Supply chain & procurement, AI, Approval, Claude, NetSuite / Dynamics / Xero, Slack

**Sources:** Oracle — NetSuite documentation — https://docs.oracle.com/en/cloud/saas/netsuite/index.html; Xero — Developer documentation — https://developer.xero.com/documentation/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Invoice Processing

**Title:** Invoice Processing (AI + approval step)

**Description:**

Invoice processing automation takes the supplier invoice from wherever it arrives — email attachment, portal, scan — extracts every field, validates it against the PO and the receipt, routes it to the right approver with the exceptions highlighted, and posts it to the ERP coded and ready to pay. Accounts payable handles exceptions instead of keying.

**How it works**

1. Capture the invoice
2. Extract fields
3. Validate and detect duplicates
4. Match to PO and receipt
5. Route exceptions and approvals
6. Approve on the phone
7. Post to the ERP
8. Supplier status replies

**Guardrails built in:** Bank-detail changes never post automatically; they trigger a verification call with the supplier. Auto-approval applies only to PO-matched invoices within tolerance and policy limits; everything else has a named approver. Duplicates are blocked before posting, not caught at month end.

**Works with:** Claude, NetSuite / Xero / QuickBooks / Sage, Slack / email, Google Drive / S3

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/invoice-processing-automation/

**Tags:** Finance & accounting, AI, Approval, Claude, NetSuite / Xero / QuickBooks / Sage, Slack / email

**Sources:** Xero — Developer documentation — https://developer.xero.com/documentation/; Intuit — QuickBooks Online API, getting started — https://developer.intuit.com/app/developer/qbo/docs/get-started; FBI IC3 — Business email compromise — https://www.ic3.gov/CrimeInfo/BEC

---

## Meeting Prep

**Title:** Meeting Prep (AI + approval step)

**Description:**

Reps walk into calls under-prepared because research takes twenty minutes and the calendar is full. The workflow watches the calendar, and for every external meeting assembles a one-page brief from the CRM, the company's site and news, LinkedIn-level role data, past interactions and product usage — then has the AI agent write the three angles worth raising. It lands in Slack an hour before the call.

**How it works**

1. Find upcoming external meetings
2. Identify attendees and account
3. Research the company
4. Research the people
5. Write the brief
6. Deliver
7. Capture the outcome

**Guardrails built in:** Only public and first-party data; no scraping behind logins, no personal data beyond professional role. Every statement in the brief carries a source; the agent is instructed to omit rather than guess. Briefs go only to the rep and the CRM; they are not forwarded externally.

**Works with:** Claude, HubSpot / Salesforce, Clay / Apollo

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/meeting-prep-research/

**Tags:** Sales, AI, Approval, Claude, HubSpot / Salesforce, Clay / Apollo

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Apollo.io — API documentation — https://docs.apollo.io/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Contract Review

**Title:** Contract Review (AI + approval step)

**Description:**

Contract review is comparison: what does this NDA, MSA or vendor agreement say, and how does that differ from what we accept? The workflow extracts the clauses, compares each to your playbook of standard and fallback positions, flags deviations with severity, drafts the redline for the deviations, and routes the contract to the right reviewer — sales ops for a standard NDA, legal for an indemnity change. Lawyers review deviations, not documents.

**How it works**

1. Capture and identify
2. Extract clauses
3. Compare to the playbook
4. Draft the redline
5. Route by risk
6. Review surface
7. Log and learn

**Guardrails built in:** The workflow triages and drafts; a person approves every contract and every redline before it goes to the counterparty. Major-risk clauses always reach a lawyer regardless of the deviation score. Extraction confidence is shown; low-confidence clauses are flagged for manual reading.

**Works with:** Claude, Google Docs / Word, Ironclad / DocuSign CLM / PandaDoc

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/contract-review-automation/

**Tags:** Operations, AI, Approval, Claude, Google Docs / Word, Ironclad / DocuSign CLM / PandaDoc

**Sources:** DocuSign — Developer center — https://developers.docusign.com/; Ironclad — API documentation — https://developer.ironcladapp.com/; Google — Docs API overview — https://developers.google.com/workspace/docs/api

---

## Customer Feedback Analysis

**Title:** Customer Feedback Analysis (AI + approval step)

**Description:**

Feedback arrives in a dozen places and is read in none of them systematically. The workflow collects every piece — NPS and CSAT verbatims, reviews, support tickets, sales-call notes, social mentions — classifies each against your theme taxonomy with sentiment and a quote, aggregates weekly, and has an AI agent write the report: what customers are saying most, what is rising, what is new, with the evidence. Product and CS get one document instead of six dashboards.

**How it works**

1. Collect feedback
2. Classify by theme and sentiment
3. Extract the quotable line
4. Aggregate
5. Write the weekly report
6. Route urgent items
7. Deliver and store
8. Maintain the taxonomy

**Guardrails built in:** Personal data is stripped from quotes; sources are linked, not reproduced. The taxonomy is owned by product; the agent proposes new themes, it does not create them. Inference is labelled as inference and separated from counts and quotes.

**Works with:** Claude, Zendesk / Intercom / Gong, Notion + Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-feedback-analysis/

**Tags:** Customer success, AI, Approval, Claude, Zendesk / Intercom / Gong, Notion + Google Sheets

**Sources:** Zendesk — API reference — https://developer.zendesk.com/api-reference/; Intercom — Developer docs — https://developers.intercom.com/docs; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Review Response

**Title:** Review Response (AI + approval step)

**Description:**

Responding to every review matters for ranking and for the next customer reading it, and almost nobody does it consistently. The workflow collects new reviews across Google Business Profile, Yelp, Trustpilot, Facebook and app stores, classifies sentiment and topic, drafts a specific response in the business's voice, sends it for a one-click approval, and routes genuine complaints to the owner or manager before any public reply goes out.

**How it works**

1. Collect new reviews
2. Classify
3. Fetch context
4. Draft the response
5. Route negatives to a person first
6. Approve and post
7. Track resolution
8. Monthly insight report

**Guardrails built in:** Negative and sensitive reviews are never answered publicly without a person's approval. Replies never dispute facts in public, mention other customers, or reveal personal data. Positive-review auto-posting is enabled only after a calibration period and can be turned off per location.

**Works with:** Claude, Google Business Profile API / Birdeye / Podium, Slack / SMS

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/review-response-automation/

**Tags:** Marketing, AI, Approval, Claude, Google Business Profile API / Birdeye / Podium, Slack / SMS

**Sources:** Google — Business Profile APIs — https://developers.google.com/my-business; FTC — final rule banning fake reviews and testimonials — https://www.ftc.gov/news-events/news/press-releases/2024/08/federal-trade-commission-announces-final-rule-banning-fake-reviews-testimonials; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Resume Screening

**Title:** Resume Screening (AI + approval step)

**Description:**

Resume screening automation applies the role's criteria — the same criteria, the same way — to every application, and explains each score so the recruiter can disagree. The workflow parses applications from the ATS, scores must-have and nice-to-have criteria with evidence quotes, flags claims to verify, and produces a ranked shortlist with the reasoning; the recruiter decides who to call.

**How it works**

1. Receive the application
2. Load the role criteria
3. Parse the resume
4. Score against criteria with evidence
5. Flag verification items
6. Build the ranked shortlist
7. Present to the recruiter
8. Audit and bias monitoring

**Guardrails built in:** No candidate is rejected automatically; the workflow ranks and explains, recruiters decide. Protected characteristics are excluded from scoring by instruction and by stripping fields before the model sees them. Every score carries an evidence quote; unexplained scores are not shown.

**Works with:** Claude, Greenhouse / Lever / Ashby, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/resume-screening-automation/

**Tags:** HR, AI, Approval, Claude, Greenhouse / Lever / Ashby, Google Sheets

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; NYC DCWP — Automated employment decision tools (Local Law 144) — https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page; eCFR — 29 CFR Part 1607, Uniform Guidelines on Employee Selection Procedures — https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607

---

## Candidate Outreach

**Title:** Candidate Outreach (AI + approval step)

**Description:**

Recruiting outreach fails for two reasons: the message is generic, and the follow-up never happens. The workflow takes a sourced list, researches each candidate from their public profile and work, drafts a message that references one specific thing they did, sends it from the recruiter's address, follows up twice on a schedule, and stops the sequence the moment the candidate replies — handing the thread to the recruiter with the research attached. Reply rates double against templated outreach, and the recruiter's time goes to conversations, not first messages.

**How it works**

1. Receive the candidate
2. Research
3. Pick the hook
4. Draft the message
5. Send from the recruiter
6. Follow up twice
7. Stop on reply
8. Measure

**Guardrails built in:** Only public, professional information is used; nothing personal, nothing inferred about protected characteristics. Sending limits: 40 new messages a day per mailbox, spaced, so the recruiter's domain reputation is protected. Every message is sent from a person's address and signed by that person; replies go to them.

**Works with:** Claude, Greenhouse / Lever / Ashby, Gmail / Outlook, Google Sheets

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/candidate-outreach-automation/

**Tags:** HR, AI, Approval, Claude, Greenhouse / Lever / Ashby, Gmail / Outlook

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; NYC DCWP — Automated employment decision tools (Local Law 144) — https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page; Google — Email sender guidelines — https://support.google.com/a/answer/81126

---

## Client Intake

**Title:** Client Intake (AI + approval step)

**Description:**

New enquiries arrive by email, form and phone note, and each one is typed into the matter system, conflict-checked by hand and answered whenever someone gets to it. The workflow classifies each enquiry by matter type, extracts the parties, dates and facts a conflict check needs, checks them against the existing client and adverse-party lists, drafts the engagement letter or the polite decline from the firm's templates, and puts the whole file in front of the responsible person for approval. Nothing is sent unreviewed; everything arrives ready to review.

**How it works**

1. Receive the enquiry
2. Classify the matter
3. Extract the conflict-check facts
4. Run the conflict check
5. Acknowledge
6. Draft the next document
7. Approve
8. Open the matter

**Guardrails built in:** Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically. Conflict results are shown with their evidence; a hit blocks the engagement letter until a person clears it. Enquiry content is processed through an API with no data retention and stored only in the firm's own systems.

**Works with:** Claude, Clio / PracticePanther, Gmail / Outlook, DocuSign / PandaDoc

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/client-intake-automation/

**Tags:** Operations, AI, Approval, Claude, Clio / PracticePanther, Gmail / Outlook

**Sources:** ABA — Model Rule 1.7: Conflict of interest, current clients — https://www.americanbar.org/groups/professional_responsibility/publications/model_rules_of_professional_conduct/rule_1_7_conflict_of_interest_current_clients/; Clio — API documentation — https://docs.developers.clio.com/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Client Reporting

**Title:** Client Reporting (AI + approval step)

**Description:**

The monthly pack is the same job for every client — pull the numbers, compare to budget and last year, spot the three variances worth a sentence, write the sentences, format, send — and it takes the practice a week of month-end. The workflow builds each client's pack from the ledger on the schedule you set, drafts the narrative in the practice's style, flags what needs a partner's eye, and delivers the draft for sign-off. The accountant's time goes to the three sentences that matter, not the twenty that do not.

**How it works**

1. Pull the numbers
2. Check the close
3. Compute the comparisons
4. Find the variances that matter
5. Draft the narrative
6. Assemble the pack
7. Review and sign off
8. Deliver and log

**Guardrails built in:** No pack is drafted on an unclean close; the workflow reports what is open instead. The narrative can only cite movements present in the numbers; causes are stated as 'appears to be' unless the ledger shows them. Every pack is approved by the accountant before it reaches a client.

**Works with:** Claude, Xero / QuickBooks / Sage, Google Docs / Word, Gmail / Outlook

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/client-reporting-automation/

**Tags:** Finance & accounting, AI, Approval, Claude, Xero / QuickBooks / Sage, Google Docs / Word

**Sources:** Xero — Developer documentation — https://developer.xero.com/documentation/; Intuit — QuickBooks Online API, getting started — https://developer.intuit.com/app/developer/qbo/docs/get-started; Google — Docs API overview — https://developers.google.com/workspace/docs/api

---

## Interview Scheduling

**Title:** Interview Scheduling (AI + approval step)

**Description:**

Scheduling an interview is six emails and a calendar puzzle, repeated for every candidate at every stage. The workflow reads the panel's calendars, offers the candidate three slots that work for everyone, books the one they pick, sends invitations with the right links, reminds both sides the day before, and handles 'can we move it' in the same thread without the recruiter touching it. The ATS stage updates itself, and no-shows drop because the candidate had a reminder and an easy way to reschedule.

**How it works**

1. Read the stage
2. Find common slots
3. Offer the slots
4. Book
5. Remind
6. Handle changes
7. Sync the ATS
8. Report

**Guardrails built in:** Panel working hours and blocked times are respected; the workflow never books over a 'focus' block or outside hours. Candidates are never offered a slot less than 24 hours away unless the recruiter allows it for the stage. Every change is written to the same email thread, so the candidate has one conversation, not five.

**Works with:** Claude, Greenhouse / Lever / Ashby, Google Calendar / Outlook, Twilio

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/interview-scheduling-automation/

**Tags:** HR, AI, Approval, Claude, Greenhouse / Lever / Ashby, Google Calendar / Outlook

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; Google — Calendar API: free/busy query — https://developers.google.com/calendar/api/v3/reference/freebusy/query; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging

---

## Lead Nurture

**Title:** Lead Nurture (AI + approval step)

**Description:**

Most nurture is a drip: the same seven emails to everyone who ever enquired. The workflow watches for a reason to write — a new listing that matches what a lead wanted, a rate change that moves their budget, the anniversary of a purchase, a life event they mentioned — drafts a short message that names the reason, sends it in the agent's voice, logs it, and stops the sequence the moment the person replies. Cold leads get two or three well-timed touches a quarter instead of a weekly newsletter, and the agent only hears about the ones who answered.

**How it works**

1. Detect the reason
2. Match leads to the signal
3. Check the guardrails
4. Draft the message
5. Approve or auto-send
6. Send and log
7. Stop on reply
8. Report

**Guardrails built in:** No message without a reason the lead would recognise; the model cannot invent one. Frequency cap: at most one touch per lead per 14 days, at most three per quarter. Anyone in an active conversation or an active CRM stage is excluded automatically.

**Works with:** Claude, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Slack

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/lead-nurture-automation/

**Tags:** Sales, AI, Approval, Claude, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook

**Sources:** Follow Up Boss — API documentation — https://docs.followupboss.com/; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business; FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls

---

## Speed-to-Lead

**Title:** Speed-to-Lead (AI + approval step)

**Description:**

Leads contacted within five minutes convert many times more often than leads contacted the next morning, and almost nobody who works alone can reply within five minutes all day. The workflow takes each new lead from the portal, the site or the CRM, looks up what is already known, qualifies from the enquiry text, drafts a two-sentence reply in the agent's voice with one question, holds it until quiet hours end, sends it from the agent's own address, logs the exchange to the CRM, and texts the agent a three-line summary when the lead answers. A quiet lead gets one nudge; a reply stops the automation and hands the conversation to the agent.

**How it works**

1. Receive the lead
2. Look up the lead in the CRM
3. Qualify
4. Draft the first reply
5. Check quiet hours and consent
6. Send the reply
7. Log and hand off
8. Follow up on silence

**Guardrails built in:** Quiet hours: nothing sent 9 pm–8 am in the lead's time zone; messages queue until morning. One question per message; the second message asks the next question, never both at once. SMS only with a number the lead gave on a form; STOP honoured on the first word and written to the CRM.

**Works with:** Claude, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Twilio

**Setup:** open `Config (edit me)`, add credentials, run in test mode first. Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/speed-to-lead-automation/

**Tags:** Sales, AI, Approval, Claude, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook

**Sources:** Follow Up Boss — API documentation — https://docs.followupboss.com/; FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging

---
