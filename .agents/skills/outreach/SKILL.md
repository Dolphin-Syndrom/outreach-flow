---
name: cold-outreach
description: Semi-automated cold email outreach workflow for job hunting. Triggers when the user provides a target company, person, or email for outreach. Handles research, fit scoring, email drafting, approval gating, and Gmail sending via Composio MCP.
---

# Cold Outreach Skill

## Trigger

This skill activates when the user provides a target for outreach. Common patterns:

- `Target: <company>` / `Company: <company>`
- `Person: <name>`
- `Email: <email>`
- Any request to draft a cold email, evaluate a lead, or reach out to a company/person.

## Workflow

Follow the **Outreach Workflow (Semi-Automated)** section in `AGENTS.md` exactly.

The pipeline is:

1. **Research** the company and contact using web tools. Save to `companies/<company-slug>.md`.
2. **Evaluate fit** using `candidate.md` and `resume.md`. Never invent experience.
3. **Score** the lead (0–100) using the Lead Evaluation criteria in `AGENTS.md`.
4. **Plan outreach strategy** internally — determine the strongest angle, tone, and relevant background.
5. **Draft email** (~90–140 words, concise and human). Save to `outreach/drafts/<company>-<person>-<role>.md` with YAML frontmatter.
6. **Add to leads.csv** if not already present. Set status to `drafted`.
7. **Present research and email** for review. State: `Waiting for explicit approval. Use SEND EMAIL to authorize sending.`
8. **STOP.** Do not send until the user explicitly says `SEND EMAIL`.

## On `SEND EMAIL`

1. Verify the draft matches what was approved.
2. Use the Composio Gmail MCP tool (`GMAIL_SEND_EMAIL`) to send.
3. Attempt to attach `resume.pdf` if supported.
4. Update `leads.csv` status to `sent` and record the date.
5. Report the result.

## Key Rules

- Never send without explicit `SEND EMAIL`.
- Never guess email addresses.
- Never fabricate information about the company, contact, or candidate.
- Never exaggerate the candidate's experience.
- Each lead gets its own approval cycle.
- Use only the strongest relevant parts of the candidate's background.
- Personalize every email — do not use generic templates.

## Files

| File | Purpose |
|---|---|
| `candidate.md` | Structured candidate profile |
| `resume.md` | Detailed resume |
| `resume.pdf` | Attachment for emails |
| `leads.csv` | Lead tracking with status lifecycle |
| `companies/<slug>.md` | Company research |
| `outreach/drafts/<company>-<person>-<role>.md` | Email drafts with frontmatter |
| `AGENTS.md` | Full rules and workflow |
| `SETUP.md` | Gmail/Composio setup instructions |
