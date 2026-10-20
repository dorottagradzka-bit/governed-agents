# AG-003 Career trends (#kArIera)

| Field | Value |
| --- | --- |
| Purpose | Analyse popular AI videos on YouTube for career-planning signals in IT and draft one LinkedIn post per week |
| Owner | Dorota Roszkowska |
| Status | Paused 2026-10-19 (focus decision: its audience is individuals planning careers, not the organisations my brand addresses) |
| Schedule | Sundays 07:48 Europe/Warsaw, disabled |
| Model | Claude Sonnet 5 |
| Autonomy | Default permission mode: an action that needs approval pauses the run (corrected 2026-10-19) |

## Layer 0 and MCP in brief

| Item | State |
| --- | --- |
| Disabled | Yes: the strongest deterministic constraint, the agent cannot run |
| Servers attached | Video analytics (needed for read tools), scheduled-task management (not needed) |
| Per-tool allowlist | None: the video-analytics write tools (upload, publish Instagram reel) are available |
| Before any restart | Detach scheduled-task management; restrict video analytics to read tools if the platform allows |

## What it can read

- Video statistics and transcripts through a video-analytics connector
- Public market reports through web search
- Its own trend log in Claude memory

## What it can do

- Send me a Markdown file with research, analysis and one draft post
- Append one line per trend to its log

## Human oversight point

Draft only. Nothing is published or produced as video automatically.

## Notable design choice

The agent keeps a trend log across weeks and labels each theme as new, confirmed or fading. A single week of popular videos is weak evidence; repetition over time is the signal. The instructions also require it to correct for YouTube popularity bias and to state a confidence level for every claim.

## Open findings

| ID | Finding | Why it matters | Proposed fix |
| --- | --- | --- | --- |
| F-001 | Instructions not yet added to this repository | A paused agent should still be fully documented before it can be restarted | Add sanitised instructions before any restart |

## Change log

| Date | Change |
| --- | --- |
| 2026-09-10 | Created |
| 2026-10-19 | Paused |
