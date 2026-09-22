# Screen applications from Greenhouse with Claude and score them in Google Sheets — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Greenhouse / Lever / Ashby, Google Sheets.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** Greenhouse, Lever, Ashby, Workable or Teamtailor post each new application; a daily run catches any missed.
2. **Google Sheets — Create Spreadsheet Row — Load the role criteria.** Must-haves, nice-to-haves and disqualifiers for the role, written by the hiring manager in plain language and approved by HR; weights per criterion.
3. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Parse the resume" step of the Resume Screening Automation workflow run by Agentmelt.
   Task: Roles, dates, employers, skills, education, certifications and locations into structured fields, with the source text kept for quoting.
   
   Rules:
   - No candidate is rejected automatically; the workflow ranks and explains, recruiters decide.
   - Protected characteristics are excluded from scoring by instruction and by stripping fields before the model sees them.
   - Every score carries an evidence quote; unexplained scores are not shown.
   - Pass-through rates by group are monitored where lawful, and criteria that skew are reviewed.
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
   You are the "Score against criteria with evidence" step of the Resume Screening Automation workflow run by Agentmelt.
   Task: Each criterion scored met / partially / not met with a quote from the application as evidence; the agent is instructed to ignore name, photo, age, gender, nationality and school prestige unless a certification is a legal requirement.
   
   Rules:
   - No candidate is rejected automatically; the workflow ranks and explains, recruiters decide.
   - Protected characteristics are excluded from scoring by instruction and by stripping fields before the model sees them.
   - Every score carries an evidence quote; unexplained scores are not shown.
   - Pass-through rates by group are monitored where lawful, and criteria that skew are reviewed.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

7. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
8. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
9. **Code by Zapier (JavaScript) — Flag verification items.** Gaps, overlapping dates, claims that need checking (certifications, seniority) listed for the interview. Start from `return { ...inputData };` and add the rule.
10. **Code by Zapier (JavaScript) — Build the ranked shortlist.** Weighted score and band (strong / possible / unlikely); disqualifier matches are listed separately with the rule, never silently dropped. Start from `return { ...inputData };` and add the rule.
11. **Webhooks by Zapier — Custom Request.** POST `https://harvest.greenhouse.io/v1/candidates/…/activity_feed/notes` (Greenhouse Harvest API; add the API key header). Scores, bands and explanations written back to the ATS as a scorecard; the recruiter reviews the strong band plus a random sample from the others and moves candidates forward.
12. **Schedule by Zapier (trigger) — Audit and bias monitoring.** Weekly: score distributions and pass-through rates by self-reported demographic group where legally collected; anomalies flagged to HR.

## Guardrails to keep

- No candidate is rejected automatically; the workflow ranks and explains, recruiters decide.
- Protected characteristics are excluded from scoring by instruction and by stripping fields before the model sees them.
- Every score carries an evidence quote; unexplained scores are not shown.
- Pass-through rates by group are monitored where lawful, and criteria that skew are reviewed.

Full blueprint: https://agentmelt.com/workflows/resume-screening-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
