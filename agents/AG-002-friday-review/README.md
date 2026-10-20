# AG-002 Friday review

| Field | Value |
| --- | --- |
| Purpose | Prepare my weekly 20-minute review of priorities and update my 90-day cockpit document from my answers |
| Owner | Dorota Roszkowska |
| Status | Active since 2026-10-19; first run 2026-10-23 |
| Schedule | Fridays 12:58 Europe/Warsaw, fresh session each run |
| Model | Claude Opus 5.5 |
| Autonomy | Runs without approval prompts |
| Instructions | [instructions.md](instructions.md) |

## Anatomy

| Layer | This agent |
| --- | --- |
| L0 Deterministic constraints | See the Layer 0 table below |
| L1 Instructions | [instructions.md](instructions.md), including the security section |
| L2 Tools (MCP) | See the MCP table below |
| L3 Memory and state | Fresh session each run; the cockpit document is its only state |
| L4 Outputs and oversight | One message to me; cockpit edits only from my answers in the session |

### Layer 0: deterministic constraints

| Constraint | In place | How it is enforced |
| --- | --- | --- |
| No carry-over between runs | Yes | Each run starts a fresh session |
| Fixed schedule | Yes | Set in the scheduled-task configuration |
| Approval gate for actions | **No** | Automatic permission mode: actions run without waiting for approval |
| Per-tool allowlist on MCP servers | **No** | Tool allowlist for every attached server is empty |
| Only the servers the agent needs | **No** | Seven connector servers attached; one needed (documents) |
| Cannot publish anywhere | **No** | The video-analytics server includes Instagram reel publishing |

### Layer 2: MCP servers and tools

| Server | Read tools | Write tools | Needed | Enforcement today |
| --- | --- | --- | --- | --- |
| Claude Docs | read, query | update, batch, create, delete | Read + update the cockpit | L1 only |
| Scheduled-task management | list tasks | create, update, delete, fire tasks | No | L1 only |
| Gmail | search, read | send, forward, trash and others | No | L1 only |
| Google Calendar | list, get events | create, update, delete events | No | L1 only |
| Google Drive | search, read | create, update, share, trash | No | L1 only |
| Notion | search, fetch | create, update, delete pages | No | L1 only |
| Video analytics (vidIQ) | analytics, search | upload video, publish Instagram reel | No | L1 only |

## What it can read

- My 90-day cockpit document (priorities, milestones, sprint plan, parking list)

## What it can do

- Send me one message with the current state and five review questions
- After I answer: tick milestones, update the next action per workstream, add items to the parking list

## Human oversight point

The agent changes the cockpit only from my answers in the same session. It may not change the goal, the dates or the structure of the document unless I ask. If it cannot read the cockpit, it says so and still asks the five questions.

## Risks and controls

| Risk | Control in place |
| --- | --- |
| The agent rewrites my priorities on its own | Edits limited to three fields and only from my answers |
| A review becomes a chore and gets skipped | Twenty minutes, five fixed questions, state prepared in advance |
| Wellbeing signals get lost in task tracking | Question 5 is an explicit energy and needs check-in |

## Open findings

| ID | Finding | Why it matters | Fix | Status |
| --- | --- | --- | --- | --- |
| F-001 | Mail, calendar, Drive, task-database and video-analytics connectors are attached by default, though the agent needs only the document connector | Least privilege: unused access is risk without benefit | Instruction-level ban on everything except the document tools (2026-10-19). Detaching the connectors still to do | Partially mitigated |
| F-002 | Runs without approval prompts while it can edit the cockpit | An unattended run could change the document if instructions were misread | Accepted risk for the cockpit only: edits depend on my answers in the session. Revisit after four runs (2026-11-13) | Accepted |
| F-003 | Automatic permission mode combined with unneeded high-impact write tools (publish Instagram reels, send mail, change scheduled tasks) | With no approval gate, nothing deterministic stands between a misread instruction and an irreversible action. Input risk is low (it reads only my own document), but the impact would be high | Detach every server except Claude Docs; then automatic mode becomes acceptable | Open |

## Change log

| Date | Change |
| --- | --- |
| 2026-10-19 | Created |
| 2026-10-19 | Security guardrail: document tools only, document content treated as data |
| 2026-10-20 | Layer 0 and MCP review added to the card; finding F-003 opened |
