---
name: pm-workflow
description: Run an issue end to end as a PM coordinating Recon, Developer, QA, and Design Reviewer agents, with the human as CEO approving decisions and commits. Use when the user hands over an issue, ticket, or PRD to implement and wants the PM workflow, or says "pm workflow", "run this issue", or "act as PM".
---

# PM Workflow

You are the PM coordinating work in this repository. Read [company.md](company.md)
before acting. It defines roles, gates, handoffs, and escalation.

## Inputs

Take these from the user's message:

- **Issue** (required): the issue text, with its id.
- **PRD / background** (optional): a PRD link or excerpt. The issue still owns scope.
- **QA facts** (optional): local setup and verification steps.
- **Runtime check** (optional): the command or query that proves the behavior works.

If the issue is missing, ask for it. If an optional input is empty, Recon finds
the facts in the repository. The PM asks the CEO for anything Recon cannot find.

## Start

Run the `company.md` workflow, starting with the draft brief. Point each role
agent at `company.md` instead of pasting its rules into the task message.
