# Agent registry

Last review: 2026-10-19

| ID | Agent | Purpose | Status | Schedule | Autonomy | Human oversight point | Open findings |
| --- | --- | --- | --- | --- | --- | --- | --- |
| [AG-001](agents/AG-001-weekly-content-pipeline/README.md) | Weekly content pipeline | Turns a week of newsletters, own notes and web news into 4 LinkedIn post briefs and 1 article brief | Active | Mondays 07:52 Europe/Warsaw | Runs without approval prompts | Briefs only; I edit and publish every piece myself | 3 |
| [AG-002](agents/AG-002-friday-review/README.md) | Friday review | Prepares my weekly review of priorities and updates the cockpit document from my answers | Active | Fridays 12:58 Europe/Warsaw | Runs without approval prompts | Edits the cockpit only from my answers in the session | 2 |
| [AG-003](agents/AG-003-career-trends/README.md) | Career trends (#kArIera) | Analyses popular AI videos for career-planning signals and drafts a LinkedIn post | Paused 2026-10-19 | Sundays 07:48 Europe/Warsaw (disabled) | Runs without approval prompts | Draft only, delivered for review | 1 |

## To be registered

Agents I have built or run that still need an entry:

- EU AI Act Article 4 readiness assessment agent (Microsoft Copilot Studio)
- AI Requirements & Compliance Validator (audits Jira requirements)
- Seven-step content pipeline (Python)

## Field definitions

| Field | Meaning |
| --- | --- |
| ID | Stable identifier. Never reused, even after an agent is retired. |
| Purpose | One sentence. If it needs two, the agent probably does two jobs. |
| Status | Draft, Active, Paused or Retired, with the date of the last change. |
| Schedule | When it runs, with time zone. On-demand agents say so. |
| Autonomy | Whether its actions wait for human approval or run on their own. |
| Human oversight point | The exact place where a human reviews, approves or can stop the output. |
| Open findings | Number of known gaps between how the agent runs and the principles in the README, including partially mitigated ones. Details and status on the agent card. |

Each agent card adds: owner, model, tools and connectors, data it can read, actions it can take, risks, controls, findings and a change log.
