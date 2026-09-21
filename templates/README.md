# Agentmelt blueprints — n8n workflow templates

48 importable n8n workflows, one per business process, generated from the blueprints at https://agentmelt.com/workflows/. Each file has a `Config (edit me)` node for your name, email, company and quiet hours, an approval step (Slack or Gmail `sendAndWait`) wherever money or a customer is involved, and a `Needs a person?` gate after every AI step so uncertain items go to a human instead of out the door.

## How to import

1. In n8n, open a workflow, click the `⋯` menu → **Import from file** (or **Import from URL** with the raw file link).
2. Open `Config (edit me)` and fill in the fields.
3. Add your credentials to each node that asks for them.
4. Run once in `test_mode: true`; switch it off when the output looks right.

The blueprint page for each template explains the trigger, the steps, the guardrails and where the standard version stops. Kits with a setup guide, scripts and prompts, or an install into your own accounts: https://agentmelt.com/packages/.

## Make and Zapier

- `make/<slug>.make.json` — the same process as a Make scenario blueprint (new scenario → ⋯ → Import blueprint). Every module resolves against Make's app definitions; connections and the `Config (edit me)` variables are yours to fill.
- `zapier/<slug>.md` — Zapier has no importable file, so the ten package blueprints ship as step-by-step Zap recipes with the Claude prompts and the Code-by-Zapier stubs.

## Templates

