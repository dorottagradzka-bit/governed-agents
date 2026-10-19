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

| ID | Finding | Why it matters | Proposed fix |
| --- | --- | --- | --- |
| F-001 | Mail, calendar, Drive, task-database and video-analytics connectors are attached by default, though the agent needs only the document connector | Least privilege: unused access is risk without benefit | Detach every connector except the document connector |
| F-002 | Runs without approval prompts while it can edit the cockpit | An unattended run could change the document if instructions were misread | Acceptable for now, since edits depend on my answers in the session; revisit after four runs |

## Change log

| Date | Change |
| --- | --- |
| 2026-10-19 | Created |
