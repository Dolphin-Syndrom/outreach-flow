# Jobhunt Automated Outreach System

## 1. Introduction

This repository contains the configuration and data files for an automated cold-email outreach system. The system uses an AI agent to research targets, calculate fit scores, and write email drafts. The system requires the OpenCode command-line interface and the Composio MCP integration.

## 2. Branches

This repository has two primary branches:

*   **`main` (Default):** This branch contains the configuration for job-hunt outreach. Use this branch to target hiring managers, recruiters, and technical leaders for employment opportunities.
*   **`startup-outreach`:** This branch contains the configuration for startup-related outreach. Use this branch to target venture capital (VC) firms, angel investors, and accelerator programs for startup funding and mentorship.

## 3. System Requirements

To operate this system, you must have the following items:

*   OpenCode version 1.18 or higher.
*   A Composio user account.
*   A Gmail account.
*   The Composio Gmail MCP server installed and authenticated.

## 4. Directory Structure

The `main` branch contains these primary files and directories:

*   `AGENTS.md`: Contains the system rules, lead evaluation criteria, and the primary workflow instructions.
*   `candidate.md`: Contains the structured data about the candidate.
*   `resume.md`: Contains the text version of the candidate resume.
*   `resume.pdf`: Contains the PDF document to attach to outgoing emails.
*   `leads.csv`: The database file that records all lead targets and their current status.
*   `SETUP.md`: The instruction manual to configure the Gmail MCP integration.
*   `companies/`: The directory that stores the output files from the company research phase.
*   `outreach/drafts/`: The directory that stores the generated email drafts before transmission.
*   `.agents/skills/outreach/SKILL.md`: The automation trigger file for OpenCode.

## 5. Operation Procedure

Follow these steps to operate the system on the `main` branch:

1.  Read `SETUP.md` to configure the Gmail connection.
2.  Input a target company and a contact person into the OpenCode interface.
3.  The agent will perform research and generate an email draft.
4.  Examine the research data and the email draft.
5.  Type `SEND EMAIL` in the OpenCode interface to transmit the message.

**WARNING:** The system will not transmit an email until you type the `SEND EMAIL` command.
