# AG-001 Weekly content pipeline

| Field | Value |
| --- | --- |
| Purpose | Turn a week of AI newsletters, my own notes and independent web news into 4 LinkedIn post briefs and 1 LinkedIn article brief, written for GEO (citability in AI answer engines) |
| Owner | Dorota Roszkowska |
| Status | Active since 2026-09-12; instructions revised 2026-10-19 |
| Schedule | Mondays 07:52 Europe/Warsaw, fresh session each run |
| Model | Claude Sonnet 5 |
| Autonomy | Default permission mode: an action that needs approval pauses the run (corrected 2026-10-19; earlier recorded as running without approval) |
| Instructions | [instructions.md](instructions.md) |

## Anatomy

| Layer | What it is | This agent |
| --- | --- | --- |
| L0 Deterministic constraints | Limits enforced outside the model by configuration; the model cannot override them | See the Layer 0 table below |
| L1 Instructions | Prompt-level rules; probabilistic, rely on the model following them | [instructions.md](instructions.md), including the security section |
| L2 Tools (MCP) | Servers and individual tools the agent can call | See the MCP table below |
| L3 Memory and state | What persists between runs | Fresh session each run; reads editorial rules and appends to its own log in Claude memory |
| L4 Outputs and oversight | What it produces and who approves it | Briefs in the planner and a Markdown file; I edit and publish manually |

### Layer 0: deterministic constraints

| Constraint | In place | How it is enforced |
| --- | --- | --- |
| Cannot publish to LinkedIn | Yes | No LinkedIn connector exists in the run |
| Cannot publish to Instagram or YouTube | **No** | The attached video-analytics server includes tools that upload videos and publish Instagram reels; see F-004 |
| No carry-over between runs | Yes | Each run starts a fresh session |
| Fixed schedule | Yes | Set in the scheduled-task configuration |
| Approval gate for actions that need it | Yes | Default permission mode pauses the run |
| Per-tool allowlist on MCP servers | **No** | Tool allowlist for every attached server is empty, which means all tools of each server are available |
| Only the servers the agent needs | **No** | Six connector servers attached; one needed (mail). Memory, planner and web search are built-in platform tools |

### Layer 2: MCP servers and tools

| Server | Read tools | Write tools | Needed | Enforcement today |
| --- | --- | --- | --- | --- |
| Gmail | search, get thread, get message | send, reply, forward, drafts, trash, labels, spam | Read only | L1 only (instructions) |
| Claude memory | read | append, write, delete | Read + append to own log | L1 only |
| Content planner (artifact data) | query | set, update, delete | Read + write own week | L1 only |
| Web search and fetch | search, fetch | none | Yes | n/a |
| Scheduled-task management | list tasks | create, update, delete, fire tasks | **No** | L1 only (added 2026-10-20); see F-004 |
| Google Calendar | list, get events | create, update, delete events | No | L1 only |
| Google Drive | search, read | create, update, share, trash | No | L1 only |
| Notion | search, fetch | create, update, delete pages | No | L1 only |
| Video analytics (vidIQ) | analytics, search | upload video, publish Instagram reel, reply to comments | No | L1 only |

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

| F-004 | Two attached servers carry high-impact write tools the agent never needs: scheduled-task management (create, change or delete scheduled tasks, including this one) and video analytics (upload videos, publish Instagram reels) | A manipulated run could change its own instructions or schedule, or publish content under my name, which breaks principle 4 | Detach both servers. Until then the approval gate in default permission mode is the only Layer 0 barrier | Open |

Instruction-level guardrails are a compensating control: they reduce the risk but rely on the model following them. The findings close when the technical restrictions are in place.

## Change log

| Date | Change |
| --- | --- |
| 2026-09-12 | Created: 14 post proposals per week from mail and newsletters |
| 2026-09-30 | Added independent web search as a third source |
| 2026-10-19 | 4 posts + 1 article per week; GEO rules; regulation names allowed in articles; first-person agent rule; personal-brand context replaces the paused advisory offer |
| 2026-10-19 | Security guardrails after first registry review: read-only mail use, no unused connectors, prompt-injection reporting, newsletters read from a dedicated label |
| 2026-10-20 | Layer 0 and MCP review added to the card. Instruction ban on scheduled-task management and on publishing anywhere. Autonomy record corrected to default permission mode |
