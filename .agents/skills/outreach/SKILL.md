---
name: startup-outreach
description: Semi-automated cold email outreach workflow for startups targeting VCs, angels, and accelerators. Triggers when the user provides a target firm, person, or program. Handles research, fit scoring, email drafting, approval gating, and Gmail sending via Composio MCP.
---

# Startup Outreach Skill

## Trigger

This skill activates when the user provides a target for startup funding or program outreach. Common patterns:

- `Target: <firm>` / `Firm: <name>` / `VC: <name>`
- `Person: <name>` / `Partner: <name>`
- `Program: <name>` / `Accelerator: <name>`
- `Email: <email>`
- Any request to draft a cold email, evaluate an investor lead, or reach out to a VC/program.

## Workflow

Follow the **Outreach Workflow (Semi-Automated)** section in `AGENTS.md` exactly.

The pipeline is:

1. **Research** the firm/program and contact using web tools. Save to `companies/<firm-slug>.md`.
2. **Evaluate fit** using `startup.md`. Never invent traction or metrics.
3. **Score** the lead (0–100) using the Lead Evaluation criteria in `AGENTS.md` (focusing on thesis/stage fit).
4. **Plan outreach strategy** internally — determine the strongest hook, tone (founder-to-investor), and ask.
5. **Draft email** (concise, direct). Save to `outreach/drafts/<firm>-<person>.md` with YAML frontmatter.
6. **Add to leads.csv** if not already present. Set status to `drafted`.
7. **Present research and email** for review. State: `Waiting for explicit approval. Use SEND EMAIL to authorize sending.`
8. **STOP.** Do not send until the user explicitly says `SEND EMAIL`.

## On `SEND EMAIL`

1. Verify the draft matches what was approved.
2. Use the Composio Gmail MCP tool (`GMAIL_SEND_EMAIL`) to send.
3. If a pitch deck is expected, instruct the user to attach it manually (as `pitch_deck.pdf` is not yet available).
4. Update `leads.csv` status to `sent` and record the date.
5. Report the result.

## Key Rules

- Never send without explicit `SEND EMAIL`.
- Never guess email addresses.
- Never fabricate information about the firm, contact, or startup metrics.
- Each lead gets its own approval cycle.
- Use only the most relevant traction/metrics that fit the investor's thesis.
- Personalize every email — do not use generic templates.

## Files

| File | Purpose |
|---|---|
| `startup.md` | Core startup details, metrics, and ask |
| `leads.csv` | Lead tracking with status lifecycle (VC schema) |
| `companies/<slug>.md` | Firm/Investor research |
| `outreach/drafts/<firm>-<person>.md` | Email drafts with frontmatter |
| `AGENTS.md` | Full rules and workflow |
| `SETUP.md` | Gmail/Composio setup instructions |
