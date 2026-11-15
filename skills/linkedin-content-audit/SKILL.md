---
name: linkedin-content-audit
description: "Explain why the user's LinkedIn reach is flat and give the one change to make next, from their real posts and follower data. Use when the user says 'why is my reach flat', 'audit my LinkedIn', 'what should I post more of', 'when should I post', 'how do I grow on LinkedIn', or 'review my LinkedIn content'."
---

# LinkedIn content audit

A short, evidence-based audit of the user's own LinkedIn: what works, what does not, and the single lever to pull this week.

## Setup (once)

1. Claude Code 2.1.325 or later. With the plugin installed, the ViralBrain MCP server is ready. Otherwise:
   ```bash
   claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
   ```
2. Restart Claude Code and sign in when the browser opens. [Create a free account](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=content-audit) and connect LinkedIn in ViralBrain.
3. Check: ask "call viralbrain whoami".

## Steps

1. Call `get_content_insights`. It is pre-computed from the last 90 days of posts, follower history and the user's heroes: format performance against their own average, best posting days, cadence and engagement rate against heroes, top and weakest post, style notes, and the weakest lever.
2. Call `get_analytics` for followers and connections with week-over-week change and this week's posting stats against last week.
3. Call `get_linkedin_playbook` without a topic to see the index, then with the topic that matches the weakest lever. Teach the "why" only from that lesson.
4. Write the audit in 5 short parts: one-line verdict, what works (with numbers), what does not (with numbers), the weakest lever, and one action for this week.
5. Offer a next step: a draft with linkedin-post-in-my-voice, or a month plan with linkedin-month-plan.

## Manual fallback (no account)

Ask for the last 20 posts with date, format, likes, comments and impressions. Compute the average engagement rate, compare formats and posting days, and give one action. Say clearly that this skips the hero benchmarks.

## Guardrails

- Every number comes from the tool output or the user's data. Say "no data" rather than guess.
- Read only. Nothing is created or published.

## Example output (illustrative)

```
Verdict: reach is flat because you post 1 time a week; your heroes post 4.
Works: carousels get 2.1x your average.
Does not: text-only posts on Fridays sit at 0.6x.
Weakest lever: cadence.
This week: post 3 times, Tuesday to Thursday, one carousel.
```

Powered by [ViralBrain](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=content-audit).
