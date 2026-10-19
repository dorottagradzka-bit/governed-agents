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
| Instructions hidden in a newsletter steer the agent (prompt injection) | The agent cannot publish; mail content treated as data; attempts reported in each run summary; see finding F-001 |

## Open findings

| ID | Finding | Why it matters | Fix | Status |
| --- | --- | --- | --- | --- |
| F-001 | The mail connector exposes write tools (send, forward, delete), not only read tools | Mailbox content is untrusted input; a crafted newsletter could try to make the agent send or forward mail | Instruction-level guardrail: read and search tools only, mail content treated as data, injection attempts reported (2026-10-19). Technical restriction of the connector still to do | Partially mitigated |
| F-002 | The agent reads the whole inbox for 7 days and filters newsletters itself | It sees personal mail it does not need | Dedicated `AI-newsletter` label created (2026-10-19); agent reads the label first and reports when it falls back to the inbox. Mail filter that applies the label still to do | Partially mitigated |
| F-003 | Calendar, Drive, task-database and video-analytics connectors are attached but not used | Unused access widens what a manipulated run could reach | Instruction-level ban on unused connectors (2026-10-19). Detaching them still to do | Partially mitigated |

Instruction-level guardrails are a compensating control: they reduce the risk but rely on the model following them. The findings close when the technical restrictions are in place.

## Change log

| Date | Change |
| --- | --- |
| 2026-09-12 | Created: 14 post proposals per week from mail and newsletters |
| 2026-09-30 | Added independent web search as a third source |
| 2026-10-19 | 4 posts + 1 article per week; GEO rules; regulation names allowed in articles; first-person agent rule; personal-brand context replaces the paused advisory offer |
| 2026-10-19 | Security guardrails after first registry review: read-only mail use, no unused connectors, prompt-injection reporting, newsletters read from a dedicated label |
