# Setting Up Automated Daily Briefings

Get a morning briefing delivered to your Telegram every day — weather, news, tasks, and more.

---

## Option 1: Cron Job (Recommended)

OpenClaw supports cron-style scheduled tasks that run independently of your main session.

### Step 1: Create the Cron Job

Ask your OpenClaw (via Telegram or canvas):

```
Set up a daily cron job at 8:00 AM EST that sends me a morning brief with:
1. Weather in [YOUR CITY]
2. Top AI/tech news headlines
3. Any calendar events today
4. Tasks I should focus on
```

OpenClaw will create the cron configuration for you.

### Step 2: Manual Configuration

If you prefer to configure it manually, create a cron job config file. See [example config](../examples/cron-daily-brief.json).

Place cron configs in your OpenClaw cron directory (check your `openclaw.json` for the path).

### Step 3: Verify

After setting up, ask your OpenClaw:
```
List all my cron jobs
```

Or trigger a test run:
```
Run my daily brief now as a test
```

---

## Option 2: Heartbeat-Based

Instead of a cron job, you can add the brief to your `HEARTBEAT.md`:

```markdown
## Morning Brief (8:00-9:00 AM only)
If current time is between 8:00-9:00 AM and no brief sent today:
- [ ] Send morning brief with weather, news, and tasks
- [ ] Log brief as sent in heartbeat-state.json
```

**Pros:** Simpler setup, uses existing heartbeat infrastructure
**Cons:** Less precise timing (depends on heartbeat interval), uses main session tokens

---

## Customization Ideas

- **Add stock prices** for tickers you follow
- **Include GitHub notifications** if you have the github skill
- **Add email summary** if you have the himalaya skill
- **Weather-based suggestions** ("It's sunny — good day for a walk")
- **Weekly version** with week-in-review on Mondays

---

## Troubleshooting

- **Brief not firing:** Check that the gateway is running and the daemon is installed
- **Wrong timezone:** Verify timezone in your `openclaw.json` config
- **Missing data:** Ensure web_search (Brave API) is configured for news lookups
