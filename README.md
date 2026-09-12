# Startup Outreach System

## 1. Introduction

This repository branch (`startup-outreach`) contains the configuration and data files for an automated cold-email outreach system tailored for founders. The system uses an AI agent to research investors, calculate fit scores, and write email drafts for startup funding and mentorship. The system requires the OpenCode command-line interface and the Composio MCP integration.

## 2. Branches

This repository has two primary branches:

*   **`startup-outreach` (Current):** This branch contains the configuration for startup-related outreach. Use this branch to target venture capital (VC) firms, angel investors, corporate labs, and accelerator programs.
*   **`main`:** This branch contains the configuration for job-hunt outreach. Use that branch to target hiring managers and recruiters for employment opportunities.

## 3. System Requirements

To operate this system, you must have the following items:

*   OpenCode version 1.18 or higher.
*   A Composio user account.
*   A Gmail account.
*   The Composio Gmail MCP server installed and authenticated.

## 4. Directory Structure

The `startup-outreach` branch contains these primary files and directories:

*   `AGENTS.md`: Contains the system rules, investor evaluation criteria, and the primary workflow instructions.
*   `startup.md`: Contains the structured data about your startup (metrics, stage, problem, solution, and the "ask").
*   `leads.csv`: The database file that records all investor and program targets and their current status.
*   `SETUP.md`: The instruction manual to configure the Gmail MCP integration.
*   `companies/`: The directory that stores the output files from the firm/investor research phase.
*   `outreach/drafts/`: The directory that stores the generated email drafts before transmission.
*   `.agents/skills/outreach/SKILL.md`: The automation trigger file for OpenCode.

## 5. Operation Procedure

Follow these steps to operate the system on the `startup-outreach` branch:

1.  Read `SETUP.md` to configure the Gmail connection.
2.  Input a target VC firm, accelerator, or investor into the OpenCode interface.
3.  The agent will perform research and generate an email draft.
4.  Examine the research data and the email draft.
5.  Type `SEND EMAIL` in the OpenCode interface to transmit the message.

**WARNING:** The system will not transmit an email until you type the `SEND EMAIL` command. If you must send a pitch deck, attach it manually before or after transmission, as the agent does not attach documents automatically in this branch.
