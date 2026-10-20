# governed-agents

AI agents built and governed by AI Governance principles.

This repository documents the AI agents I build and run, together with the way I govern them: what each agent is for, what it can access, what it is allowed to do, where a human stays in the loop, and what risks remain open. Every change to an agent's instructions is versioned here, so the history of each agent is auditable.

I am a Business Analyst specialising in AI Governance, AI change and AIfullness: attention, concentration and self-regulation as core competencies for working with AI. This repository is the practical side of that work. Governance described in policies is easy; governance applied to agents that run every week is the real test.

## Principles

1. **Registered before running.** Every agent has an entry in the [agent registry](REGISTRY.md) before it is trusted with real work.
2. **Least privilege, enforced in Layer 0.** An agent gets only the MCP servers and tools it needs for its purpose, limited by configuration rather than by instructions. Instructions (Layer 1) are a second line of defence, never the only one. Anything broader is recorded as an open finding.
3. **A named human oversight point.** Each agent states where a human reviews, approves or can stop its output.
4. **Nothing published automatically.** Agents prepare; a human decides.
5. **Instructions under version control.** Changes to prompts and instructions go through commits, so they are traceable.
6. **Sanitised for publication.** Public files contain no personal addresses, private links or employer data.

## Structure

```
REGISTRY.md                  Agent registry: one row per agent, plus field definitions
RISK-ACCEPTANCE.md           Documented risk acceptance decisions with review dates
agents/
  AG-001-weekly-content-pipeline/
    README.md                Agent card: purpose, access, oversight, risks, findings
    instructions.md          Sanitised instructions the agent runs on
  AG-002-friday-review/
    README.md
    instructions.md
  AG-003-career-trends/
    README.md
```

## Status

Sprint 1 of 4 (20 Oct – 2 Nov 2026): anatomy of an agent. Registering and reviewing the agents already in use. Later sprints add an agent built in code, evaluations, decision logging and human approval steps.

---

**PL:** Repozytorium dokumentuje agentów AI, których buduję i uruchamiam, oraz sposób, w jaki nimi zarządzam zgodnie z zasadami AI Governance: rejestr, minimalne uprawnienia, wskazany punkt nadzoru człowieka i wersjonowane instrukcje.
