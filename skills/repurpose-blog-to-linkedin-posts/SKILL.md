---
name: repurpose-blog-to-linkedin-posts
description: "Turn one blog post, article, YouTube video or Reddit thread into 5 different LinkedIn posts, each with its own angle, saved as drafts. Use when the user says 'repurpose this blog', 'turn this article into LinkedIn posts', 'make 5 posts from this', 'repurpose this video for LinkedIn', or pastes a URL and asks for several posts."
---

# Repurpose a blog into 5 LinkedIn posts

Reads the real content behind a URL, picks 5 distinct angles, and writes 5 LinkedIn posts saved as drafts in ViralBrain. Nothing is published.

## Setup (once)

1. Claude Code 2.1.325 or later. With the plugin installed, the ViralBrain MCP server is ready. Otherwise:
   ```bash
   claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
   ```
2. Restart Claude Code and sign in when the browser opens. [Create a free account](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=repurpose-blog). Free covers 3 posts a month; 5 voice-matched posts need Pro (EUR 1, 7-day trial).
3. Check: ask "call viralbrain whoami".

## Steps

1. Call `read_link` with the URL. It returns the article text, the YouTube transcript or the Reddit thread with top comments. Stop if it returns nothing usable and ask for the text.
2. Pick 5 angles from the content that do not overlap, for example: the main lesson, one surprising number, a mistake to avoid, a short how-to, and a personal take. Show the 5 angles to the user in one line each.
3. **Pro:** call `generate_post` 5 times with `idea` set to the source text and `angle` set to one angle each. Each call saves a draft.
4. **Free, or when the quota runs out:** write the remaining posts yourself in the user's voice (call `list_voices` for their voice notes) and save each with `create_post` (`hook`, `body`, optional `cta`, `topic` set to the source title).
5. Optionally call `add_context` to save the source summary in the user's ViralBrain knowledge base so later posts can cite it.
6. List the 5 drafts with their hooks.

## Manual fallback (no account)

Paste the article text. Do steps 2 and 4 in the chat and give the 5 posts as text. Check each with the free [post preview](https://viralbrain.ai/tools/post-preview?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=repurpose-blog-fallback).

## Guardrails

- Every fact in a post must come from the source. Credit the author when the post leans on someone else's work.
- Draft only. Never publish or schedule unless asked.

## Example output (illustrative)

```
Source: "How we cut onboarding time in half" (1,800 words)
1. Lesson: The fastest onboarding step is the one you delete.
2. Number: 11 steps became 5. Here is what we cut.
3. Mistake: We automated the wrong step first.
4. How-to: A 3-question test for every onboarding step.
5. Take: Most onboarding is for the team, not the user.
5 drafts saved in ViralBrain.
```

Powered by [ViralBrain](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=repurpose-blog).
