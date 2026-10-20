# Risk acceptance: RA-2026-001

| Field | Value |
| --- | --- |
| Decision | Accept the current configuration of AG-001, AG-002 and AG-003 without changes |
| Accepted by | Dorota Roszkowska, owner of all three agents |
| Date | 2026-10-20 |
| Review date | 2026-11-13 (after four runs of AG-002), or earlier if a trigger below occurs |
| Status | Active |

## Rationale

The agents are in a learning phase and run on my own data only. No client, employer or third-party data is processed. The decision is to first describe precisely how the agents work and what risks they carry, and only then decide which Layer 0 controls are worth the effort. The risks below are understood, recorded and bounded in time by the review date.

## Current state

| | AG-001 Weekly content pipeline | AG-002 Friday review | AG-003 Career trends |
| --- | --- | --- | --- |
| State | Active, Mondays 07:52 | Active, Fridays 12:58 | Disabled |
| Permission mode | Default: actions that need approval pause the run | Automatic: nothing waits for approval | Default |
| Reads untrusted content | Yes: newsletters, web pages | No: only my own cockpit document | Yes: video transcripts |
| MCP servers attached / needed | 6 / 1 | 7 / 1 | 2 / 1 |
| Per-tool allowlist | None | None | None |

## How the controls work today

| Layer | Role | What is in place |
| --- | --- | --- |
| L0 Deterministic constraints | Decides whether an agent **can** act | Schedule, fresh session per run, no LinkedIn connector, AG-003 disabled, approval gate in default mode |
| L1 Instructions | Decides whether an agent **will** act | Read-only mail use, no publishing, no changes to scheduled tasks, external content treated as data, injection attempts reported |
| Model behaviour | Trained resistance to instructions embedded in content | Real but not auditable |
| L4 Human | Decides whether output **reaches the world** | Every piece of content is edited and published by me |

**Known unknown:** the exact scope of the approval gate in default mode is set by the platform and not visible to me. AG-001 completed six runs that wrote to the planner, memory and files without pausing. The strength of the only Layer 0 barrier on AG-001 is therefore unknown.

## Accepted risks

Likelihood and impact are qualitative judgements, not measurements.

| ID | Scenario | Agent | Likelihood | Impact | Current protection |
| --- | --- | --- | --- | --- | --- |
| R1 | A crafted newsletter makes the agent send or forward mail from my account | AG-001 | Low | High: data leak, mail sent in my name | L1, model behaviour, approval gate of unknown scope |
| R2 | The same mechanism leads to publishing an Instagram reel or YouTube video | AG-001 | Very low (also requires a connected Instagram account in the video-analytics service, not verified) | High: reputation | As R1 |
| R3 | The agent changes scheduled tasks, including its own instructions | AG-001 | Very low | High and silent: may go unnoticed | L1 (since 2026-10-20), approval gate |
| R4 | Memory poisoning: content from a newsletter enters the memory log that my other sessions read | AG-001 | Low | Medium: affects the context of future sessions | L1 |
| R5 | Inbox fallback: the newsletter label is empty, so the agent scans the whole inbox and private content may reach the output file or log | AG-001 | Certain on the next run | Low to medium | L1 (skip mail that looks private) |
| R6 | Factual errors in briefs | AG-001 | Medium | Low | L4: I verify before publishing |
| R7 | A model error leads to an irreversible action with no approval gate | AG-002 | Very low: no untrusted input | High: same tools as R1–R3 | L1 only |
| R8 | Incorrect edit of the cockpit | AG-002 | Low | Low: document keeps version history | L1, version history |
| R9 | Any of the above | AG-003 | None | None | L0: disabled |

**Pattern:** likelihood is low, impact is high, and the two come from different layers. Instructions and model behaviour lower the likelihood. Only Layer 0 can cap the impact, and Layer 0 is thin today. R1–R3 and R7 are rare-but-costly risks, not small ones.

**Detectability:** problems would surface mainly through the summary the agent writes itself. In R1–R3 the same agent would be both the source of the problem and the author of the report. There is no independent log I review routinely.

## Triggers for an early review

Review this acceptance before 2026-11-13 if any of these occurs:

- An agent summary reports a prompt-injection attempt
- An agent takes any action outside its instructions, or a run summary is missing
- A new connector, tool or data source is added to any agent
- Any agent starts processing data that is not mine (client, employer, third party)
- AG-003 is re-enabled
- I start work at the bank (2027): no employer data may reach these agents

## Options considered for the review

Not decided. Listed so the review starts from a known set:

1. Detach unneeded MCP servers (closes most of R2, R3, R7)
2. Per-tool allowlist on Gmail, read and search only (closes R1)
3. Switch AG-002 to default permission mode (reduces R7)
4. Gmail filter that fills the `AI-newsletter` label (closes R5)
5. Independent check of run history after each run (improves detectability)
