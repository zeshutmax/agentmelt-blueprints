# n8n.io listing copy

One block per template. Paste the title and description into the n8n creator form; the tags are the ones n8n accepts most often.

## Spend Analysis

**File:** `spend-analysis.n8n.json`

**Title:** Classify AP and PO lines with Claude and build a spend cube in Postgres

**Description:**

**Who's it for**
Procurement and finance teams that want category-level spend visibility without a six-figure spend-analytics suite.

**How it works**
Trigger: Runs after accounts payable closes the month.
1. Extract AP and PO lines
2. Normalise suppliers
3. Classify each line
4. Learn from corrections
5. Build the spend cube
6. Detect opportunities
7. Write the opportunity briefs
8. Publish and track
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Postgres / BigQuery, Looker / Power BI / Metabase, Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Swap the category taxonomy in the Config node for your own (UNSPSC or in-house), and point the reporting node at Looker, Power BI or a Google Sheet. Keep the guardrail: Classification below the confidence threshold is reviewed by a person before it enters the cube.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/spend-analysis/

**Tags:** Supply chain & procurement, AI, Postgres / BigQuery, Looker / Power BI / Metabase, Google Sheets

**Sources:** Google Cloud — BigQuery documentation — https://cloud.google.com/bigquery/docs; UNGM — United Nations Standard Products and Services Code (UNSPSC) — https://www.ungm.org/Public/UNSPSC; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Demand Forecasting

**File:** `demand-forecasting.n8n.json`

**Title:** Forecast weekly demand from sales data with Claude and publish to Google Sheets

**Description:**

**Who's it for**
Operations and supply-chain planners who forecast in spreadsheets and want a repeatable weekly run with explanations.

