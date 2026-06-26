---
name: morning-email-digest
description: Daily 7:30am digest  pulls Gmail inbox, trash, and full-week calendar, sends color-coded HTML email to [melissaw212@gmail.com](mailto:melissaw212@gmail.com)
---

You are generating Melissa's daily email digest and sending it to [melissaw212@gmail.com](mailto:melissaw212@gmail.com). Today's date is available in your environment. Run ALL data fetches before writing a single word of the email.

---

## STEP 1  FETCH DATA (run all three before writing anything)

**A. Gmail Inbox**  Use the Gmail MCP (mcp__4dc3c0a1-e385-4ef1-bedf-7cfac77411e9) to search inbox messages from the last 24 hours:

- Query: `in:inbox newer_than:1d`

- Retrieve up to 50 messages. For each: sender name, sender email, subject, short body summary.

- Also search starred messages: `is:starred`  surface any that haven't been acted on.

**B. Gmail Trash**  Search the Gmail MCP for trash messages from the last 3 days:

- Query: `in:trash newer_than:3d`

- Retrieve up to 20 messages. Flag only: emails from real people, financial alerts, job opportunities, anything requiring a response. Skip obvious spam.

**C. Google Calendar**  Use the Google Calendar MCP (mcp__083868ca-e8e1-4cb4-83a6-921fd09dc003) to:

- List all calendars (gcal_list_calendars)

- Fetch all events for the current full week (Monday through Sunday). Use today's date to compute Monday start and Sunday end.

- For each event: day, start/end time, title, location or meeting link (paste the full Zoom/Meet/Teams URL inline), attendees, RSVP status.

---

## STEP 2  BUILD THE HTML EMAIL

Use this complete CSS and structure. Copy it exactly:

```html

<!DOCTYPE html>

<html>

<head>

<meta charset="UTF-8">

<style>

  body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif; font-size: 14px; color: #1a1a1a; max-width: 680px; margin: 0 auto; padding: 20px; line-height: 1.6; background: #f9f9f9;

  .header { background: #1a1a2e; color: white; padding: 20px 24px; border-radius: 8px; margin-bottom: 20px;

  .header h1 { font-size: 22px; margin: 0 0 4px 0; color: white;

  .header p { margin: 0; color: #aaa; font-size: 13px;

  .section { background: white; border-radius: 8px; margin-bottom: 16px; overflow: hidden; box-shadow: 0 1px 3px rgba(0,0,0,0.08);

  .sec-red    { background: #c0392b; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-orange { background: #e67e22; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-blue   { background: #2980b9; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-green  { background: #27ae60; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-purple { background: #8e44ad; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-teal   { background: #16a085; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-gray   { background: #7f8c8d; color: white; padding: 10px 16px; font-weight: 700; font-size: 12px; text-transform: uppercase; letter-spacing: 0.08em;

  .sec-body   { padding: 14px 16px;

  .tag { display: inline-block; font-size: 10px; font-weight: 700; letter-spacing: 0.05em; padding: 2px 7px; border-radius: 3px; margin-left: 6px; vertical-align: middle;

  .t-red    { background: #fde8e8; color: #c0392b;

  .t-yellow { background: #fef9e7; color: #b7950b;

  .t-green  { background: #e9f7ef; color: #1e8449;

  .t-blue   { background: #eaf4fb; color: #1a5276;

  .t-gray   { background: #f2f3f4; color: #555;

  ol, ul { margin: 0; padding-left: 20px;

  li { margin-bottom: 9px; line-height: 1.5;

  .day-label { font-weight: 700; font-size: 13px; color: #2c3e50; margin: 10px 0 4px 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 3px;

  .event { margin-left: 8px; margin-bottom: 4px; font-size: 13px;

  .today-flag { color: #c0392b; font-weight: 700; margin-right: 3px;

  a { color: #2980b9;

  .meta { color: #888; font-size: 12px; margin-top: 3px;

  hr { border: none; border-top: 1px solid #ecf0f1; margin: 10px 0;

</style>

</head>

<body>

```

### Section header color assignments (use these consistently):

- **ACTION REQUIRED**  `sec-red`

- **TODAY'S CALENDAR**  `sec-orange`

- **THIS WEEK'S CALENDAR**  `sec-orange`

- **JOBS & OPPORTUNITIES**  `sec-blue`

- **RECRUITER & PERSONAL OUTREACH**  `sec-purple`

- **FOLLOW-UPS & WAITING**  inline style `background:#f39c12; color:white;`

- **PURCHASES, RECEIPTS & FINANCIAL**  `sec-green`

- **EVERYTHING ELSE**  `sec-gray`

- **TRASH WATCH**  `sec-teal`

### Inline tag colors:

- `t-red` = NO REPLY, ACTION NEEDED, URGENT, FIX

