# Outreach Workflow — Setup Guide

## Prerequisites

- [OpenCode](https://github.com/opencode-ai/opencode) v1.18+ installed
- A Composio account (free tier: [dashboard.composio.dev](https://dashboard.composio.dev))
- A Gmail account for sending

## 1. Add Gmail MCP to OpenCode

Run this in your terminal:

```bash
opencode mcp add composio_gmail --url https://mcp.composio.dev/composio/gmail
```

## 2. Authenticate Gmail

```bash
opencode mcp auth composio_gmail
```

This opens a browser window where you authorize Composio to access your Gmail account. You only need to do this once.

## 3. Verify

```bash
opencode mcp list
```

You should see `composio_gmail` listed and connected.

## 4. Usage

Once configured, the agent can send emails through OpenCode using the Composio Gmail tools. The workflow is:

1. You provide a target company and contact.
2. The agent researches, evaluates fit, and drafts an email.
3. The agent saves the draft and presents it for review.
4. You review and say `SEND EMAIL` to authorize.
5. The agent sends via the Gmail MCP tool.

## Project Structure

```
jobhunt/
├── AGENTS.md              # Agent rules and workflow
├── SETUP.md               # This file
├── candidate.md           # Your structured profile
├── resume.md              # Resume in markdown
├── resume.pdf             # Resume for attachment
├── leads.csv              # Lead tracking
├── companies/             # Company research files
│   └── <company-slug>.md
└── outreach/
    └── drafts/            # Email drafts
        └── <company>-<person>-<role>.md
```

## Notes

- All emails require explicit `SEND EMAIL` approval before sending.
- The agent never sends automatically or guesses email addresses.
- Resume attachment depends on Composio Gmail tool support.
- If attachment is not supported, the agent will remind you to attach manually.
