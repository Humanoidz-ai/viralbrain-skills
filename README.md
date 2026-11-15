# ViralBrain skills for Claude Code

Five free skills for LinkedIn. Each one does a single job end to end and runs on the [ViralBrain](https://viralbrain.ai/?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=readme-intro) MCP server, which reads your real posts, voice and analytics. Each skill also has a manual fallback that works without an account.

| Skill | What it does | Works on the free plan |
|---|---|---|
| [linkedin-post-in-my-voice](skills/linkedin-post-in-my-voice/SKILL.md) | Writes a post in your voice from an idea, notes or a link, saved as a draft | Yes (3 posts a month); voice-matched generation needs Pro |
| [find-my-best-hooks](skills/find-my-best-hooks/SKILL.md) | Finds the openings that worked for you and writes 5 more in that shape | Yes |
| [repurpose-blog-to-linkedin-posts](skills/repurpose-blog-to-linkedin-posts/SKILL.md) | Turns one article, video or Reddit thread into 5 posts with different angles | Partly; 5 generated posts need Pro |
| [linkedin-content-audit](skills/linkedin-content-audit/SKILL.md) | Explains why reach is flat and gives one action for this week | Yes |
| [linkedin-month-plan](skills/linkedin-month-plan/SKILL.md) | Builds a month of daily topics and turns picked days into drafts | Yes; refreshing days needs Pro |

Nothing here publishes or schedules a post unless you ask for it.

## Install

Tested with Claude Code 2.1.325.

As a plugin (skills and the MCP server in one step):

```bash
claude plugin marketplace add Humanoidz-ai/viralbrain-skills
claude plugin install viralbrain-skills@viralbrain-skills
```

Or by hand:

```bash
git clone https://github.com/Humanoidz-ai/viralbrain-skills.git
cp -R viralbrain-skills/skills/* ~/.claude/skills/
claude mcp add --transport http viralbrain https://viralbrain.ai/api/mcp
```

Restart Claude Code. The first ViralBrain call opens a browser to sign in (OAuth, no API key to paste). Check the connection by asking "call viralbrain whoami".

Codex users can connect the same server with `codex mcp add viralbrain --transport http --url https://viralbrain.ai/api/mcp`.

## Plans

- Free: 3 hero profiles and 3 posts a month. [Sign up](https://viralbrain.ai/auth/signup?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=readme-plans).
- Pro (EUR 39 a month) and Premium (EUR 69 a month) both start with a EUR 1, 7-day trial. See [pricing](https://viralbrain.ai/pricing?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=readme-plans).

More about the server and its tools: [LinkedIn MCP server](https://viralbrain.ai/linkedin-mcp-server?utm_source=github&utm_medium=skill&utm_campaign=viralbrain-skills&utm_content=readme-mcp).

## Privacy

The skills hold no keys and no personal data. Sign-in uses OAuth with viralbrain.ai, and every tool call is scoped to your own account.

## Note for David

Walid set this up on 2026-11-15 as part of free public skills for each product. The skills only call the existing hosted MCP server at `https://viralbrain.ai/api/mcp` and link to `/auth/signup`, `/pricing` and free `/tools/*` pages, all with `utm_campaign=viralbrain-skills` so signups from here show up in PostHog. No app code changed. Plan facts come from `app/lib/constants/plans.ts` as summarised in the repo's money-page-seo product facts. If you would rather not publish this under the Humanoidz-ai org, it can be moved or made private.

## License

MIT. See [LICENSE](LICENSE).
