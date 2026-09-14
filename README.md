# Agentmelt blueprints — n8n workflow templates

48 importable n8n workflows, one per business process, generated from the blueprints at https://agentmelt.com/workflows/. Each file has a `Config (edit me)` node for your name, email, company and quiet hours, an approval step (Slack or Gmail `sendAndWait`) wherever money or a customer is involved, and a `Needs a person?` gate after every AI step so uncertain items go to a human instead of out the door.

## How to import

1. In n8n, open a workflow, click the `⋯` menu → **Import from file** (or **Import from URL** with the raw file link).
2. Open `Config (edit me)` and fill in the fields.
3. Add your credentials to each node that asks for them.
4. Run once in `test_mode: true`; switch it off when the output looks right.

The blueprint page for each template explains the trigger, the steps, the guardrails and where the standard version stops. Kits with a setup guide, scripts and prompts, or an install into your own accounts: https://agentmelt.com/packages/.

## What is verified

Every file is validated against n8n's own node definitions (n8n-nodes-base 2.38, langchain nodes) before it is published: known node types and versions, every required parameter present, every connection to an input that accepts it, every `$('Node')` reference resolvable. All 48 import into n8n 2.38 through the CLI and through the editor; the only markers the editor shows are the credentials a template cannot ship.

## Templates

