# Agentmelt blueprints — n8n workflow templates

48 importable n8n workflows, one per business process, generated from the blueprints at https://agentmelt.com/workflows/. Each file has a `Config (edit me)` node for your name, email, company and quiet hours, an approval step (Slack or Gmail `sendAndWait`) wherever money or a customer is involved, and a `Needs a person?` gate after every AI step so uncertain items go to a human instead of out the door.

## How to import

1. In n8n, open a workflow, click the `⋯` menu → **Import from file** (or **Import from URL** with the raw file link).
2. Open `Config (edit me)` and fill in the fields.
3. Add your credentials to each node that asks for them.
4. Run once in `test_mode: true`; switch it off when the output looks right.

The blueprint page for each template explains the trigger, the steps, the guardrails and where the standard version stops. Kits with a setup guide, scripts and prompts, or an install into your own accounts: https://agentmelt.com/packages/.

## Templates

| Template | Department | Blueprint page |
|---|---|---|
| [Spend Analysis](./spend-analysis.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/spend-analysis/ |
| [Demand Forecasting](./demand-forecasting.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/demand-forecasting/ |
| [Employee Onboarding](./employee-onboarding-automation.n8n.json) | HR | https://agentmelt.com/workflows/employee-onboarding-automation/ |
| [Automated Code Review](./automated-code-review.n8n.json) | Engineering | https://agentmelt.com/workflows/automated-code-review/ |
| [Expansion Opportunity Detection](./expansion-opportunity-detection.n8n.json) | Customer success | https://agentmelt.com/workflows/expansion-opportunity-detection/ |
| [Unit Test Generation](./unit-test-generation.n8n.json) | Engineering | https://agentmelt.com/workflows/unit-test-generation/ |
| [Inventory Optimization](./inventory-optimization.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/inventory-optimization/ |
| [Social Listening & Response](./social-listening-response.n8n.json) | Marketing | https://agentmelt.com/workflows/social-listening-response/ |
| [Employee Offboarding](./employee-offboarding-automation.n8n.json) | HR | https://agentmelt.com/workflows/employee-offboarding-automation/ |
| [Insurance Underwriting Intake](./insurance-underwriting-intake.n8n.json) | Insurance | https://agentmelt.com/workflows/insurance-underwriting-intake/ |
| [Financial Reconciliation](./financial-reconciliation-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/financial-reconciliation-automation/ |
| [Email Triage](./email-triage-automation.n8n.json) | Operations | https://agentmelt.com/workflows/email-triage-automation/ |
| [Support Ticket Deflection](./support-ticket-deflection.n8n.json) | Customer support | https://agentmelt.com/workflows/support-ticket-deflection/ |
| [Document & Proposal Generation](./document-generation-automation.n8n.json) | Operations | https://agentmelt.com/workflows/document-generation-automation/ |
| [Subscription & Dunning](./subscription-dunning-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/subscription-dunning-automation/ |
| [Logistics Optimization](./logistics-optimization.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/logistics-optimization/ |
| [Proactive Customer Outreach](./proactive-customer-outreach.n8n.json) | Customer support | https://agentmelt.com/workflows/proactive-customer-outreach/ |
| [Customer Onboarding](./customer-onboarding-automation.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-onboarding-automation/ |
| [Supplier Risk Monitoring](./supplier-risk-monitoring.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/supplier-risk-monitoring/ |
| [Prior Authorization](./prior-authorization-automation.n8n.json) | Operations | https://agentmelt.com/workflows/prior-authorization-automation/ |
| [Customer Health Scoring](./customer-health-scoring.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-health-scoring/ |
| [Insurance Claims Intake](./insurance-claims-intake.n8n.json) | Insurance | https://agentmelt.com/workflows/insurance-claims-intake/ |
| [Payroll](./payroll-automation.n8n.json) | HR | https://agentmelt.com/workflows/payroll-automation/ |
| [Security Alert Triage](./security-alert-triage.n8n.json) | Security & IT | https://agentmelt.com/workflows/security-alert-triage/ |
| [Competitor Monitoring](./competitor-monitoring.n8n.json) | Marketing | https://agentmelt.com/workflows/competitor-monitoring/ |
| [Content Repurposing](./content-repurposing-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/content-repurposing-automation/ |
| [Customer Win-Back](./customer-win-back-automation.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-win-back-automation/ |
| [Appointment Reminder](./appointment-reminders-automation.n8n.json) | Operations | https://agentmelt.com/workflows/appointment-reminders-automation/ |
| [KYC/AML Monitoring](./kyc-aml-monitoring.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/kyc-aml-monitoring/ |
| [Inbound Lead Qualification](./inbound-lead-qualification.n8n.json) | Sales | https://agentmelt.com/workflows/inbound-lead-qualification/ |
| [Data Migration](./data-migration-automation.n8n.json) | Engineering | https://agentmelt.com/workflows/data-migration-automation/ |
| [Cold Outbound](./cold-outbound-sequencing.n8n.json) | Sales | https://agentmelt.com/workflows/cold-outbound-sequencing/ |
| [Weekly Reporting](./weekly-reporting-automation.n8n.json) | Operations | https://agentmelt.com/workflows/weekly-reporting-automation/ |
| [Real Estate Listing](./listing-description-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/listing-description-automation/ |
| [IT Helpdesk](./it-helpdesk-automation.n8n.json) | Security & IT | https://agentmelt.com/workflows/it-helpdesk-automation/ |
| [Purchase Order](./purchase-order-automation.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/purchase-order-automation/ |
| [Invoice Processing](./invoice-processing-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/invoice-processing-automation/ |
| [Meeting Prep](./meeting-prep-research.n8n.json) | Sales | https://agentmelt.com/workflows/meeting-prep-research/ |
| [Contract Review](./contract-review-automation.n8n.json) | Operations | https://agentmelt.com/workflows/contract-review-automation/ |
| [Customer Feedback Analysis](./customer-feedback-analysis.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-feedback-analysis/ |
| [Review Response](./review-response-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/review-response-automation/ |
| [Resume Screening](./resume-screening-automation.n8n.json) | HR | https://agentmelt.com/workflows/resume-screening-automation/ |
| [Candidate Outreach](./candidate-outreach-automation.n8n.json) | HR | https://agentmelt.com/workflows/candidate-outreach-automation/ |
| [Client Intake](./client-intake-automation.n8n.json) | Operations | https://agentmelt.com/workflows/client-intake-automation/ |
| [Client Reporting](./client-reporting-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/client-reporting-automation/ |
| [Interview Scheduling](./interview-scheduling-automation.n8n.json) | HR | https://agentmelt.com/workflows/interview-scheduling-automation/ |
| [Lead Nurture](./lead-nurture-automation.n8n.json) | Sales | https://agentmelt.com/workflows/lead-nurture-automation/ |
| [Speed-to-Lead](./speed-to-lead-automation.n8n.json) | Sales | https://agentmelt.com/workflows/speed-to-lead-automation/ |

Generated from the site data on 2026-09-16. Licence: use and adapt freely; the blueprint copy and kits stay © Agentmelt.
