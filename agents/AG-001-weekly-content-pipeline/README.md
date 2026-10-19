# AG-001 Weekly content pipeline

| Field | Value |
| --- | --- |
| Purpose | Turn a week of AI newsletters, my own notes and independent web news into 4 LinkedIn post briefs and 1 LinkedIn article brief, written for GEO (citability in AI answer engines) |
| Owner | Dorota Roszkowska |
| Status | Active since 2026-09-12; instructions revised 2026-10-19 |
| Schedule | Mondays 07:52 Europe/Warsaw, fresh session each run |
| Model | Claude Sonnet 5 |
| Autonomy | Runs without approval prompts |
| Instructions | [instructions.md](instructions.md) |

## What it can read

- My mailbox: notes I send to myself and AI newsletters from the last 7 days
- Public web pages through search
- My editorial rules and the workflow's own log in Claude memory

## What it can do

- Write 5 briefs into my content planner, plus 2–3 ideas into a backlog
- Send me a Markdown file with all 14 proposals and the ranking
- Append one log entry about the run to Claude memory

## Human oversight point

The agent produces briefs, not posts. I rewrite each brief in my own words, verify flagged facts at the primary source and publish manually. Nothing reaches LinkedIn without me.

## Risks and controls

| Risk | Control in place |
| --- | --- |
| A wrong fact from a newsletter ends up in a post | Every factual claim is flagged for verification at the primary source; newsletters are never treated as final sources |
| Content claims experience I do not have | Rule: first-person statements about agents only for what I actually built and documented |
| Generic, low-value AI writing | Explicit anti-slop rules, one thesis per piece, briefs instead of finished text |
| Instructions hidden in a newsletter steer the agent (prompt injection) | Partial: the agent cannot publish; see finding F-001 |

## Open findings

| ID | Finding | Why it matters | Proposed fix |
| --- | --- | --- | --- |
| F-001 | The mail connector exposes write tools (send, forward, delete), not only read tools | Mailbox content is untrusted input; a crafted newsletter could try to make the agent send or forward mail | Restrict the connector to read and search tools for this agent |
| F-002 | The agent reads the whole inbox for 7 days and filters newsletters itself | It sees personal mail it does not need | Use a dedicated label or sender filter so only relevant mail is in scope |
| F-003 | Calendar, Drive and video-analytics connectors are attached but not used | Unused access widens what a manipulated run could reach | Detach connectors the instructions do not use |

## Change log

| Date | Change |
| --- | --- |
| 2026-09-12 | Created: 14 post proposals per week from mail and newsletters |
| 2026-09-30 | Added independent web search as a third source |
| 2026-10-19 | 4 posts + 1 article per week; GEO rules; regulation names allowed in articles; first-person agent rule; personal-brand context replaces the paused advisory offer |