| Template | Department | Make | Blueprint page |
|---|---|---|---|
| [Spend Analysis](./spend-analysis.n8n.json) | Supply chain & procurement | [blueprint](./make/spend-analysis.make.json) | https://agentmelt.com/workflows/spend-analysis/ |
| [Demand Forecasting](./demand-forecasting.n8n.json) | Supply chain & procurement | [blueprint](./make/demand-forecasting.make.json) | https://agentmelt.com/workflows/demand-forecasting/ |
| [Employee Onboarding](./employee-onboarding-automation.n8n.json) | HR | [blueprint](./make/employee-onboarding-automation.make.json) | https://agentmelt.com/workflows/employee-onboarding-automation/ |
| [Automated Code Review](./automated-code-review.n8n.json) | Engineering | [blueprint](./make/automated-code-review.make.json) | https://agentmelt.com/workflows/automated-code-review/ |
| [Expansion Opportunity Detection](./expansion-opportunity-detection.n8n.json) | Customer success | [blueprint](./make/expansion-opportunity-detection.make.json) | https://agentmelt.com/workflows/expansion-opportunity-detection/ |
| [Unit Test Generation](./unit-test-generation.n8n.json) | Engineering | [blueprint](./make/unit-test-generation.make.json) | https://agentmelt.com/workflows/unit-test-generation/ |
| [Inventory Optimization](./inventory-optimization.n8n.json) | Supply chain & procurement | [blueprint](./make/inventory-optimization.make.json) | https://agentmelt.com/workflows/inventory-optimization/ |
| [Social Listening](./social-listening-response.n8n.json) | Marketing | [blueprint](./make/social-listening-response.make.json) | https://agentmelt.com/workflows/social-listening-response/ |
| [Employee Offboarding](./employee-offboarding-automation.n8n.json) | HR | [blueprint](./make/employee-offboarding-automation.make.json) | https://agentmelt.com/workflows/employee-offboarding-automation/ |
| [Automated Insurance Underwriting Intake](./insurance-underwriting-intake.n8n.json) | Insurance | [blueprint](./make/insurance-underwriting-intake.make.json) | https://agentmelt.com/workflows/insurance-underwriting-intake/ |
| [Financial Reconciliation](./financial-reconciliation-automation.n8n.json) | Finance & accounting | [blueprint](./make/financial-reconciliation-automation.make.json) | https://agentmelt.com/workflows/financial-reconciliation-automation/ |
| [Email Triage](./email-triage-automation.n8n.json) | Operations | [blueprint](./make/email-triage-automation.make.json) | https://agentmelt.com/workflows/email-triage-automation/ |
| [Support Ticket Deflection](./support-ticket-deflection.n8n.json) | Customer support | [blueprint](./make/support-ticket-deflection.make.json) | https://agentmelt.com/workflows/support-ticket-deflection/ |
| [Document & Proposal Generation](./document-generation-automation.n8n.json) | Operations | [blueprint](./make/document-generation-automation.make.json) | https://agentmelt.com/workflows/document-generation-automation/ |
| [Subscription & Dunning](./subscription-dunning-automation.n8n.json) | Finance & accounting | [blueprint](./make/subscription-dunning-automation.make.json) | https://agentmelt.com/workflows/subscription-dunning-automation/ |
| [Logistics Optimization](./logistics-optimization.n8n.json) | Supply chain & procurement | [blueprint](./make/logistics-optimization.make.json) | https://agentmelt.com/workflows/logistics-optimization/ |
| [Proactive Customer Outreach](./proactive-customer-outreach.n8n.json) | Customer support | [blueprint](./make/proactive-customer-outreach.make.json) | https://agentmelt.com/workflows/proactive-customer-outreach/ |
| [Customer Onboarding](./customer-onboarding-automation.n8n.json) | Customer success | [blueprint](./make/customer-onboarding-automation.make.json) | https://agentmelt.com/workflows/customer-onboarding-automation/ |
| [Supplier Risk Monitoring](./supplier-risk-monitoring.n8n.json) | Supply chain & procurement | [blueprint](./make/supplier-risk-monitoring.make.json) | https://agentmelt.com/workflows/supplier-risk-monitoring/ |
| [Prior Authorization](./prior-authorization-automation.n8n.json) | Operations | [blueprint](./make/prior-authorization-automation.make.json) | https://agentmelt.com/workflows/prior-authorization-automation/ |
| [Customer Health Scoring](./customer-health-scoring.n8n.json) | Customer success | [blueprint](./make/customer-health-scoring.make.json) | https://agentmelt.com/workflows/customer-health-scoring/ |
| [Insurance Claims Intake](./insurance-claims-intake.n8n.json) | Insurance | [blueprint](./make/insurance-claims-intake.make.json) | https://agentmelt.com/workflows/insurance-claims-intake/ |
| [Payroll](./payroll-automation.n8n.json) | HR | [blueprint](./make/payroll-automation.make.json) | https://agentmelt.com/workflows/payroll-automation/ |
| [Automated Security Alert Triage](./security-alert-triage.n8n.json) | Security & IT | [blueprint](./make/security-alert-triage.make.json) | https://agentmelt.com/workflows/security-alert-triage/ |
| [Competitor Monitoring](./competitor-monitoring.n8n.json) | Marketing | [blueprint](./make/competitor-monitoring.make.json) | https://agentmelt.com/workflows/competitor-monitoring/ |
| [Content Repurposing](./content-repurposing-automation.n8n.json) | Marketing | [blueprint](./make/content-repurposing-automation.make.json) | https://agentmelt.com/workflows/content-repurposing-automation/ |
| [Customer Win-Back](./customer-win-back-automation.n8n.json) | Customer success | [blueprint](./make/customer-win-back-automation.make.json) | https://agentmelt.com/workflows/customer-win-back-automation/ |
| [Appointment Reminders](./appointment-reminders-automation.n8n.json) | Operations | [blueprint](./make/appointment-reminders-automation.make.json) | https://agentmelt.com/workflows/appointment-reminders-automation/ |
| [KYC/AML Monitoring](./kyc-aml-monitoring.n8n.json) | Finance & accounting | [blueprint](./make/kyc-aml-monitoring.make.json) | https://agentmelt.com/workflows/kyc-aml-monitoring/ |
| [Inbound Lead Qualification](./inbound-lead-qualification.n8n.json) | Sales | [blueprint](./make/inbound-lead-qualification.make.json) | https://agentmelt.com/workflows/inbound-lead-qualification/ |
| [Data Migration](./data-migration-automation.n8n.json) | Engineering | [blueprint](./make/data-migration-automation.make.json) | https://agentmelt.com/workflows/data-migration-automation/ |
| [Cold Outbound](./cold-outbound-sequencing.n8n.json) | Sales | [blueprint](./make/cold-outbound-sequencing.make.json) | https://agentmelt.com/workflows/cold-outbound-sequencing/ |
| [Weekly Reporting](./weekly-reporting-automation.n8n.json) | Operations | [blueprint](./make/weekly-reporting-automation.make.json) | https://agentmelt.com/workflows/weekly-reporting-automation/ |
| [Real Estate Listing](./listing-description-automation.n8n.json) | Marketing | [blueprint](./make/listing-description-automation.make.json) | https://agentmelt.com/workflows/listing-description-automation/ |
| [IT Helpdesk](./it-helpdesk-automation.n8n.json) | Security & IT | [blueprint](./make/it-helpdesk-automation.make.json) | https://agentmelt.com/workflows/it-helpdesk-automation/ |
| [Purchase Order](./purchase-order-automation.n8n.json) | Supply chain & procurement | [blueprint](./make/purchase-order-automation.make.json) | https://agentmelt.com/workflows/purchase-order-automation/ |
| [Invoice Processing](./invoice-processing-automation.n8n.json) | Finance & accounting | [blueprint](./make/invoice-processing-automation.make.json) | https://agentmelt.com/workflows/invoice-processing-automation/ |
| [Meeting Prep](./meeting-prep-research.n8n.json) | Sales | [blueprint](./make/meeting-prep-research.make.json) | https://agentmelt.com/workflows/meeting-prep-research/ |
| [Contract Review](./contract-review-automation.n8n.json) | Operations | [blueprint](./make/contract-review-automation.make.json) | https://agentmelt.com/workflows/contract-review-automation/ |
| [Customer Feedback Analysis](./customer-feedback-analysis.n8n.json) | Customer success | [blueprint](./make/customer-feedback-analysis.make.json) | https://agentmelt.com/workflows/customer-feedback-analysis/ |
| [Review Response](./review-response-automation.n8n.json) | Marketing | [blueprint](./make/review-response-automation.make.json) | https://agentmelt.com/workflows/review-response-automation/ |
| [Resume Screening](./resume-screening-automation.n8n.json) | HR | [blueprint](./make/resume-screening-automation.make.json) | https://agentmelt.com/workflows/resume-screening-automation/ |
| [Candidate Outreach](./candidate-outreach-automation.n8n.json) | HR | [blueprint](./make/candidate-outreach-automation.make.json) | https://agentmelt.com/workflows/candidate-outreach-automation/ |
| [Client Intake](./client-intake-automation.n8n.json) | Operations | [blueprint](./make/client-intake-automation.make.json) | https://agentmelt.com/workflows/client-intake-automation/ |
| [Client Reporting](./client-reporting-automation.n8n.json) | Finance & accounting | [blueprint](./make/client-reporting-automation.make.json) | https://agentmelt.com/workflows/client-reporting-automation/ |
| [Interview Scheduling](./interview-scheduling-automation.n8n.json) | HR | [blueprint](./make/interview-scheduling-automation.make.json) | https://agentmelt.com/workflows/interview-scheduling-automation/ |
| [Lead Nurture](./lead-nurture-automation.n8n.json) | Sales | [blueprint](./make/lead-nurture-automation.make.json) | https://agentmelt.com/workflows/lead-nurture-automation/ |
| [Speed-to-Lead](./speed-to-lead-automation.n8n.json) | Sales | [blueprint](./make/speed-to-lead-automation.make.json) | https://agentmelt.com/workflows/speed-to-lead-automation/ |

Generated from the site data on 2026-09-21. Licence: use and adapt freely; the blueprint copy and kits stay © Agentmelt.
