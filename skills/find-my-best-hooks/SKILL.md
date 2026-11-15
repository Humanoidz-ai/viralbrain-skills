---
name: find-my-best-hooks
description: "Find the user's best-performing LinkedIn hooks and turn the pattern into new hooks. Use when the user says 'find my best hooks', 'which openings work for me', 'what hooks perform best', 'analyse my LinkedIn posts', or 'write hooks like my top posts'."
---

# Find my best hooks

Reads the user's own LinkedIn posts and performance through ViralBrain, names the opening lines that worked, explains the pattern, and drafts new hooks in that pattern.

## Setup (once)

1. Claude Code 2.1.325 or later. With the plugin installed, the ViralBrain MCP server is ready. Otherwise:
   ```bash
   claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
   ```
2. Restart Claude Code and sign in when the browser opens. [Create a free account](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=best-hooks) and connect LinkedIn in ViralBrain so it can read your posts.
3. Check: ask "call viralbrain whoami".

## Steps

1. Call `get_content_insights`. It returns your top and weakest post, format performance against your own average and best posting days, computed from your last 90 days.
2. Call `list_posts` with `state` set to published and `limit` 50, then `get_post` on the strongest few to read their full openings.
3. Pull the first line of each post. Group the strong ones by shape (a number, a confession, a contrarian claim, a question, a story start) and say which shape wins for this user, with the posts as evidence.
4. Call `get_linkedin_playbook` with topic `hooks` for ViralBrain's coaching notes on hooks, and use only what it says when you explain why a hook works.
5. Write 5 new hooks in the winning shape for a topic the user names. Offer to turn the best one into a draft with the linkedin-post-in-my-voice skill.

## Manual fallback (no account)

Ask the user to paste their last 10 posts with likes and comments. Rank by engagement, take the first lines and do steps 3 and 5 by hand. The free [hook generator](https://viralbrain.ai/tools/hook-generator?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=best-hooks-fallback) gives extra variations.

## Guardrails

- Every claim about what works cites the user's own posts or the ViralBrain playbook. No generic "LinkedIn rewards X" claims.
- Read only. This skill creates nothing unless the user asks for a draft.

## Example output (illustrative)

```
Your top 3 posts all open with a number and a cost:
1. "I lost 3 clients in one week. Here is what I changed."
2. ...
Winning shape: number + loss. Your questions as openers sit below your average.
5 new hooks for "pricing": ...
```

Powered by [ViralBrain](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=best-hooks).
