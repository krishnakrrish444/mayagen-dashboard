# Mayagen Mission Control — Agent Roster

Initial agents:

- `agent:main:main` — Vision / Jarvis (Coordinator)
- `agent:seo-growth:main` — Vision (SEO & Growth Analyst)
- `agent:content-lead:main` — Loki (Content & Messaging Lead)
- `agent:product-ux:main` — Shuri (Product & UX Analyst)

Each agent has:
- A SOUL file under `mayagen/agents/<agent>/SOUL.md`
- Access to the shared task list under `mayagen/tasks/`
- Access to Mayagen reports under `mayagen/reports/`

Heartbeat cron jobs (to be configured next) will wake these agents periodically to:
- Check for tasks assigned to them
- Do a slice of work
- Update task files and their own WORKING.md
