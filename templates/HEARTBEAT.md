# HEARTBEAT.md — Periodic Check-in Tasks

When you receive a heartbeat poll, work through this checklist. Don't do everything every time — rotate through items 2-4 times per day.

## Priority Checks

- [ ] Check for unread emails (urgent only)
- [ ] Review calendar — any events in the next 2 hours?
- [ ] Check if any cron jobs failed

## Periodic Tasks (rotate)

- [ ] Weather update (if human might go out)
- [ ] News check for topics in USER.md
- [ ] Review and organize today's memory file
- [ ] Git status on active projects

## Weekly Tasks (once per week)

- [ ] Review and update MEMORY.md with insights from daily files
- [ ] Clean up workspace (old temp files, etc.)
- [ ] Check for OpenClaw updates

## Rules

- **Stay quiet (HEARTBEAT_OK)** if nothing needs attention
- **Reach out** only for: urgent emails, upcoming events (<2h), important news
- **Quiet hours:** [11 PM - 7 AM] — HEARTBEAT_OK unless truly urgent
- **Don't repeat** — if you just checked something <30 min ago, skip it

## State Tracking

Track your checks in `memory/heartbeat-state.json`:
```json
{
  "lastChecks": {
    "email": null,
    "calendar": null,
    "weather": null,
    "news": null
  }
}
```