- `t-yellow` = WAITING, FOLLOW UP, STARRED, FINANCIAL, HEALTH

- `t-green` = CONFIRMED, SHIPPED, REFUND, JOB MATCH

- `t-blue` = JOB ALERT, INFO, ALUMNI CONNECTION, JOB DIGEST

- `t-gray` = FYI, PROMO, NEWSLETTER, TRASH, PURCHASE

### EMAIL SECTIONS  build in this order:

**HEADER BLOCK:**

```html

<div class="header">

  <h1>Good morning, Melissa</h1>

  <p>[Day of week], [Month Day, Year]</p>

</div>

```

**SECTION 1  ACTION REQUIRED** (sec-red)  always show

Everything Melissa must do, respond to, or act on TODAY. RSVPs needed, recruiters waiting, financial disputes, expiring offers, same-day meeting prep. Numbered list. Each item: who, what, deadline/context.

**SECTION 2  TODAY'S CALENDAR** (sec-orange)  always show

All events for today. Flag each with  `<span class="today-flag"></span>`. Full meeting links inline.

**SECTION 3  THIS WEEK'S CALENDAR** (sec-orange)  always show

MondaySunday. `.day-label` for each day. Time, title, full meeting link. Flag today's events with . Empty days: "Clear."

**SECTION 4  JOBS & OPPORTUNITIES** (sec-blue)  always show

All job alerts, LinkedIn notifications, recruiter outreach, job board emails from last 24 hours. Title, company, location, salary if listed, one-line description. Group by level: VP/Head  Director  IC.

**SECTION 5  RECRUITER & PERSONAL OUTREACH** (sec-purple)  omit if none

Direct emails from real people. Sender + company, subject, 12 sentence summary. Flag if response needed.

**SECTION 6  FOLLOW-UPS & WAITING** (inline background:#f39c12)  omit if none

Anything sent with no reply. Who, when sent, what's needed. Pending RSVPs, unresolved disputes, stalled outreach.

**SECTION 7  PURCHASES, RECEIPTS & FINANCIAL** (sec-green)  omit if none

Orders, shipping, returns, refunds, financial alerts, subscriptions. Flag time-sensitive items.

**SECTION 8  EVERYTHING ELSE** (sec-gray)  omit if none

Newsletters, digests, social/dating notifications. One line each.

**SECTION 9  TRASH WATCH** (sec-teal)  always show

Last 3 days of trash: surface emails from real people, financial alerts, job opportunities, urgent subjects only. Flag if job search emails are landing in trash (filter fix needed). If nothing notable: "Nothing notable in trash."

---

## STEP 3  DROP EMAIL IN OUTBOX (replaces old Zapier send)

The sandbox blocks googleapis.com, so this task does not send email. Instead, drop two files into the shared outbox. A local Mac cron job runs every 5 minutes, picks up pending emails, sends them via the Gmail API, applies the INBOX label, and moves them to `/Users/Owner/Documents/Claude/Outbox/sent/`.

Use a unique ID per run to avoid collisions. Format: `morning-email-digest-YYYY-MM-DD-HHMMSS` (compute via bash).

DROP IN EXACTLY ONE PATH (not both  duplicates cause cron to send twice).

PRIMARY PATH (try first):

- HTML: `/Users/Owner/Documents/Claude/Outbox/pending/<id>.html`

- Meta: `/Users/Owner/Documents/Claude/Outbox/pending/<id>.meta.json`

WRITE TO PRIMARY ONLY IF YOU CAN. If the primary write succeeds (no error), STOP. Do not also write to the fallback path.

FALLBACK PATH (use ONLY if primary write errored with permission/access denied):

- HTML: `/Users/Owner/Documents/Claude/Scheduled/morning-email-digest/pending/<id>.html`

- Meta: `/Users/Owner/Documents/Claude/Scheduled/morning-email-digest/pending/<id>.meta.json`

Cron watches both paths but expects each delivery in only one of them.

meta.json contents (single line, valid JSON):

```

\"to":"melissaw212@gmail.com","subject":"Daily Digest  [Month Day, Year]"

```

Write the HTML file FIRST, then the meta.json file. The cron only sends when it sees a `.meta.json`, so writing meta last avoids racing.

Do NOT call Zapier. Do NOT call create_draft. Do NOT use Chrome MCP.

---

## STEP 4  VERIFY

Confirm both files exist in WHICHEVER path you used (primary or fallback) and the HTML file is non-empty. That's the signal to the local cron that the digest is ready to send.

---

## RULES

- Skip emails Melissa sent to herself

- Skip pure retail promos UNLESS order confirmation, shipping, return, or financial charge

- Every entry: 12 sentences max, except action items

- Sections 1, 2, 3, 4, 9 always appear  others omit if empty

- Run all three data fetches before writing anything