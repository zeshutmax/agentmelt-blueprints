# Schedule interviews from Greenhouse stage changes with Google Calendar, Claude and Twilio — Zapier recipe

Zapier has no importable file, so this is the build guide: the same process as the n8n template and the Make blueprint, one Zap step per line. Expect 10–14 steps; the AI steps use the **Anthropic (Claude)** app, rules go in **Code by Zapier**, and every AI step is followed by a **Filter** that stops the Zap when Claude flags the item for a person.

## Before you start

- Keep the values from "Config (edit me)" somewhere the steps can read them — a **Storage by Zapier** key each, or a Formatter → Utilities step at the top of the Zap: your name, your email, company, time zone, quiet hours (21–8), approver (channel or email), test mode.
- Connect the apps once: Anthropic (an API key), plus Greenhouse / Lever / Ashby, Google Calendar / Outlook, Twilio.
- Turn the Zap on with test mode on; read the first runs in Zap History before switching it off.

## Steps

1. **Trigger — Webhooks by Zapier — Catch Hook (trigger).** Moving a candidate to an interview stage in Greenhouse, Lever or Ashby — or a row change in the tracking sheet — starts scheduling for that stage's panel.
2. **Google Calendar — Create Detailed Event — Find common slots.** Free/busy across every panel member for the next ten working days, inside their working hours, avoiding lunch and back-to-back blocks; three options, spread across days.
3. **Gmail — Send Email — Offer the slots.** One email from the recruiter with three buttons or links, the format, who they will meet, and what to prepare — written for the stage, not a template dump.
4. **Google Calendar — Create Detailed Event — Book.** The chosen slot becomes an event on every calendar with the video link or room, the candidate's CV attached for the panel, and the interview kit.
5. **Twilio — Send SMS — Remind.** Candidate: 24 hours and 2 hours before, by email and SMS if they gave a number.
6. **Anthropic (Claude) — Send Message.** Model `claude-sonnet-5`, max tokens 2000, temperature 0.2. Paste the system prompt below; the user message is the fields from the previous step.

   ```
   You are the "Handle changes" step of the Interview Scheduling Automation workflow run by Agentmelt.
   Task: A reply asking to move, cancel or ask a question is understood and acted on in the same thread; new slots are offered without the recruiter.
   
   Rules:
   - Panel working hours and blocked times are respected; the workflow never books over a 'focus' block or outside hours.
   - Candidates are never offered a slot less than 24 hours away unless the recruiter allows it for the stage.
   - Every change is written to the same email thread, so the candidate has one conversation, not five.
   - SMS only with a number the candidate gave; opt-out honoured.
   - The recruiter is copied on every candidate-facing message and can take over any thread by replying.
   - Answer only from the data provided in the input. If something is missing, say so in the output instead of guessing.
   - If this step produces a message or a document, put the full text in `draft` (and a `subject` if it is an email); put a one-line summary in `summary`.
   - Set `needs_human` true whenever you are unsure, the input is unusual, or a rule above applies; a person will look at it.
   - Return valid JSON matching the output schema; no prose outside the JSON.
   
   Reply with a single JSON object and nothing else: the fields the task needs, plus "needs_human" (true when unsure), "confidence" (0–1) and "summary" (one line).
   ```

7. **Code by Zapier (JavaScript) — parse Claude's JSON.** Input `text` = Claude's reply; code `return JSON.parse(inputData.text);` so the fields become mappable in later steps.
8. **Filter by Zapier.** Only continue if `needs_human` (from the previous step) *does not exactly match* `true`. Everything Claude is unsure about stops here — check Zap History for those, or add a **Paths** step whose second path posts the item to your approver.
9. **Webhooks by Zapier — Custom Request.** POST `https://harvest.greenhouse.io/v1/applications/…/move` (Greenhouse Harvest API; add the API key header). Interview scheduled, rescheduled, completed or no-show is written back to the candidate's record; the scorecard is opened for the panel.
10. **Google Sheets — Create Spreadsheet Row — Report.** Time from stage change to booked, reschedule rate, no-show rate by role and stage, so the recruiter sees where the process drags.

## Guardrails to keep

- Panel working hours and blocked times are respected; the workflow never books over a 'focus' block or outside hours.
- Candidates are never offered a slot less than 24 hours away unless the recruiter allows it for the stage.
- Every change is written to the same email thread, so the candidate has one conversation, not five.
- SMS only with a number the candidate gave; opt-out honoured.
- The recruiter is copied on every candidate-facing message and can take over any thread by replying.

Full blueprint: https://agentmelt.com/workflows/interview-scheduling-automation/ · n8n template and Make blueprint: https://github.com/zeshutmax/agentmelt-blueprints