| Template | Department | Blueprint page |
|---|---|---|
| [Spend Analysis](./templates/spend-analysis.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/spend-analysis/ |
| [Demand Forecasting](./templates/demand-forecasting.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/demand-forecasting/ |
| [Employee Onboarding](./templates/employee-onboarding-automation.n8n.json) | HR | https://agentmelt.com/workflows/employee-onboarding-automation/ |
| [Automated Code Review](./templates/automated-code-review.n8n.json) | Engineering | https://agentmelt.com/workflows/automated-code-review/ |
| [Expansion Opportunity Detection](./templates/expansion-opportunity-detection.n8n.json) | Customer success | https://agentmelt.com/workflows/expansion-opportunity-detection/ |
| [Unit Test Generation](./templates/unit-test-generation.n8n.json) | Engineering | https://agentmelt.com/workflows/unit-test-generation/ |
| [Inventory Optimization](./templates/inventory-optimization.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/inventory-optimization/ |
| [Social Listening & Response](./templates/social-listening-response.n8n.json) | Marketing | https://agentmelt.com/workflows/social-listening-response/ |
| [Employee Offboarding](./templates/employee-offboarding-automation.n8n.json) | HR | https://agentmelt.com/workflows/employee-offboarding-automation/ |
| [Insurance Underwriting Intake](./templates/insurance-underwriting-intake.n8n.json) | Insurance | https://agentmelt.com/workflows/insurance-underwriting-intake/ |
| [Financial Reconciliation](./templates/financial-reconciliation-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/financial-reconciliation-automation/ |
| [Email Triage](./templates/email-triage-automation.n8n.json) | Operations | https://agentmelt.com/workflows/email-triage-automation/ |
| [Support Ticket Deflection](./templates/support-ticket-deflection.n8n.json) | Customer support | https://agentmelt.com/workflows/support-ticket-deflection/ |
| [Document & Proposal Generation](./templates/document-generation-automation.n8n.json) | Operations | https://agentmelt.com/workflows/document-generation-automation/ |
| [Subscription & Dunning](./templates/subscription-dunning-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/subscription-dunning-automation/ |
| [Logistics Optimization](./templates/logistics-optimization.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/logistics-optimization/ |
| [Proactive Customer Outreach](./templates/proactive-customer-outreach.n8n.json) | Customer support | https://agentmelt.com/workflows/proactive-customer-outreach/ |
| [Customer Onboarding](./templates/customer-onboarding-automation.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-onboarding-automation/ |
| [Supplier Risk Monitoring](./templates/supplier-risk-monitoring.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/supplier-risk-monitoring/ |
| [Prior Authorization](./templates/prior-authorization-automation.n8n.json) | Operations | https://agentmelt.com/workflows/prior-authorization-automation/ |
| [Customer Health Scoring](./templates/customer-health-scoring.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-health-scoring/ |
| [Insurance Claims Intake](./templates/insurance-claims-intake.n8n.json) | Insurance | https://agentmelt.com/workflows/insurance-claims-intake/ |
| [Payroll](./templates/payroll-automation.n8n.json) | HR | https://agentmelt.com/workflows/payroll-automation/ |
| [Security Alert Triage](./templates/security-alert-triage.n8n.json) | Security & IT | https://agentmelt.com/workflows/security-alert-triage/ |
| [Competitor Monitoring](./templates/competitor-monitoring.n8n.json) | Marketing | https://agentmelt.com/workflows/competitor-monitoring/ |
| [Content Repurposing](./templates/content-repurposing-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/content-repurposing-automation/ |
| [Customer Win-Back](./templates/customer-win-back-automation.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-win-back-automation/ |
| [Appointment Reminder](./templates/appointment-reminders-automation.n8n.json) | Operations | https://agentmelt.com/workflows/appointment-reminders-automation/ |
| [KYC/AML Monitoring](./templates/kyc-aml-monitoring.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/kyc-aml-monitoring/ |
| [Inbound Lead Qualification](./templates/inbound-lead-qualification.n8n.json) | Sales | https://agentmelt.com/workflows/inbound-lead-qualification/ |
| [Data Migration](./templates/data-migration-automation.n8n.json) | Engineering | https://agentmelt.com/workflows/data-migration-automation/ |
| [Cold Outbound](./templates/cold-outbound-sequencing.n8n.json) | Sales | https://agentmelt.com/workflows/cold-outbound-sequencing/ |
| [Weekly Reporting](./templates/weekly-reporting-automation.n8n.json) | Operations | https://agentmelt.com/workflows/weekly-reporting-automation/ |
| [Real Estate Listing](./templates/listing-description-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/listing-description-automation/ |
| [IT Helpdesk](./templates/it-helpdesk-automation.n8n.json) | Security & IT | https://agentmelt.com/workflows/it-helpdesk-automation/ |
| [Purchase Order](./templates/purchase-order-automation.n8n.json) | Supply chain & procurement | https://agentmelt.com/workflows/purchase-order-automation/ |
| [Invoice Processing](./templates/invoice-processing-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/invoice-processing-automation/ |
| [Meeting Prep](./templates/meeting-prep-research.n8n.json) | Sales | https://agentmelt.com/workflows/meeting-prep-research/ |
| [Contract Review](./templates/contract-review-automation.n8n.json) | Operations | https://agentmelt.com/workflows/contract-review-automation/ |
| [Customer Feedback Analysis](./templates/customer-feedback-analysis.n8n.json) | Customer success | https://agentmelt.com/workflows/customer-feedback-analysis/ |
| [Review Response](./templates/review-response-automation.n8n.json) | Marketing | https://agentmelt.com/workflows/review-response-automation/ |
| [Resume Screening](./templates/resume-screening-automation.n8n.json) | HR | https://agentmelt.com/workflows/resume-screening-automation/ |
| [Candidate Outreach](./templates/candidate-outreach-automation.n8n.json) | HR | https://agentmelt.com/workflows/candidate-outreach-automation/ |
| [Client Intake](./templates/client-intake-automation.n8n.json) | Operations | https://agentmelt.com/workflows/client-intake-automation/ |
| [Client Reporting](./templates/client-reporting-automation.n8n.json) | Finance & accounting | https://agentmelt.com/workflows/client-reporting-automation/ |
| [Interview Scheduling](./templates/interview-scheduling-automation.n8n.json) | HR | https://agentmelt.com/workflows/interview-scheduling-automation/ |
| [Lead Nurture](./templates/lead-nurture-automation.n8n.json) | Sales | https://agentmelt.com/workflows/lead-nurture-automation/ |
| [Speed-to-Lead](./templates/speed-to-lead-automation.n8n.json) | Sales | https://agentmelt.com/workflows/speed-to-lead-automation/ |

Generated from the site data on 2026-09-14. Licence: MIT for the workflow files (see LICENSE). The blueprint pages, kits and guides on agentmelt.com stay © Agentmelt.
