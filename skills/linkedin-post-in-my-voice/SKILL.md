---
name: linkedin-post-in-my-voice
description: "Write a LinkedIn post that sounds like the user, from an idea, notes or a link, and save it as a draft. Use when the user says 'write a LinkedIn post in my voice', 'turn this into a LinkedIn post', 'draft a post about', 'sound like me on LinkedIn', or pastes a link and asks for a post about it."
---

# LinkedIn post in my voice

Takes an idea, notes or a URL and returns one LinkedIn post in the user's own voice, saved as a draft in their ViralBrain account. Nothing is published.

## Setup (once)

1. Claude Code 2.1.325 or later. If you installed this repo as a plugin, the ViralBrain MCP server is already configured. Otherwise run:
   ```bash
   claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
   ```
2. Restart Claude Code and sign in when the browser opens. No account yet: [create one free](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=post-in-my-voice). The free plan includes 3 posts a month. Full voice-matched generation (`generate_post`) needs Pro, which starts with a EUR 1, 7-day trial.
3. Check the connection: ask "call viralbrain whoami". It returns your account.

## Steps

1. If the user gave a URL, call `read_link` with it first and use the returned text as raw material. Never write about a page you have not read.
2. Call `list_voices` to get the user's analysed voice and any heroes (creators they follow). Use the user's own voice unless they ask for a hero's style.
3. **Pro users:** call `generate_post` with `idea` (the topic or the `read_link` text), an optional `angle`, and `heroId` if a hero voice was chosen. It voice-matches, runs ViralBrain's anti-slop pass and saves the draft. Show the result.
4. **Free users, or if `generate_post` is refused for the plan:** write the post yourself from the voice notes `list_voices` returned. Then save it with `create_post` (`hook`, `body`, optional `cta` and `topic`). Tell the user the draft is in ViralBrain.
5. Show the post with its hook on its own first line, and say where the draft lives (ViralBrain, Drafts).

## Manual fallback (no account)

Ask the user to paste 3 to 5 of their own past posts. Note their sentence length, opening style, line breaks and sign-off, then write the post to match. Check it with the free [post preview](https://viralbrain.ai/tools/post-preview?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=post-in-my-voice-fallback) to see where "see more" cuts it.

## Guardrails

- Draft only. Never call `publish_post_now` or `schedule_post` unless the user asks in so many words.
- Do not invent numbers, clients or results the user did not give you.

## Example output (illustrative)

```
Hook: I stopped writing LinkedIn posts at night. My reach doubled.
Body: (5 short paragraphs in the user's voice, built from their notes)
CTA: What time do you write?
Saved as a draft in ViralBrain.
```

Powered by [ViralBrain](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=post-in-my-voice).