**How it works**
Trigger: Runs Sunday night after the ERP's weekly close.
1. Pull sales history
2. Pull the signals
3. Clean and align
4. Run the forecasting model
5. Score last week's forecast
6. Write forecasts to the planning system
7. Explain the exceptions
8. Publish the weekly review
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus LightGBM / Chronos / TimesFM / TimeGPT, BigQuery / Snowflake / Postgres, Google Sheets / planning tool (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Change the horizon and aggregation level in the Config node; replace the statistical model step with your own endpoint if you already run one. Keep the guardrail: The model forecasts; the agent explains.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/demand-forecasting/

**Tags:** Supply chain & procurement, AI, LightGBM / Chronos / TimesFM / TimeGPT, BigQuery / Snowflake / Postgres, Google Sheets / planning tool

**Sources:** Amazon Science — Chronos forecasting models — https://github.com/amazon-science/chronos-forecasting; LightGBM — documentation — https://lightgbm.readthedocs.io/; Nixtla — TimeGPT documentation — https://docs.nixtla.io/

---

## Employee Onboarding

**File:** `employee-onboarding-automation.n8n.json`

**Title:** Onboard new hires from BambooHR to Slack, Jira and DocuSign with Claude

**Description:**

**Who's it for**
HR and people-ops teams that build every new hire's checklist, accounts and paperwork by hand.

**How it works**
Trigger: BambooHR, Rippling, Workday or Personio announces the moment a candidate's status becomes Hired; for platforms that cannot, the workflow checks the HRIS every hour.
1. Receive the new-hire event
2. Build the checklist for this role
3. Create the tracking board
4. Request accounts and equipment
5. Send documents for signature
6. Schedule the first two weeks
7. Run the welcome sequence
8. Answer policy questions
9. Chase overdue tasks and check in
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus BambooHR / Rippling / Workday, Notion / Jira / Google Sheets, DocuSign / PandaDoc, Slack / Microsoft Teams (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the role-to-checklist mapping in the Config node and add your own account-provisioning nodes (Okta, Google Workspace) after the approval step. Keep the guardrail: The AI agent answers only from the handbook and cites the page; it refuses pay, performance and grievance topics and routes them to HR.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/employee-onboarding-automation/

**Tags:** HR, AI, BambooHR / Rippling / Workday, Notion / Jira / Google Sheets, DocuSign / PandaDoc

**Sources:** BambooHR — API documentation — https://documentation.bamboohr.com/docs; DocuSign — eSignature REST API — https://developers.docusign.com/docs/esign-rest-api/; Slack — API documentation — https://api.slack.com/docs

---

## Automated Code Review

**File:** `automated-code-review.n8n.json`

**Title:** Review GitHub pull requests with Claude and post findings as PR comments

**Description:**

**Who's it for**
Engineering teams that want a consistent first-pass review on every pull request before a human looks.

**How it works**
Trigger: pull_request opened, synchronize and ready_for_review events; draft PRs are skipped unless labelled.
1. Receive the PR event
2. Fetch the diff and context
3. Run static checks
4. Analyse the change
5. Filter to what matters
6. Post inline comments and summary
7. Label and route
8. Learn from resolutions
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus GitHub / GitLab, CI (GitHub Actions, GitLab CI), Linear / Jira (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Tune the severity threshold and the file globs in the Config node; add a Linear or Jira node to open tickets for blocking findings. Keep the guardrail: The workflow never approves or merges; it reviews and labels.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/automated-code-review/

**Tags:** Engineering, AI, GitHub / GitLab, CI (GitHub Actions, GitLab CI), Linear / Jira

**Sources:** GitHub — REST API: pull request reviews — https://docs.github.com/en/rest/pulls/reviews; GitHub — Actions documentation — https://docs.github.com/en/actions; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Expansion Opportunity Detection

**File:** `expansion-opportunity-detection.n8n.json`

**Title:** Detect expansion signals in Amplitude and HubSpot with Claude and alert account owners

**Description:**

**Who's it for**
Customer-success and sales teams that learn about upsell moments too late, if at all.

**How it works**
Trigger: Weekly scoring run; instant triggers for high-value signals like hitting a plan limit or a pricing-page visit by an admin.
1. Pull usage and account data
2. Pull engagement and buying signals
3. Compute the readiness score
4. Match to a play
5. Draft the opener
6. Route to the owner
7. Track outcomes by signal
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Amplitude / Mixpanel / Pendo, HubSpot / Salesforce, Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Adjust the signal weights and the minimum ARR in the Config node; route alerts to Slack or straight into HubSpot tasks. Keep the guardrail: Scores explain themselves — each account shows the signals behind it.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/expansion-opportunity-detection/

**Tags:** Customer success, AI, Amplitude / Mixpanel / Pendo, HubSpot / Salesforce, Google Sheets

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Amplitude — API reference — https://amplitude.com/docs/apis; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Unit Test Generation

**File:** `unit-test-generation.n8n.json`

**Title:** Generate unit tests for GitHub pull requests with Claude and run them in CI

**Description:**

**Who's it for**
Engineering teams with thin test coverage who want tests proposed automatically on every change.

**How it works**
Trigger: PR events on the main repositories; a label can request generation on demand.
1. Receive the PR and diff
2. Find untested changed functions
3. Assemble context
4. Generate tests
5. Run in CI
6. Keep what passes and adds coverage
7. Open the companion PR
8. Learn from reviews
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus GitHub Actions / GitLab CI, Jest / pytest / Go test / JUnit (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the test framework and directories in the Config node; swap the GitHub nodes for GitLab if that is where the code lives. Keep the guardrail: Generated tests are proposed in a separate PR; nothing merges without an engineer's review.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/unit-test-generation/

**Tags:** Engineering, AI, GitHub Actions / GitLab CI, Jest / pytest / Go test / JUnit

**Sources:** GitHub — Actions documentation — https://docs.github.com/en/actions; Jest — Getting started — https://jestjs.io/docs/getting-started; pytest — documentation — https://docs.pytest.org/

---

## Inventory Optimization

**File:** `inventory-optimization.n8n.json`

**Title:** Recommend reorder quantities from ERP stock levels with Claude and approve in Slack

**Description:**

**Who's it for**
Operations teams that decide reorders from a spreadsheet and want the maths and the exceptions done for them.

**How it works**
Trigger: Runs after the demand-forecasting workflow writes new forecasts; a daily run checks stock positions against reorder points.
1. Read forecasts and error
2. Read inventory and open orders
3. Measure supplier lead times
4. Compute safety stock and reorder points
5. Classify SKUs
6. Generate purchase suggestions
7. Explain parameter changes
8. Publish to buyers and the ERP
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus ERP / WMS (NetSuite, SAP B1, Cin7, Fishbowl), Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put your service levels and lead times in the Config node; connect the ERP node to NetSuite, SAP B1, Cin7 or Fishbowl. Keep the guardrail: Draft POs only — a buyer approves before anything is sent to a supplier.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/inventory-optimization/

**Tags:** Supply chain & procurement, AI, ERP / WMS (NetSuite, SAP B1, Cin7, Fishbowl), Google Sheets

**Sources:** Oracle — NetSuite documentation — https://docs.oracle.com/en/cloud/saas/netsuite/index.html; ASCM — supply chain standards and body of knowledge — https://www.ascm.org/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Social Listening

**File:** `social-listening-response.n8n.json`

**Title:** Monitor brand mentions with Claude and draft replies for approval in Slack

**Description:**

**Who's it for**
Marketing and support teams that answer social mentions by hand and miss the ones that matter.

**How it works**
Trigger: Hourly pulls from each source's API or a listening provider; high-severity classifications trigger immediate alerts.
1. Collect mentions
2. De-duplicate and filter
3. Classify intent and sentiment
4. Draft the response
5. Route by category
6. Approve and post
7. Log everything
8. Weekly listening report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Brand24 / Mention / platform APIs, Slack, HubSpot + Zendesk (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Change the sources and the severity rules in the Config node; add a HubSpot or Zendesk node to open a ticket for complaints. Keep the guardrail: Nothing is posted publicly without human approval; the agent drafts.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/social-listening-response/

**Tags:** Marketing, AI, Approval, Brand24 / Mention / platform APIs, Slack, HubSpot + Zendesk

**Sources:** Meta — Graph API — https://developers.facebook.com/docs/graph-api/; X — Developer platform overview — https://docs.x.com/overview; Slack — API documentation — https://api.slack.com/docs

---

## Employee Offboarding

**File:** `employee-offboarding-automation.n8n.json`

**Title:** Offboard leavers from the HRIS to Okta, Jira and Google Workspace with Claude

**Description:**

**Who's it for**
IT and HR teams that revoke access and collect equipment from a checklist that is never quite complete.

**How it works**
Trigger: The HRIS fires when an employment end date is set.
1. Receive the termination record
2. Assemble the leaver's access map
3. Open revocation tickets with deadlines
4. Schedule equipment return
5. Generate the knowledge-transfer checklist
6. Hand off to finance and payroll
7. Send the exit survey
8. Confirm closure
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Okta / Entra ID / Google Workspace, Jira Service Management / ServiceNow, Typeform / Google Forms (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the access-revocation order and the exit-survey questions in the Config node; add your own SaaS admin APIs as extra revocation nodes. Keep the guardrail: The workflow requests revocation; IT executes it.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/employee-offboarding-automation/

**Tags:** HR, AI, Okta / Entra ID / Google Workspace, Jira Service Management / ServiceNow, Typeform / Google Forms

**Sources:** Okta — API reference — https://developer.okta.com/docs/reference/; Google — Workspace Admin SDK — https://developers.google.com/workspace/admin; Atlassian — Jira Service Management Cloud REST API — https://developer.atlassian.com/cloud/jira/service-desk/rest/

---

## Automated Insurance Underwriting Intake

**File:** `insurance-underwriting-intake.n8n.json`

**Title:** Extract broker submissions from Gmail with Claude and triage them for underwriters

**Description:**

**Who's it for**
Commercial underwriting teams that key submissions from email into the workbench by hand.

**How it works**
Trigger: New emails to submissions@ with attachments; portal submissions arrive as they are filed.
1. Capture and classify attachments
2. Extract application data
3. Check completeness
4. Pull third-party data
5. Apply appetite rules
6. Indicative rating
7. Assemble the file and questions
8. Queue and track
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Policy admin / workbench (Duck Creek, Guidewire, Applied, or in-house), Third-party data providers, Outlook / Gmail (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Define the appetite rules and the required-fields list in the Config node; point the write-back node at your policy admin system. Keep the guardrail: No binding decisions are automated; the workflow triages and prepares.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/insurance-underwriting-intake/

**Tags:** Insurance, AI, Policy admin / workbench (Duck Creek, Guidewire, Applied, or in-house), Third-party data providers, Outlook / Gmail

**Sources:** ACORD — Standards and architecture — https://www.acord.org/standards-architecture; NAIC — model laws and regulations — https://content.naic.org/model-laws; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Financial Reconciliation

**File:** `financial-reconciliation-automation.n8n.json`

**Title:** Reconcile Stripe payouts against NetSuite with Claude and flag exceptions in Slack

**Description:**

**Who's it for**
Finance teams that match bank feeds, processor payouts and the ledger in spreadsheets every morning.

**How it works**
Trigger: Daily run at 6am after bank and processor feeds update; on-demand run before close.
1. Pull the three sides
2. Match deterministically
3. Classify the breaks
4. Explain the unknowns
5. Route for approval
6. Post approved entries
7. Maintain the reconciliation file
8. Close-readiness report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus NetSuite / Xero / QuickBooks, Stripe / Adyen + Plaid (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the matching tolerances and the exception owners in the Config node; swap NetSuite for Xero or QuickBooks. Keep the guardrail: Nothing posts to the ledger without an accountant's approval; auto-matching only marks, it does not create entries.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/financial-reconciliation-automation/

**Tags:** Finance & accounting, AI, Approval, NetSuite / Xero / QuickBooks, Stripe / Adyen + Plaid

**Sources:** Stripe — Balance transactions API — https://docs.stripe.com/api/balance_transactions; Plaid — Transactions — https://plaid.com/docs/transactions/; Xero — Developer documentation — https://developer.xero.com/documentation/

---

## Email Triage

**File:** `email-triage-automation.n8n.json`

**Title:** Triage a shared Gmail inbox with Claude and create tasks in Asana and Slack

**Description:**

**Who's it for**
Operations teams and assistants who sort a shared inbox by hand and lose requests in the pile.

**How it works**
Trigger: Polls the mailbox every minute for new messages via Gmail or Microsoft Outlook triggers; threads are handled as a unit.
1. Receive and de-duplicate
2. Classify
3. Fetch context
4. Extract tasks and dates
5. Draft routine replies
6. Route
7. Approve and send
8. Daily digest
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Gmail / Outlook, Asana / Linear / Notion, Slack (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the categories and the routing rules in the Config node; replace Asana with Linear or Notion. Keep the guardrail: Drafts require approval by default; auto-send is enabled per category by the inbox owner and logged.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/email-triage-automation/

**Tags:** Operations, AI, Approval, Gmail / Outlook, Asana / Linear / Notion, Slack

**Sources:** Google — Gmail API guides — https://developers.google.com/workspace/gmail/api/guides; Microsoft Graph — Outlook mail API overview — https://learn.microsoft.com/en-us/graph/api/resources/mail-api-overview; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Support Ticket Deflection

**File:** `support-ticket-deflection.n8n.json`

**Title:** Answer Zendesk tickets from your help centre with Claude and escalate the rest

**Description:**

**Who's it for**
Support teams that answer the same twenty questions every day and want them handled before an agent opens the ticket.

**How it works**
Trigger: Zendesk, Intercom, Freshdesk, Help Scout or HubSpot posts each new conversation.
1. Receive the ticket
2. Fetch customer context
3. Classify and prioritise
4. Retrieve knowledge
5. Draft the answer with a confidence score
6. Resolve or route
7. Send and log
8. Learn from reopens
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Zendesk / Intercom / Freshdesk, Pinecone / Supabase / Qdrant, HubSpot / Stripe (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Point the vector store at your own help-centre export; set the confidence threshold and the escalation tags in the Config node. Keep the guardrail: The agent answers only from your knowledge base and cites the source; no general-knowledge answers.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/support-ticket-deflection/

**Tags:** Customer support, AI, Zendesk / Intercom / Freshdesk, Pinecone / Supabase / Qdrant, HubSpot / Stripe

**Sources:** Zendesk — API reference — https://developer.zendesk.com/api-reference/; Intercom — Developer docs — https://developers.intercom.com/docs; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Document & Proposal Generation

**File:** `document-generation-automation.n8n.json`

**Title:** Generate proposals from HubSpot deals with Claude in Google Docs

**Description:**

**Who's it for**
Sales and operations teams that assemble proposals and statements of work from the last one, every time.

**How it works**
Trigger: A 'new proposal' form, a deal moving to the proposal stage in the CRM, or an RFP document uploaded to a folder starts the run.
1. Receive the request
2. Pull the client record
3. Parse the RFP or brief
4. Retrieve past answers and case material
5. Draft each section
6. Consistency and compliance check
7. Produce the document
8. Route for review and learn
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Pinecone / Supabase, Google Docs / Microsoft Word, HubSpot / Salesforce (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Store your section templates in the Config node; swap Google Docs for Microsoft Word and HubSpot for Salesforce. Keep the guardrail: Every reused answer is sourced to the document it came from; the writer can see what was adapted.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/document-generation-automation/

**Tags:** Operations, AI, Approval, Pinecone / Supabase, Google Docs / Microsoft Word, HubSpot / Salesforce

**Sources:** Google — Docs API overview — https://developers.google.com/workspace/docs/api; Microsoft Graph — overview — https://learn.microsoft.com/en-us/graph/overview; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview

---

## Subscription & Dunning

**File:** `subscription-dunning-automation.n8n.json`

**Title:** Recover failed Stripe payments with Claude-written emails and Twilio SMS

**Description:**

**Who's it for**
SaaS finance and growth teams losing revenue to expired cards and silent cancellations.

**How it works**
Trigger: invoice.payment_failed, customer.subscription.updated, cancellation requested, trial ending, card expiring soon.
1. Receive the billing event
2. Choose the retry strategy
3. Draft the dunning message
4. Send across the sequence
5. Handle plan changes and pauses
6. Cancellation intercept
7. Alert finance and the owner
8. Weekly recovery report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Stripe / Chargebee / Recurly, Gmail + Twilio + Intercom, Slack + Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Change the retry schedule and the tone rules in the Config node; add Intercom or Slack for the high-value accounts. Keep the guardrail: Retry schedules respect card-network rules and the provider's limits.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/subscription-dunning-automation/

**Tags:** Finance & accounting, AI, Stripe / Chargebee / Recurly, Gmail + Twilio + Intercom, Slack + Google Sheets

**Sources:** Stripe — Smart Retries — https://docs.stripe.com/billing/revenue-recovery/smart-retries; Chargebee — Dunning — https://www.chargebee.com/docs/2.0/dunning.html; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Logistics Optimization

**File:** `logistics-optimization.n8n.json`

**Title:** Pick the cheapest carrier for shipped orders with EasyPost and Claude

**Description:**

**Who's it for**
E-commerce operations teams that choose carriers by habit and answer 'where is my order' by hand.

**How it works**
Trigger: The WMS or e-commerce platform (Shopify, NetSuite, ShipStation) posts when a shipment is packed.
1. Receive the shipment
2. Rate across carriers
3. Select the service
4. Book and label
5. Track in flight
6. Detect and explain delays
7. Notify and escalate
8. Audit carrier invoices
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus EasyPost / Shippo / carrier APIs, Gmail / Zendesk, Google Sheets / Postgres (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put your carrier accounts and service rules in the Config node; connect the order webhook to Shopify, NetSuite or ShipStation. Keep the guardrail: Customer messages for orders above a value threshold are approved by a person before sending.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/logistics-optimization/

**Tags:** Supply chain & procurement, AI, EasyPost / Shippo / carrier APIs, Gmail / Zendesk, Google Sheets / Postgres

**Sources:** EasyPost — API documentation — https://docs.easypost.com/; Shippo — API documentation — https://docs.goshippo.com/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Proactive Customer Outreach

**File:** `proactive-customer-outreach.n8n.json`

**Title:** Reach out to at-risk customers from Stripe and Segment events with Claude

**Description:**

**Who's it for**
Support and success teams that hear about problems only when the customer complains or leaves.

**How it works**
Trigger: Stripe/Chargebee (payment failed, trial ending), product analytics (Segment, Mixpanel, PostHog events), error monitoring (Sentry), shipping (tracking exceptions).
1. Receive or detect the signal
2. Load the customer's context
3. Decide whether to reach out
4. Draft the message
5. Approve if sensitive
6. Send on the right channel
7. Log and watch the response
8. Report what it prevented
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Stripe / Chargebee, Segment / PostHog / Mixpanel, HubSpot / Intercom (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Define the trigger events and the message templates in the Config node; send through HubSpot, Intercom or Gmail. Keep the guardrail: Frequency cap: one proactive message per customer per week across all scenarios.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/proactive-customer-outreach/

**Tags:** Customer support, AI, Approval, Stripe / Chargebee, Segment / PostHog / Mixpanel, HubSpot / Intercom

**Sources:** Stripe — Webhooks — https://docs.stripe.com/webhooks; Segment — Documentation — https://segment.com/docs/; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Customer Onboarding

**File:** `customer-onboarding-automation.n8n.json`

**Title:** Guide new signups to activation with Claude using Segment and HubSpot

**Description:**

**Who's it for**
Product and success teams whose new customers stall between signup and first value.

**How it works**
Trigger: The product or billing system posts new signups; a daily Schedule Trigger evaluates every account still in onboarding against milestone deadlines.
1. Register the new account
2. Track milestones from product events
3. Detect stalls
4. Send the right nudge
5. Answer setup questions
6. Escalate to a person
7. Celebrate activation and hand over
8. Report the funnel
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Segment / Mixpanel / PostHog, HubSpot / Intercom (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the milestones and the nudge timing in the Config node; replace Segment with Mixpanel or PostHog. Keep the guardrail: Nudges are sent only on stalls, with a cap of one per milestone; no message for customers making progress.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-onboarding-automation/

**Tags:** Customer success, AI, Segment / Mixpanel / PostHog, HubSpot / Intercom

**Sources:** Segment — Documentation — https://segment.com/docs/; Intercom — Developer docs — https://developers.intercom.com/docs; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview

---

## Supplier Risk Monitoring

**File:** `supplier-risk-monitoring.n8n.json`

**Title:** Score supplier risk from news and credit data with Claude and report in Slack

**Description:**

**Who's it for**
Procurement teams that learn about a supplier's trouble from a missed delivery.

**How it works**
Trigger: News and delivery data refresh daily; financial and ESG data refresh weekly; the composite score is recomputed weekly and on any high-severity signal.
1. Load the supplier portfolio
2. Pull financial signals
3. Pull news and events
4. Measure delivery performance
5. Classify and weight signals
6. Compute the composite score
7. Draft the risk brief
8. Alert and track
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus D&B / Creditsafe / Coface, News API / GDELT, Slack + Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the risk weights and the watchlist in the Config node; add D&B, Creditsafe or your own data provider as sources. Keep the guardrail: Scores are explainable: every alert lists the signals and weights that produced it.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/supplier-risk-monitoring/

**Tags:** Supply chain & procurement, AI, D&B / Creditsafe / Coface, News API / GDELT, Slack + Google Sheets

**Sources:** GDELT Project — global news event data — https://www.gdeltproject.org/; Dun & Bradstreet — Direct+ API documentation — https://directplus.documentation.dnb.com/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Prior Authorization

**File:** `prior-authorization-automation.n8n.json`

**Title:** Prepare prior authorization requests from EHR orders with Claude

**Description:**

**Who's it for**
Clinic and practice staff who spend hours a day on payer portals and phone queues.

**How it works**
Trigger: New orders and referrals from the EHR (via FHIR, HL7 or a daily export) are checked against payer rules; status polling runs twice daily.
1. Detect auth requirement
2. Gather documentation
3. Check completeness against criteria
4. Draft the medical-necessity summary
5. Submit
6. Track status
7. Draft appeals
8. Report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus EHR (Epic, athenahealth, eClinicalWorks…), Availity / payer portals (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Keep the payer rules in the Config node; this template assumes self-hosted n8n and a model under a BAA — set both before running on patient data. Keep the guardrail: Every submission and appeal is reviewed and signed by a clinician or authorised staff member; nothing is sent automatically.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/prior-authorization-automation/

**Tags:** Operations, AI, EHR (Epic, athenahealth, eClinicalWorks…), Availity / payer portals

**Sources:** CMS — Interoperability and Prior Authorization Final Rule (CMS-0057-F) — https://www.cms.gov/priorities/key-initiatives/burden-reduction/interoperability/policies-and-regulations/cms-interoperability-and-prior-authorization-final-rule-cms-0057-f; HHS — HIPAA for professionals — https://www.hhs.gov/hipaa/for-professionals/index.html; Availity — payer connectivity — https://www.availity.com/

---

## Customer Health Scoring

**File:** `customer-health-scoring.n8n.json`

**Title:** Score customer health from Mixpanel and Zendesk data with Claude into HubSpot

**Description:**

**Who's it for**
Customer-success teams that manage renewals from gut feel and a quarterly spreadsheet.

**How it works**
Trigger: Weekly scoring; immediate re-score on high-severity events such as a champion's user being deactivated, a payment failure, or a very negative ticket.
1. Collect the components
2. Score each component
3. Analyse ticket sentiment
4. Compute score and trend
5. Detect drops and thresholds
6. Draft the intervention
7. Alert the owner and update the CRM
8. Calibrate quarterly
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Mixpanel / Amplitude / PostHog, Zendesk / Intercom, HubSpot / Salesforce (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Adjust the score inputs and thresholds in the Config node; swap Mixpanel for Amplitude and HubSpot for Salesforce. Keep the guardrail: Scores show their components; no black-box number.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-health-scoring/

**Tags:** Customer success, AI, Mixpanel / Amplitude / PostHog, Zendesk / Intercom, HubSpot / Salesforce

**Sources:** Mixpanel — API reference — https://developer.mixpanel.com/reference/overview; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Zendesk — API reference — https://developer.zendesk.com/api-reference/

---

## Insurance Claims Intake

**File:** `insurance-claims-intake.n8n.json`

**Title:** Intake insurance claims from email and portal submissions with Claude

**Description:**

**Who's it for**
Claims teams that re-key first notice of loss from emails, forms and call notes.

**How it works**
Trigger: Emails to claims@, portal and app submissions as they happen, and call-centre transcripts from the telephony platform.
1. Capture the notice
2. Extract the facts
3. Verify policy and coverage
4. Triage severity and complexity
5. Screen fraud indicators
6. Route
7. Acknowledge the claimant
8. Create the file and assign
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Claims system (Guidewire ClaimCenter, Duck Creek, Snapsheet, in-house), Policy admin, Telephony (Five9, Talkdesk) (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Define the claim types and the required documents in the Config node; point the write-back at your claims system. Keep the guardrail: Coverage determinations and claim decisions are made by adjusters; the workflow verifies and summarises.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/insurance-claims-intake/

**Tags:** Insurance, AI, Claims system (Guidewire ClaimCenter, Duck Creek, Snapsheet, in-house), Policy admin, Telephony (Five9, Talkdesk)

**Sources:** ACORD — Standards and architecture — https://www.acord.org/standards-architecture; NAIC — model laws and regulations — https://content.naic.org/model-laws; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Payroll

**File:** `payroll-automation.n8n.json`

**Title:** Prepare payroll from Gusto time data with Claude and approve in Slack

**Description:**

**Who's it for**
Small HR and finance teams that run payroll checks by hand every period and still find errors after the fact.

**How it works**
Trigger: Runs on the cut-off date each period, plus a preview run three days earlier so managers can fix missing approvals.
1. Collect period inputs
2. Normalise into one employee ledger
3. Validate against policy
4. Anomaly review
5. Send the exceptions report
6. Wait for approval
7. Push the run to the provider
8. Reconcile after the run
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Gusto / ADP / Rippling / Deel, Slack, Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the pay-period rules and the anomaly thresholds in the Config node; connect Gusto, ADP, Rippling or Deel. Keep the guardrail: The workflow never submits without an explicit human approval; the Wait node is the control.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/payroll-automation/

**Tags:** HR, AI, Approval, Gusto / ADP / Rippling / Deel, Slack, Google Sheets

**Sources:** Gusto — API documentation — https://docs.gusto.com/; IRS — Publication 15, Employer's Tax Guide — https://www.irs.gov/publications/p15; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Automated Security Alert Triage

**File:** `security-alert-triage.n8n.json`

**Title:** Triage SIEM alerts with Claude, enrich with VirusTotal and page on-call via Slack

**Description:**

**Who's it for**
Small security teams drowning in alerts from Splunk, Sentinel or CrowdStrike.

**How it works**
Trigger: Splunk, Sentinel, Elastic, CrowdStrike, SentinelOne, Wazuh or Google SecOps posts new alerts; tools that cannot push alerts are polled instead.
1. Receive and normalise the alert
2. Enrich entities
3. Correlate with recent activity
4. Score and classify
5. Analyst-style assessment
6. Auto-close or queue
7. Notify and escalate
8. Weekly tuning report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Splunk / Sentinel / CrowdStrike, VirusTotal / AbuseIPDB / MISP, Slack / PagerDuty (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the severity rules and the enrichment sources in the Config node; add PagerDuty for critical findings. Keep the guardrail: The workflow never takes containment actions (isolate host, disable user) on its own; it recommends and a human executes, or a separate approved playbook runs with explicit authorisation.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/security-alert-triage/

**Tags:** Security & IT, AI, Splunk / Sentinel / CrowdStrike, VirusTotal / AbuseIPDB / MISP, Slack / PagerDuty

**Sources:** MITRE ATT&CK — https://attack.mitre.org/; NIST SP 800-61 Rev. 3 — Incident response recommendations — https://csrc.nist.gov/pubs/sp/800/61/r3/final; VirusTotal — API reference — https://docs.virustotal.com/reference/overview

---

## Competitor Monitoring

**File:** `competitor-monitoring.n8n.json`

**Title:** Track competitor pages with Firecrawl and Claude and post a weekly brief to Notion

**Description:**

**Who's it for**
Marketing and product teams that check competitor sites by hand, or not at all.

**How it works**
Trigger: Daily snapshots of monitored pages and feeds; the brief compiles weekly, with instant alerts for pricing changes.
1. Snapshot monitored pages
2. Collect feeds
3. Detect material changes
4. Classify and assess
5. Instant alerts for pricing
6. Write the weekly brief
7. Update battle cards
8. Distribute and log
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Browserless / Firecrawl, Notion + Slack (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
List the pages and the change types you care about in the Config node; send the brief to Slack instead of Notion if you prefer. Keep the guardrail: Only public sources are monitored; no login walls, no scraping in violation of terms.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/competitor-monitoring/

**Tags:** Marketing, AI, Browserless / Firecrawl, Notion + Slack

**Sources:** Firecrawl — documentation — https://docs.firecrawl.dev/introduction; IETF RFC 9309 — Robots Exclusion Protocol — https://www.rfc-editor.org/rfc/rfc9309; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Content Repurposing

**File:** `content-repurposing-automation.n8n.json`

**Title:** Turn podcast episodes from Google Drive into posts with Deepgram and Claude

**Description:**

**Who's it for**
Content teams that publish one long piece and never get to the ten short ones it could become.

**How it works**
Trigger: A recording dropped in the 'episodes' folder, a new item in the podcast RSS feed, or a new Riverside/Zoom recording starts the run.
1. Transcribe
2. Extract structure
3. Draft the long-form
4. Draft the short-form
5. Clip list for the editor
6. Review board
7. Schedule approved assets
8. Report performance back
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Deepgram / AssemblyAI, Notion, Buffer / Hootsuite / CMS (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the output formats and your voice rules in the Config node; publish through Buffer, Hootsuite or your CMS. Keep the guardrail: Nothing publishes without approval on the review board.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/content-repurposing-automation/

**Tags:** Marketing, AI, Approval, Deepgram / AssemblyAI, Notion, Buffer / Hootsuite / CMS

**Sources:** Deepgram — documentation — https://developers.deepgram.com/home; AssemblyAI — documentation — https://www.assemblyai.com/docs; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Customer Win-Back

**File:** `customer-win-back-automation.n8n.json`

**Title:** Win back churned customers from Stripe and HubSpot with Claude-written emails

**Description:**

**Who's it for**
SaaS growth teams that never contact churned accounts again, even when the reason they left is fixed.

**How it works**
Trigger: Weekly scan of churned accounts against triggers; a release-notes event or a manual trigger when a feature ships; seasonal calendar for seasonal businesses.
1. Build the churned segment
2. Classify the reason
3. Match triggers to segments
4. Draft the message
5. Approve high-value sends
6. Send and route replies
7. Track reactivation
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Stripe / Chargebee + HubSpot, Gmail / Customer.io (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Define the win-back triggers and the offer rules in the Config node; send through Customer.io or Gmail. Keep the guardrail: Excluded segments (business closed, requested no contact, poor fit) never receive win-back messages.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-win-back-automation/

**Tags:** Customer success, AI, Approval, Stripe / Chargebee + HubSpot, Gmail / Customer.io

**Sources:** Stripe — Subscriptions API — https://docs.stripe.com/api/subscriptions; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business

---

## Appointment Reminders

**File:** `appointment-reminders-automation.n8n.json`

**Title:** Send appointment reminders and handle replies with Twilio and Claude

**Description:**

**Who's it for**
Clinics, salons and service businesses losing revenue to no-shows.

**How it works**
Trigger: Hourly scan of upcoming appointments in the scheduling system; instant triggers for new bookings, cancellations and inbound SMS replies.
1. Pull upcoming appointments
2. Decide the cadence and channel
3. Send the reminder
4. Understand replies
5. Book reschedules from real availability
6. Fill cancellations from the waitlist
7. Update the record and the desk
8. Report weekly
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Twilio, Scheduling system (Dentrix, Cliniko, Acuity, Calendly…) (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the reminder timing and the reschedule rules in the Config node; connect your scheduling system (Acuity, Calendly, Cliniko…). Keep the guardrail: Only patients with recorded consent for SMS or automated calls are messaged; opt-out words stop the sequence immediately.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/appointment-reminders-automation/

**Tags:** Operations, AI, Twilio, Scheduling system (Dentrix, Cliniko, Acuity, Calendly…)

**Sources:** FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## KYC/AML Monitoring

**File:** `kyc-aml-monitoring.n8n.json`

**Title:** Screen customers against sanctions lists with ComplyAdvantage and Claude

**Description:**

**Who's it for**
Compliance teams at fintechs and payment companies that screen and re-screen by hand.

**How it works**
Trigger: New customers screened at onboarding; the full book re-screened daily against list updates; transaction events evaluated in near real time.
1. Screen the customer
2. Pre-assess matches
3. Evaluate transactions
4. Build the case
5. Route to the analyst
6. Record the decision
7. Continuous re-screening
8. Regulatory reporting
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus ComplyAdvantage / Dow Jones / OpenSanctions, Postgres (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the screening sources and the match thresholds in the Config node; this template assumes self-hosted n8n and a Postgres audit table. Keep the guardrail: No case is closed without an analyst's recorded decision; the agent drafts, never decides.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/kyc-aml-monitoring/

**Tags:** Finance & accounting, AI, Approval, ComplyAdvantage / Dow Jones / OpenSanctions, Postgres

**Sources:** FATF — The FATF Recommendations — https://www.fatf-gafi.org/en/publications/Fatfrecommendations/Fatf-recommendations.html; OpenSanctions — documentation — https://www.opensanctions.org/docs/; FinCEN — Financial Crimes Enforcement Network — https://www.fincen.gov/

---

## Inbound Lead Qualification

**File:** `inbound-lead-qualification.n8n.json`

**Title:** Qualify inbound leads from HubSpot forms with Clay and Claude and book meetings

**Description:**

**Who's it for**
Sales teams that reply to demo requests hours later and qualify by hand.

**How it works**
Trigger: Any form submission or demo request posts to the workflow; chat-widget conversations and inbound emails to sales@ use the same path.
1. Receive the submission
2. Enrich
3. Score against the ICP
4. Read the message
5. Route
6. Notify the rep with context
7. Update the CRM
8. Follow up on silence
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Clay / Apollo / Clearbit, HubSpot / Salesforce, Slack + Calendly (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the qualification criteria and the routing rules in the Config node; swap Clay for Apollo or Clearbit. Keep the guardrail: The first reply commits to nothing: no pricing, no availability, no promises — it acknowledges and asks.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/inbound-lead-qualification/

**Tags:** Sales, AI, Clay / Apollo / Clearbit, HubSpot / Salesforce, Slack + Calendly

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Calendly — API documentation — https://developer.calendly.com/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Data Migration

**File:** `data-migration-automation.n8n.json`

**Title:** Migrate records between systems with Claude-assisted mapping and validation

**Description:**

**Who's it for**
Ops and engineering teams moving data from one CRM, help desk or database to another without a migration vendor.

**How it works**
Trigger: Each phase — profile, map, validate, dry-run, cutover — starts on an explicit click; no phase runs unattended.
1. Profile the source
2. Propose the mapping
3. Confirm the mapping
4. Apply transformations
5. Validate
6. Dry run
7. Cut over in batches
8. Reconcile and hand over
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Postgres / BigQuery, Target APIs (HubSpot, Salesforce, Zendesk…) (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put the source and target schemas in the Config node; run each phase (profile, map, validate, dry-run, cutover) by hand from the manual trigger. Keep the guardrail: No phase runs without an explicit trigger; cutover requires a dry run that passed.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/data-migration-automation/

**Tags:** Engineering, AI, Approval, Postgres / BigQuery, Target APIs (HubSpot, Salesforce, Zendesk…)

**Sources:** PostgreSQL — documentation — https://www.postgresql.org/docs/; HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Cold Outbound

**File:** `cold-outbound-sequencing.n8n.json`

**Title:** Personalize cold outbound from Apollo lists with Claude and send via Instantly

**Description:**

**Who's it for**
Sales teams that send templated sequences and get templated results.

**How it works**
Trigger: A daily run selects the next batch from the list; the sending tool reports replies, bounces and unsubscribes in real time.
1. Build the batch
2. Research each account
3. Write the first line and email
4. Quality gate
5. Load into the sequencer
6. Detect replies and classify
7. Hand to a rep
8. Report by angle and segment
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Apollo / Clay, Instantly / Smartlead / Lemlist, HubSpot / Salesforce (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the daily batch size and the personalization rules in the Config node; swap Instantly for Smartlead or Lemlist. Keep the guardrail: Daily volume per mailbox is capped and warm-up is respected; the workflow never sends outside the sequencer's limits.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/cold-outbound-sequencing/

**Tags:** Sales, AI, Approval, Apollo / Clay, Instantly / Smartlead / Lemlist, HubSpot / Salesforce

**Sources:** Google — Email sender guidelines — https://support.google.com/a/answer/81126; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business; Apollo.io — API documentation — https://docs.apollo.io/

---

## Weekly Reporting

**File:** `weekly-reporting-automation.n8n.json`

**Title:** Compile a weekly report from BigQuery with Claude into Google Docs and Slack

**Description:**

**Who's it for**
Operations leads who spend Monday morning assembling the same report from five dashboards.

**How it works**
Trigger: Weekly run after data sources have closed the week; on-demand run for ad-hoc periods.
1. Run the metric queries
2. Assemble the metrics table
3. Pull context
4. Draft the narrative
5. Render the report
6. Approve
7. Distribute
8. Maintain the catalogue
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus BigQuery / Snowflake / Postgres, Google Docs + Slack (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
List the metrics and their queries in the Config node; replace BigQuery with Snowflake or Postgres. Keep the guardrail: Every number in the narrative must appear in the metrics table; the agent cannot introduce figures.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/weekly-reporting-automation/

**Tags:** Operations, AI, Approval, BigQuery / Snowflake / Postgres, Google Docs + Slack

**Sources:** Google Cloud — BigQuery documentation — https://cloud.google.com/bigquery/docs; Google — Docs API overview — https://developers.google.com/workspace/docs/api; Slack — API documentation — https://api.slack.com/docs

---

## Real Estate Listing

**File:** `listing-description-automation.n8n.json`

**Title:** Write real estate listing descriptions with Claude from Follow Up Boss

**Description:**

**Who's it for**
Real-estate agents and teams that write every listing description and social post from scratch.

**How it works**
Trigger: Follow Up Boss, kvCORE, a Google Form, or a change in the MLS feed for the agent's listings starts the run.
1. Receive the listing
2. Describe the photos
3. Draft the MLS description
4. Draft the derivatives
5. Compliance and brand check
6. Review and approve
7. Publish
8. Track
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Follow Up Boss / kvCORE, Mailchimp / Constant Contact, Buffer / Meta API (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put your voice rules and fair-housing checklist in the Config node; publish through Mailchimp, Buffer or the Meta API. Keep the guardrail: Fair-housing language check runs on every asset before review; flagged copy cannot be approved without an edit.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/listing-description-automation/

**Tags:** Marketing, AI, Approval, Follow Up Boss / kvCORE, Mailchimp / Constant Contact, Buffer / Meta API

**Sources:** U.S. Department of Justice — The Fair Housing Act — https://www.justice.gov/crt/fair-housing-act-1; Follow Up Boss — API documentation — https://docs.followupboss.com/; Meta — Graph API — https://developers.facebook.com/docs/graph-api/

---

## IT Helpdesk

**File:** `it-helpdesk-automation.n8n.json`

**Title:** Resolve IT requests from Slack with Claude, Okta and Jira Service Management

**Description:**

**Who's it for**
Small IT teams that answer password resets and access requests all day.

**How it works**
Trigger: Messages to the IT bot or #it-help channel, and new tickets in Jira Service Management, Freshservice or ServiceNow.
1. Receive the request
2. Classify the request
3. Answer from the knowledge base
4. Self-service actions with approval
5. Execute through the systems
6. Create or update the ticket
7. Route unresolved requests
8. Improve the knowledge base
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Okta / Entra ID / Google Workspace, Jamf / Intune, Jira Service Management / Freshservice (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Edit the request types and the self-service rules in the Config node; add Jamf or Intune for device actions. Keep the guardrail: Identity is taken from the chat platform's SSO, never from the message; sensitive actions require a fresh MFA step.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/it-helpdesk-automation/

**Tags:** Security & IT, AI, Approval, Okta / Entra ID / Google Workspace, Jamf / Intune, Jira Service Management / Freshservice

**Sources:** Okta — API reference — https://developer.okta.com/docs/reference/; Microsoft Graph — overview — https://learn.microsoft.com/en-us/graph/overview; Jamf — developer portal — https://developer.jamf.com/

---

## Purchase Order

**File:** `purchase-order-automation.n8n.json`

**Title:** Route purchase requests from Slack to approval and create POs in NetSuite with Claude

**Description:**

**Who's it for**
Finance and operations teams that approve purchases in email threads and lose track of them.

**How it works**
Trigger: A purchase-request form (or a Slack slash command) starts the workflow; email requests to procurement@ are parsed the same way.
1. Receive the request
2. Normalise and complete
3. Check budget and policy
4. Route approvals
5. Create the PO
6. Send to the supplier
7. Track receipt
8. Report committed spend
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus NetSuite / Dynamics / Xero, Slack (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the approval thresholds and the approver map in the Config node; swap NetSuite for Dynamics or Xero. Keep the guardrail: No PO is created without the approvals the policy matrix requires; the workflow enforces, it does not decide.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/purchase-order-automation/

**Tags:** Supply chain & procurement, AI, Approval, NetSuite / Dynamics / Xero, Slack

**Sources:** Oracle — NetSuite documentation — https://docs.oracle.com/en/cloud/saas/netsuite/index.html; Xero — Developer documentation — https://developer.xero.com/documentation/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Invoice Processing

**File:** `invoice-processing-automation.n8n.json`

**Title:** Extract supplier invoices from Gmail with Claude and post them to Xero for approval

**Description:**

**Who's it for**
Accountants, bookkeepers and AP teams that key invoices in by hand and chase approvals by email.

**How it works**
Trigger: New attachments to ap@ start the run; supplier portals and scanned batches are polled hourly.
1. Capture the invoice
2. Extract fields
3. Validate and detect duplicates
4. Match to PO and receipt
5. Route exceptions and approvals
6. Approve on the phone
7. Post to the ERP
8. Supplier status replies
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus NetSuite / Xero / QuickBooks / Sage, Slack / email, Google Drive / S3 (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the coding rules and the approval thresholds in the Config node; swap Xero for QuickBooks, NetSuite or Sage. Keep the guardrail: Bank-detail changes never post automatically; they trigger a verification call with the supplier.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/invoice-processing-automation/

**Tags:** Finance & accounting, AI, Approval, NetSuite / Xero / QuickBooks / Sage, Slack / email, Google Drive / S3

**Sources:** Xero — Developer documentation — https://developer.xero.com/documentation/; Intuit — QuickBooks Online API, getting started — https://developer.intuit.com/app/developer/qbo/docs/get-started; FBI IC3 — Business email compromise — https://www.ic3.gov/CrimeInfo/BEC

---

## Meeting Prep

**File:** `meeting-prep-research.n8n.json`

**Title:** Prepare meeting briefs from Google Calendar with Claude, HubSpot and Clay

**Description:**

**Who's it for**
Sales reps and founders who walk into external meetings with two minutes of research.

**How it works**
Trigger: Google or Microsoft calendar scanned for meetings with external attendees in the next 24 hours; new bookings as they land.
1. Find upcoming external meetings
2. Identify attendees and account
3. Research the company
4. Research the people
5. Write the brief
6. Deliver
7. Capture the outcome
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus HubSpot / Salesforce, Clay / Apollo (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the lookahead window and the brief sections in the Config node; swap HubSpot for Salesforce. Keep the guardrail: Only public and first-party data; no scraping behind logins, no personal data beyond professional role.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/meeting-prep-research/

**Tags:** Sales, AI, HubSpot / Salesforce, Clay / Apollo

**Sources:** HubSpot — API overview — https://developers.hubspot.com/docs/api-reference/latest/overview; Apollo.io — API documentation — https://docs.apollo.io/; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Contract Review

**File:** `contract-review-automation.n8n.json`

**Title:** Review incoming contracts with Claude against your playbook in Google Docs

**Description:**

**Who's it for**
Legal and operations teams that review the same clause types in every contract.

**How it works**
Trigger: Attachments to contracts@, new documents in the CLM or DocuSign/PandaDoc inbox, or a form submission from sales.
1. Capture and identify
2. Extract clauses
3. Compare to the playbook
4. Draft the redline
5. Route by risk
6. Review surface
7. Log and learn
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Google Docs / Word, Ironclad / DocuSign CLM / PandaDoc (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put your clause playbook and risk thresholds in the Config node; connect Ironclad, DocuSign CLM or PandaDoc as the source. Keep the guardrail: The workflow triages and drafts; a person approves every contract and every redline before it goes to the counterparty.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/contract-review-automation/

**Tags:** Operations, AI, Approval, Google Docs / Word, Ironclad / DocuSign CLM / PandaDoc

**Sources:** DocuSign — Developer center — https://developers.docusign.com/; Ironclad — API documentation — https://developer.ironcladapp.com/; Google — Docs API overview — https://developers.google.com/workspace/docs/api

---

## Customer Feedback Analysis

**File:** `customer-feedback-analysis.n8n.json`

**Title:** Analyze customer feedback from Zendesk and Gong with Claude and report in Notion

**Description:**

**Who's it for**
Product and success teams that read tickets one at a time and miss the pattern.

**How it works**
Trigger: Daily pulls from each source; the weekly report compiles Monday morning.
1. Collect feedback
2. Classify by theme and sentiment
3. Extract the quotable line
4. Aggregate
5. Write the weekly report
6. Route urgent items
7. Deliver and store
8. Maintain the taxonomy
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Zendesk / Intercom / Gong, Notion + Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the theme taxonomy and the report cadence in the Config node; add Intercom or survey tools as sources. Keep the guardrail: Personal data is stripped from quotes; sources are linked, not reproduced.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/customer-feedback-analysis/

**Tags:** Customer success, AI, Zendesk / Intercom / Gong, Notion + Google Sheets

**Sources:** Zendesk — API reference — https://developer.zendesk.com/api-reference/; Intercom — Developer docs — https://developers.intercom.com/docs; n8n docs — AI Agent node — https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.agent/

---

## Review Response

**File:** `review-response-automation.n8n.json`

**Title:** Draft replies to Google reviews with Claude and approve them in Slack

**Description:**

**Who's it for**
Local businesses and franchises that answer reviews late, or only the bad ones.

**How it works**
Trigger: Polls each platform's API or a review-aggregation provider hourly; negative reviews trigger immediate alerts.
1. Collect new reviews
2. Classify
3. Fetch context
4. Draft the response
5. Route negatives to a person first
6. Approve and post
7. Track resolution
8. Monthly insight report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Google Business Profile API / Birdeye / Podium, Slack / SMS (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set your tone rules and the escalation words in the Config node; connect Birdeye or Podium if you aggregate reviews there. Keep the guardrail: Negative and sensitive reviews are never answered publicly without a person's approval.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/review-response-automation/

**Tags:** Marketing, AI, Approval, Google Business Profile API / Birdeye / Podium, Slack / SMS

**Sources:** Google — Business Profile APIs — https://developers.google.com/my-business; FTC — final rule banning fake reviews and testimonials — https://www.ftc.gov/news-events/news/press-releases/2024/08/federal-trade-commission-announces-final-rule-banning-fake-reviews-testimonials; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Resume Screening

**File:** `resume-screening-automation.n8n.json`

**Title:** Screen applications from Greenhouse with Claude and score them in Google Sheets

**Description:**

**Who's it for**
Recruiters and hiring teams that read every application by hand and still miss good candidates.

**How it works**
Trigger: Greenhouse, Lever, Ashby, Workable or Teamtailor post each new application; a daily run catches any missed.
1. Receive the application
2. Load the role criteria
3. Parse the resume
4. Score against criteria with evidence
5. Flag verification items
6. Build the ranked shortlist
7. Present to the recruiter
8. Audit and bias monitoring
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Greenhouse / Lever / Ashby, Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put the role's criteria and knock-out questions in the Config node; swap Greenhouse for Lever or Ashby. Keep the guardrail: No candidate is rejected automatically; the workflow ranks and explains, recruiters decide.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/resume-screening-automation/

**Tags:** HR, AI, Greenhouse / Lever / Ashby, Google Sheets

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; NYC DCWP — Automated employment decision tools (Local Law 144) — https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page; eCFR — 29 CFR Part 1607, Uniform Guidelines on Employee Selection Procedures — https://www.ecfr.gov/current/title-29/subtitle-B/chapter-XIV/part-1607

---

## Candidate Outreach

**File:** `candidate-outreach-automation.n8n.json`

**Title:** Send personalized candidate outreach from Greenhouse projects with Claude and Gmail

**Description:**

**Who's it for**
Recruiters who source in the ATS and write every first message by hand.

**How it works**
Trigger: A candidate added to a sourcing project in the ATS or a row added to the outreach sheet starts a sequence for that person.
1. Receive the candidate
2. Research
3. Pick the hook
4. Draft the message
5. Send from the recruiter
6. Follow up twice
7. Stop on reply
8. Measure
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Greenhouse / Lever / Ashby, Gmail / Outlook, Google Sheets (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the outreach voice and the follow-up cadence in the Config node; swap Gmail for Outlook and Greenhouse for Lever or Ashby. Keep the guardrail: Only public, professional information is used; nothing personal, nothing inferred about protected characteristics.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/candidate-outreach-automation/

**Tags:** HR, AI, Greenhouse / Lever / Ashby, Gmail / Outlook, Google Sheets

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; NYC DCWP — Automated employment decision tools (Local Law 144) — https://www.nyc.gov/site/dca/about/automated-employment-decision-tools.page; Google — Email sender guidelines — https://support.google.com/a/answer/81126

---

## Client Intake

**File:** `client-intake-automation.n8n.json`

**Title:** Intake new client enquiries from Gmail with Claude into Clio and DocuSign

**Description:**

**Who's it for**
Law firms and professional practices that reply to enquiries a day late and re-key them into the practice system.

**How it works**
Trigger: An email to the intake address, a website form submission, or a phone note typed into the shared inbox starts intake for that enquiry.
1. Receive the enquiry
2. Classify the matter
3. Extract the conflict-check facts
4. Run the conflict check
5. Acknowledge
6. Draft the next document
7. Approve
8. Open the matter
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Clio / PracticePanther, Gmail / Outlook, DocuSign / PandaDoc (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Define the practice areas and the conflict-check questions in the Config node; swap Clio for PracticePanther. Keep the guardrail: Nothing is sent to an enquirer except the acknowledgement until a person approves; no advice or fee is ever quoted automatically.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/client-intake-automation/

**Tags:** Operations, AI, Approval, Clio / PracticePanther, Gmail / Outlook, DocuSign / PandaDoc

**Sources:** ABA — Model Rule 1.7: Conflict of interest, current clients — https://www.americanbar.org/groups/professional_responsibility/publications/model_rules_of_professional_conduct/rule_1_7_conflict_of_interest_current_clients/; Clio — API documentation — https://docs.developers.clio.com/; n8n docs — Wait node (approval steps) — https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.wait/

---

## Client Reporting

**File:** `client-reporting-automation.n8n.json`

**Title:** Draft monthly client reports from Xero with Claude in Google Docs

**Description:**

**Who's it for**
Accountants and bookkeepers who write the same month-end commentary for every client.

**How it works**
Trigger: On the day you set after month-end close — or when an accountant asks for a client by name — the pack for that client is built.
1. Pull the numbers
2. Check the close
3. Compute the comparisons
4. Find the variances that matter
5. Draft the narrative
6. Assemble the pack
7. Review and sign off
8. Deliver and log
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Xero / QuickBooks / Sage, Google Docs / Word, Gmail / Outlook (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the report sections and the thresholds that trigger commentary in the Config node; swap Xero for QuickBooks or Sage. Keep the guardrail: No pack is drafted on an unclean close; the workflow reports what is open instead.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/client-reporting-automation/

**Tags:** Finance & accounting, AI, Approval, Xero / QuickBooks / Sage, Google Docs / Word, Gmail / Outlook

**Sources:** Xero — Developer documentation — https://developer.xero.com/documentation/; Intuit — QuickBooks Online API, getting started — https://developer.intuit.com/app/developer/qbo/docs/get-started; Google — Docs API overview — https://developers.google.com/workspace/docs/api

---

## Interview Scheduling

**File:** `interview-scheduling-automation.n8n.json`

**Title:** Schedule interviews from Greenhouse stage changes with Google Calendar, Claude and Twilio

**Description:**

**Who's it for**
Recruiters and coordinators who spend their week on calendar tennis.

**How it works**
Trigger: Moving a candidate to an interview stage in Greenhouse, Lever or Ashby — or a row change in the tracking sheet — starts scheduling for that stage's panel.
1. Read the stage
2. Find common slots
3. Offer the slots
4. Book
5. Remind
6. Handle changes
7. Sync the ATS
8. Report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Greenhouse / Lever / Ashby, Google Calendar / Outlook, Twilio (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the interviewer pools and the working hours in the Config node; swap Google Calendar for Outlook. Keep the guardrail: Panel working hours and blocked times are respected; the workflow never books over a 'focus' block or outside hours.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/interview-scheduling-automation/

**Tags:** HR, AI, Greenhouse / Lever / Ashby, Google Calendar / Outlook, Twilio

**Sources:** Greenhouse — Harvest API — https://developers.greenhouse.io/harvest.html; Google — Calendar API: free/busy query — https://developers.google.com/calendar/api/v3/reference/freebusy/query; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging

---

## Lead Nurture

**File:** `lead-nurture-automation.n8n.json`

**Title:** Nurture real estate leads from Follow Up Boss signals with Claude and Gmail

**Description:**

**Who's it for**
Real-estate agents whose long-term leads go cold because nobody has a reason to write.

**How it works**
Trigger: A new listing in the CRM or MLS feed, a rate change from your lender's feed, an anniversary or birthday in the CRM, or a lead going quiet for N days each start a run for the leads they affect.
1. Detect the reason
2. Match leads to the signal
3. Check the guardrails
4. Draft the message
5. Approve or auto-send
6. Send and log
7. Stop on reply
8. Report
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing, and the write-back waits for an approval in Slack or Gmail.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Slack (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Set the signal types and your voice rules in the Config node; swap Follow Up Boss for kvCORE or HubSpot. Keep the guardrail: No message without a reason the lead would recognise; the model cannot invent one.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/lead-nurture-automation/

**Tags:** Sales, AI, Approval, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Slack

**Sources:** Follow Up Boss — API documentation — https://docs.followupboss.com/; FTC — CAN-SPAM Act compliance guide — https://www.ftc.gov/business-guidance/resources/can-spam-act-compliance-guide-business; FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls

---

## Speed-to-Lead

**File:** `speed-to-lead-automation.n8n.json`

**Title:** Reply to new real estate leads in minutes with Claude, Follow Up Boss and Twilio

**Description:**

**Who's it for**
Real-estate agents and teams who lose portal leads to whoever answers first.

**How it works**
Trigger: A lead email from Zillow or Realtor.com, a website form submission, or a new person appearing in Follow Up Boss or kvCORE starts the run.
1. Receive the lead
2. Look up the lead in the CRM
3. Qualify
4. Draft the first reply
5. Check quiet hours and consent
6. Send the reply
7. Log and hand off
8. Follow up on silence
Every AI step is followed by a "Needs a person?" gate that parks low-confidence items instead of guessing.

**How to set up**
1. Open "Config (edit me)" and fill in the fields (names, approver, quiet hours, thresholds).
2. Add credentials to each service node.
3. Run once with test_mode on, read the output, then switch the trigger on.

**Requirements**
An Anthropic API key for the Claude nodes, plus Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Twilio (or their equivalents — the nodes are standard and easy to swap).

**How to customize the workflow**
Put your first-reply rules and quiet hours in the Config node; swap Follow Up Boss for kvCORE or HubSpot and Twilio for your SMS provider. Keep the guardrail: Quiet hours: nothing sent 9 pm–8 am in the lead's time zone; messages queue until morning.

Full blueprint with trigger, steps, guardrails and where the standard version stops: https://agentmelt.com/workflows/speed-to-lead-automation/

**Tags:** Sales, AI, Follow Up Boss / kvCORE / HubSpot, Gmail / Outlook, Twilio

**Sources:** Follow Up Boss — API documentation — https://docs.followupboss.com/; FCC — Telemarketing and robocalls (TCPA) — https://www.fcc.gov/general/telemarketing-and-robocalls; Twilio — Programmable Messaging docs — https://www.twilio.com/docs/messaging

---
