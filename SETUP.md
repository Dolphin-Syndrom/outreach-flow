# Startup Outreach Workflow — Setup Guide

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

1. You provide a target VC firm, accelerator, or investor.
2. The agent researches their thesis, evaluates fit against your `startup.md`, and drafts an email.
3. The agent saves the draft and presents it for review.
4. You review and say `SEND EMAIL` to authorize.
5. The agent sends via the Gmail MCP tool.

## Project Structure (Startup Branch)

```
jobhunt/
├── AGENTS.md              # Agent rules and workflow for investors
├── SETUP.md               # This file
├── startup.md             # Your startup details & metrics
├── leads.csv              # Investor lead tracking
├── companies/             # VC/Firm research files
│   └── <firm-slug>.md
└── outreach/
    └── drafts/            # Email drafts
        └── <firm>-<person>.md
```

## Notes

- All emails require explicit `SEND EMAIL` approval before sending.
- The agent never sends automatically or guesses email addresses.
- If you intend to attach a pitch deck or one-pager, you must do so manually through Gmail for now, as no standard file is provided yet.
