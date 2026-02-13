# Mayagen Mission Control — Coordinator Guide

This document extends AGENTS.md with specifics for running the Mayagen.ai squad.

## Workspace Layout

- Shared root: `mayagen/`
- Tasks: `mayagen/tasks/INBOX.md`, `mayagen/tasks/ACTIVE.md`, `mayagen/tasks/DONE.md`
- Agent SOULs: `mayagen/agents/<agent>/SOUL.md`
- Reports: `mayagen/reports/*.md`

## Agents (Initial)

- `agent:main:main` — Vision / Jarvis (Coordinator)
- `agent:seo-growth:main` — Vision (SEO & Growth Analyst)
- `agent:content-lead:main` — Loki (Content & Messaging Lead)
- `agent:product-ux:main` — Shuri (Product & UX Analyst)

## Coordinator Responsibilities

When acting as coordinator for Mayagen:

1. **Review tasks**
   - Read `mayagen/tasks/INBOX.md` and `ACTIVE.md`.
   - Clarify tasks if they are vague; add context/links to reports.

2. **Assign work**
   - Decide which specialist agent should own each task.
   - Use their names/handles in Owners field (e.g. `@seo-growth`).
   - Optionally spawn sub-sessions with a focused brief.

3. **Track progress**
   - When agents produce new reports or docs, link them back into the task.
   - Move tasks from INBOX → ACTIVE → DONE as appropriate.

4. **Report to SK**
   - Summarize important progress in plain language.
   - Highlight blockers and decisions needed.

## Agent Behavior (Specialists)

On wakeup (heartbeat) each specialist should:

1. Read `memory/WORKING.md` (their own current focus).
2. Scan `mayagen/tasks/ACTIVE.md` for tasks they own.
3. If none, scan `mayagen/tasks/INBOX.md` for tasks matching their skills.
4. Do a reasonable slice of work (not everything at once) and:
   - Update the relevant task file (status, checkboxes, notes).
   - Write outputs to an appropriate report/doc file.
5. If nothing needs their attention, reply `HEARTBEAT_OK`.

This is the Mayagen version of "Mission Control" from the Mission Control article.
