# Agent registry

Last review: 2026-10-26

| ID | Agent | Purpose | Status | Schedule | Autonomy | Human oversight point | Open findings |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [AG-001](agents/AG-001-weekly-content-pipeline/README.md) | Weekly content pipeline | Turns a week of newsletters, own notes and web news into 4 LinkedIn post briefs and 1 article brief | Active | Mondays 07:52 Europe/Warsaw | Default mode: approval gate on | Briefs only; I edit and publish every piece myself | 4 |
| [AG-002](agents/AG-002-friday-review/README.md) | Friday review | Prepares my weekly review of priorities and updates the cockpit document from my answers | Active | Fridays 12:58 Europe/Warsaw | Automatic mode: no approval gate | Edits the cockpit only from my answers in the session | 3 |
| [AG-003](agents/AG-003-career-trends/README.md) | Career trends (#kArIera) | Analyses popular AI videos for career-planning signals and drafts a LinkedIn post | Paused 2026-10-19 | Sundays 07:48 Europe/Warsaw (disabled) | Default mode: approval gate on | Draft only, delivered for review | 1 |
| [AG-004](agents/AG-004-research-pipeline/README.md) | Research-to-publication pipeline | Turns high-quality scientific publications into verified insights and, after my approval, publications | Pilot 2026-10-26: stage 1 run manually once | Saturday scan planned, not yet scheduled | Run by me in a chat session; no scheduled task | Four human gates: select, accept analysis, approve draft, publish | 4 open design items (D-004 resolved) |
| AG-005 | Content pipeline (Python, LinkedIn) | Not yet verified: see open questions below | Draft 2026-10-26: entry opened, not yet checked against code | Not yet verified | Not yet verified | Manual editing by me before publication (owner statement; code check pending) | Not yet assessed |

**Layer 0 summary (2026-10-19):** none of the three agents has a per-tool allowlist on its MCP servers, and all carry servers they do not need. Every safety rule added so far lives in Layer 1 instructions. The current configuration is accepted as is until 2026-11-13: see [RA-2026-001](RISK-ACCEPTANCE.md).

## Detailed entries

Each value states where it can be checked. A value with no source in code, configuration or this repository is not written in; it stays an open question.

### AG-003 Career trends (#kArIera)

| Field | Value | Source |
| --- | --- | --- |
| Purpose | Analyse popular AI videos on YouTube for career-planning signals in IT and draft one LinkedIn post per week | [Agent card](agents/AG-003-career-trends/README.md) |
| Tools | Video-analytics server (vidIQ): video statistics and transcripts. Web search: public market reports. Claude memory: its own trend log. Scheduled-task management server: attached, not needed | Agent card; [RA-2026-001](RISK-ACCEPTANCE.md) (servers attached / needed: 2 / 1) |
| Permissions | Read: video data and transcripts, web pages, its trend log. Write: one Markdown file to me, one log line per trend. No per-tool allowlist, so the video-analytics write tools (upload video, publish Instagram reel) and all scheduled-task tools (create, update, delete, fire) are available. Default permission mode: actions that need approval pause the run. Disabled, so it cannot run at all | Agent card; RA-2026-001 |
| Risks | While disabled: none (R9 in RA-2026-001). On restart: (1) it reads untrusted content (video transcripts) while publishing tools are available, so a crafted transcript could try to trigger an upload or a reel; (2) it could change scheduled tasks, including its own; (3) a factual error or popularity bias could reach the draft. Controls: Layer 0, disabled state and the approval gate; Layer 1, draft-only rule, confidence level per claim, popularity-bias correction; Layer 4, I review every draft. Instructions are not yet in this repository (F-001), so the Layer 1 controls cannot be checked here | RA-2026-001; agent card |
| Owner | Dorota Roszkowska | Agent card |
| Status | Paused | Agent card |
| Pause date | 2026-10-19 | Agent card |
| Pause reason | Focus decision: its audience is individuals planning careers in IT, not the organisations my brand addresses | Agent card |
| Restart conditions | Add sanitised instructions (F-001); detach scheduled-task management; restrict video analytics to read tools if the platform allows. A restart triggers an early review of RA-2026-001 | Agent card; RA-2026-001 |

### AG-005 Content pipeline (Python, LinkedIn)

| Field | Value | Source |
| --- | --- | --- |
| Purpose | Open (Q1, Q4, Q6) | Not yet verified |
| Tools | Open (Q3, Q5) | Not yet verified |
| Permissions | Open (Q5, Q7) | Not yet verified |
| Risks | **Control point: manual editing.** No text produced by the pipeline reaches LinkedIn without being edited by me. Where this edit sits in the flow, and whether the code itself has any publishing path, is not yet verified (Q8). Specific risk scenarios to be written after the code check | Owner statement, 2026-10-26 |
| Owner | Dorota Roszkowska | Owner statement, 2026-10-26 |

Open questions, to be closed by checking the code before 2026-11-02:

- Q1. Is this the "seven-step content pipeline (Python)" previously listed as to be registered? Is it seven agents or seven steps, and what is each one called?
- Q2. Where is the code? It is not in this repository; add a sanitised copy or a link to its source.
- Q3. Which model API and model does each agent call, and where is the API key kept?
- Q4. What does it read: files, URLs, feeds, mail?
- Q5. Does any step write outside its working folder, call the network beyond the model API, or include a publishing library or LinkedIn API?
- Q6. What does the last step produce, in what format and where?
- Q7. How is it run (manually, scheduled) and when did it last run?
- Q8. Where exactly is the manual edit: only on the final text, or also between steps? Does the code pause for approval anywhere?

## To be registered

Agents I have built or run that still need an entry:

- AI Requirements & Compliance Validator (audits Jira requirements)

## Not registrable

- EU AI Act Article 4 readiness assessment agent (Microsoft Copilot Studio): access to the environment was lost before registration, so the agent cannot be documented from its configuration. Recorded here so the gap stays visible.

## Field definitions

| Field | Meaning |
| --- | --- |
| ID | Stable identifier. Never reused, even after an agent is retired. |
| Purpose | One sentence. If it needs two, the agent probably does two jobs. |
| Status | Draft, Active, Paused or Retired, with the date of the last change. A paused agent also records the pause date and reason. |
| Schedule | When it runs, with time zone. On-demand agents say so. |
| Autonomy | Whether its actions wait for human approval or run on their own. A platform setting, so part of Layer 0. |
| Tools | Servers, APIs and libraries the agent can call, including ones attached but not needed. |
| Permissions | What it can read and write, and which layer enforces each limit. |
| Risks | Realistic failure scenarios and the control point that catches each one. |
| Owner | The person accountable for the agent and its changes. |
| Layer 0 | Deterministic constraints enforced outside the model: configuration, permissions, allowlists, code. The model cannot override them. |
| Layer 1 | Instructions. Probabilistic: they work only as long as the model follows them. A control that exists only in Layer 1 is recorded as partially mitigated at best. |
| MCP table | Each attached server with its read and write tools, whether the agent needs them, and which layer enforces the limit. |
| Human oversight point | The exact place where a human reviews, approves or can stop the output. |
| Open findings | Number of known gaps between how the agent runs and the principles in the README, including partially mitigated ones. Details and status on the agent card. |
| Source | Where a registry value can be checked: code, configuration, an agent card or a dated owner statement. |

Each agent card adds: model, data it can read, actions it can take, controls, findings and a change log.
