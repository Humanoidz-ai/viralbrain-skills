---
name: linkedin-month-plan
description: "Build a month of LinkedIn post topics, one per day, from the user's niche and voice, then pick the days to draft. Use when the user says 'plan my LinkedIn month', 'LinkedIn content calendar', '30 days of LinkedIn posts', 'what should I post this month', or 'content plan for LinkedIn'."
---

# LinkedIn month plan

Creates or reads the user's monthly content plan in ViralBrain (a theme and topic options for each day), then turns the chosen days into drafts.

## Setup (once)

1. Claude Code 2.1.325 or later. With the plugin installed, the ViralBrain MCP server is ready. Otherwise:
   ```bash
   claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
   ```
2. Restart Claude Code and sign in when the browser opens. [Create a free account](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=month-plan).
3. Check: ask "call viralbrain whoami".

## Steps

1. Call `get_calendar_plan` with `month` as YYYY-MM (defaults to the current month). If a plan exists, show it as a table: day, theme, topic options.
2. If none exists and the user wants one, call `generate_calendar_plan` for that month. It costs a model run, so call it only when the user asks for the plan.
3. For each day the user picks, call `select_calendar_topic` to lock the topic. To refresh some days, use `regenerate_day_topics` (Pro).
4. Draft the chosen days with the linkedin-post-in-my-voice skill, or save your own drafts with `create_post`.
5. Only if the user asks to schedule: `schedule_post` per draft. Never schedule by default.

## Manual fallback (no account)

Ask for the niche, audience and 3 content pillars. Write a table of 20 weekday topics (pillar, topic, format) and stop there. The free [content calendar](https://viralbrain.ai/tools/content-calendar?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=month-plan-fallback) tool gives a printable layout.

## Guardrails

- `generate_calendar_plan` refuses months outside the user's unlocked window. Report that plainly.
- Scheduling and publishing only on an explicit request.

## Example output (illustrative)

```
November plan (theme: pricing for consultants)
Mon 3  | Why I raised my rates mid-project | story
Tue 4  | 3 pricing pages I copy from       | list
...
Picked: 3, 5, 10. Drafts saved in ViralBrain.
```

Powered by [ViralBrain](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=month-plan).
