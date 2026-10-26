# Agent registry

Last review: 2026-10-19

| ID | Agent | Purpose | Status | Schedule | Autonomy | Human oversight point | Open findings |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [AG-001](agents/AG-001-weekly-content-pipeline/README.md) | Weekly content pipeline | Turns a week of newsletters, own notes and web news into 4 LinkedIn post briefs and 1 article brief | Active | Mondays 07:52 Europe/Warsaw | Default mode: approval gate on | Briefs only; I edit and publish every piece myself | 4 |
| [AG-002](agents/AG-002-friday-review/README.md) | Friday review | Prepares my weekly review of priorities and updates the cockpit document from my answers | Active | Fridays 12:58 Europe/Warsaw | Automatic mode: no approval gate | Edits the cockpit only from my answers in the session | 3 |
| [AG-003](agents/AG-003-career-trends/README.md) | Career trends (#kArIera) | Analyses popular AI videos for career-planning signals and drafts a LinkedIn post | Paused 2026-10-19 | Sundays 07:48 Europe/Warsaw (disabled) | Default mode: approval gate on | Draft only, delivered for review | 1 |
| [AG-004](agents/AG-004-research-pipeline/README.md) | Research-to-publication pipeline | Turns high-quality scientific publications into verified insights and, after my approval, publications | Pilot 2026-10-26: stage 1 run manually once | Saturday scan planned, not yet scheduled | Run by me in a chat session; no scheduled task | Four human gates: select, accept analysis, approve draft, publish | 4 open design items (D-004 resolved) |

**Layer 0 summary (2026-10-19):** none of the three agents has a per-tool allowlist on its MCP servers, and all carry servers they do not need. Every safety rule added so far lives in Layer 1 instructions. The current configuration is accepted as is until 2026-11-13: see [RA-2026-001](RISK-ACCEPTANCE.md).

## To be registered

Agents I have built or run that still need an entry:

- AI Requirements & Compliance Validator (audits Jira requirements)
- Seven-step content pipeline (Python)

## Not registrable

- EU AI Act Article 4 readiness assessment agent (Microsoft Copilot Studio): access to the environment was lost before registration, so the agent cannot be documented from its configuration. Recorded here so the gap stays visible.

## Field definitions

| Field | Meaning |
| --- | --- |
| ID | Stable identifier. Never reused, even after an agent is retired. |
| Purpose | One sentence. If it needs two, the agent probably does two jobs. |
| Status | Draft, Active, Paused or Retired, with the date of the last change. |
| Schedule | When it runs, with time zone. On-demand agents say so. |
| Autonomy | Whether its actions wait for human approval or run on their own. A platform setting, so part of Layer 0. |
| Layer 0 | Deterministic constraints enforced outside the model: configuration, permissions, allowlists, code. The model cannot override them. |
| Layer 1 | Instructions. Probabilistic: they work only as long as the model follows them. A control that exists only in Layer 1 is recorded as partially mitigated at best. |
| MCP table | Each attached server with its read and write tools, whether the agent needs them, and which layer enforces the limit. |
| Human oversight point | The exact place where a human reviews, approves or can stop the output. |
| Open findings | Number of known gaps between how the agent runs and the principles in the README, including partially mitigated ones. Details and status on the agent card. |

Each agent card adds: owner, model, tools and connectors, data it can read, actions it can take, risks, controls, findings and a change log.
