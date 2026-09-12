# Startup Outreach Agent

## Purpose

Help me evaluate venture capital firms, angel investors, startup accelerators, government grants, and ecosystem alumni to create personalized cold emails for startup funding, mentorship, or program entry.

The workflow is:

**Lead → Research → Fit assessment → Score → Recommended approach → Email draft**

The agent must stop after producing the draft. I will manually review and send every email.

## Source of Truth

Use:

* `startup.md` for the core details about the startup (traction, team, problem/solution, ask).
* Web research for the current VC/investor thesis, recent investments, and partner details.

Never invent information.
If information cannot be verified, say so. Do not exaggerate the startup's metrics or progress.

## Lead Evaluation

For each lead, determine:

1. Is the firm/investor active and relevant to my startup's sector?
2. Do they invest at our current stage?
3. Is the specific contact relevant (e.g., GP, Partner, Program Director)?
4. What part of the firm's thesis or portfolio overlaps with our startup?

Score each lead from **0–100** based on:

* Investment thesis / sector fit: 30
* Stage fit (e.g., Pre-seed/Seed): 25
* Fund/program relevance (e.g., active fund, relevant accelerator): 15
* Contact relevance (Partner > Analyst): 15
* Geography/Location fit: 10
* Other relevant factors (alumni connection, shared network): 5

Prioritize leads scoring **80+**.

## Outreach

Personalize every email using verified information about the firm, their thesis, and the recipient.

Do not simply replace the firm name in a generic template.
Choose only the strongest relevant parts of the startup's story that align with the investor's focus.
Keep emails concise, founder-oriented, and direct.

## Contact Priority

Prefer decision-makers and people who can write checks or refer strongly:

1. Partner / General Partner / Managing Director
2. Principal / VP
3. Program Director / Accelerator Lead
4. Associate / Analyst
5. EIR / Resident / Alumni who can refer

A senior title alone does not make someone a good target. Consider whether their specific investment focus (e.g., AI, Enterprise, B2B) matches our startup.

## Safety / Accuracy

Never:

* Claim traction, revenue, or metrics we do not have.
* Invent product capabilities.
* Claim a VC is actively investing in our specific niche without evidence.
* Send emails or LinkedIn messages automatically.
* Alter the startup profile without permission.
* Contact anyone externally without explicit approval.

All external communication requires my manual approval and action.

---

## Outreach Workflow (Semi-Automated)

The full pipeline for each lead is:

**Input → Research → Fit assessment → Score → Outreach strategy → Email draft → Approval gate → Send**

### Input

The user provides a target and optionally a person and email. Examples:

```
Target: Sequoia Surge
Person: Rajan
Email: rajan@example.com
```

```
Firm: Nexus Venture Partners
Person: Suvir
Email: suvir@example.com
```

### Step 1 — Research

Use web tools to investigate:

* Official firm website and investment thesis.
* Active funds or accelerator programs.
* Recent investments in similar spaces.
* Person's specific focus areas and board seats.

Save research to `companies/<firm-slug>.md`.

If the firm's stage/thesis cannot be verified, state this clearly.

### Step 2 — Fit Assessment

Use `startup.md` as the source of truth.

Match against: investment thesis, stage, sector, AI/agentic overlap, geographic focus.

### Step 3 — Score

Use the existing scoring system (0–100) from the Lead Evaluation section.

### Step 4 — Outreach Strategy

Before drafting, determine internally:

* The specific ask (funding, intro, mentorship).
* Fit score.
* Strongest thesis overlap (why this specific firm?).
* Strongest startup metric or milestone to mention.
* Appropriate tone (founder-to-investor).
* Reason for contacting this specific person.

### Step 5 — Email Draft

Write a concise, human, and professional cold email.

Include:

* Short introduction (who we are).
* The problem & solution (the hook).
* Relevant traction or milestones.
* Specific reason for contacting this firm/partner.
* Concise request (e.g., a 15-minute call).

Avoid: marketing fluff, excessive flattery, buzzword stuffing, generic AI language.

Generate a clear subject line.

### Step 6 — Save Draft

Save the final draft to `outreach/drafts/<firm>-<person>.md`.

Use YAML frontmatter:

```yaml
---
firm: VC Firm Name
person: Partner Name
email: partner@example.com
role: General Partner
fund_or_program: Fund III
investment_stage: pre-seed
fit_score: 85
status: drafted
subject: "Subject line"
created: YYYY-MM-DD
---
```

Do not overwrite an existing draft without checking first.

### Step 7 — Hard Approval Gate

After research and preparation, **STOP**.

Present:

**Research summary:**

* Firm
* Contact
* Contact relevance
* Thesis/Stage fit
* Fit score
* Key reasoning

**Email preview:**

* Subject
* Complete email body
* Mention if a pitch deck should be attached (as placeholder for now)

Then say:

`Waiting for explicit approval. Use SEND EMAIL to authorize sending.`

Do NOT send at this stage.
Do NOT treat any other response as approval.

### Step 8 — Send (only on `SEND EMAIL`)

Only when the user explicitly issues `SEND EMAIL`:

1. Verify recipient, subject, and body match the approved draft.
2. Send via the configured Gmail MCP/tool integration.
3. If a pitch deck is required, instruct the user to attach it manually (since none is provided yet).
4. If anything changed since approval, stop and request approval again.

After confirmed send:

1. Update `leads.csv` status to `sent` and record the date.
2. Update the draft frontmatter status.
3. Report the send result.

If send fails, do not mark as sent.

## Lead Tracking

### CSV Schema

`leads.csv` fields:

`firm,person,email,role,fund_or_program,investment_stage,sector_fit,fit_score,status,draft_file,sent_date,notes`

### Status Values

* `researched` — research complete, no draft yet.
* `drafted` — email drafted, pending approval.
* `approved` — user approved, ready to send.
* `sent` — Gmail confirmed delivery.
* `replied` — recipient responded.
* `rejected` — user decided not to send.

### Rules

* Add leads when first researched.
* Update status at each workflow step.
* Never mark as `sent` without Gmail confirmation.
* `sent_date` is ISO format, filled only on confirmed delivery.
* `draft_file` is the relative path to the draft.

## Gmail Integration

Gmail sending is handled via **Composio Gmail MCP** through OpenCode.

### Setup (one-time)

```bash
opencode mcp add composio_gmail --url https://mcp.composio.dev/composio/gmail
```

Then authenticate:

```bash
opencode mcp auth composio_gmail
```

See `SETUP.md` for detailed instructions.

### Send Behavior

* Use the Gmail MCP `GMAIL_SEND_EMAIL` tool to send.
* Use the recipient email exactly as provided or verified.
* Never guess an email address.

## Expanded Safety Rules

In addition to the existing safety rules, never:

* Send without explicit `SEND EMAIL` command.
* Guess an email address.
* Fabricate an investment thesis.
* Fabricate contact information.
* Send to multiple recipients unless explicitly specified.
* Automatically follow up.
* Automatically send LinkedIn messages.
* Alter the startup profile without permission.

For multiple leads, each email requires its own approval.

The default is always: **Research → Prepare → Show → Wait → Send only after `SEND EMAIL`.**
