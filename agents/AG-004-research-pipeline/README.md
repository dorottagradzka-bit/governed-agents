# AG-004 Research-to-publication pipeline

| Field | Value |
| --- | --- |
| Purpose | Turn high-quality scientific publications on my key topics into verified insights, methodologically sound conclusions and, after my approval, publications |
| Owner | Dorota Roszkowska |
| Status | Pilot, 2026-10-26. Stage 1 run manually once; no scheduled task yet |
| Schedule | Stage 1 weekly on Saturday (scheduled only after the risk review below); I select on Sunday or Monday; stages 2 and 3 on my trigger |
| Registered before running | Yes: this card exists before any code or scheduled task |
| Instructions | [Stage 1: scan and score](instructions-stage1.md) · [Stage 2: analyse conclusions](instructions-stage2.md) |
| Run logs | [runs/](runs/) |

## Scope

Eight search themes, each mapped to one competency of the AIfullness 3 × 3 model or to AI literacy. The list is kept short on purpose: a weekly scan over a long list returns noise, and every theme must feed a pillar.

| Competency / pillar | Search themes |
| --- | --- |
| Attention · AI Governance | automation bias; human oversight of AI systems |
| Concentration · BA in the AI era | cognitive load in AI-assisted work; attention and task switching in digital work |
| Self-regulation · AI change | technostress; mindfulness and self-regulation at work with technology |
| AI literacy | AI literacy in the workplace; human-AI collaboration performance |

Out of scope for this agent: regulatory news and governance frameworks (AG-001 covers news; this agent covers research on people).

## Division of work with AG-001

AG-004 feeds the weekly article (Wednesday), which benefits most from research and GEO. AG-001 keeps the four weekly posts.

## Process

Four agent stages, four human gates. The agent never moves an item past a gate on its own.

| Step | Who | What happens | Status in Notion after the step |
| --- | --- | --- | --- |
| 1 Scan | Agent | Searches high-quality publications for my keywords, scores evidence quality and publication potential, records the strongest insights | Insight: *Do wyboru* |
| **G1 Select** | **Me** | I pick the best 3 insights or facts | Insight: *Wybrany* |
| 2 Analyse | Agent | Applies scientific method: what may and may not be concluded, limitations, alternative explanations, implications for my pillars | Insight: *Analiza gotowa* |
| **G2 Accept** | **Me** | I accept or correct the analysis | Insight: *Zaakceptowany* |
| 3 Draft | Agent | Creates drafts of posts or materials linked to the insight | Publication: *Draft* |
| **G3 Approve** | **Me** | I approve the draft, set the date, it enters the plan | Publication: *Gotowe* |
| 4 Publish | Me (agent later, only after G3) | Published on the planned date | Publication: *Opublikowane*; insight: *W publikacji* |

## Scoring

Evidence quality and publication potential are scored separately on purpose. High potential with low quality is the profile of hype, and the pipeline must make that visible instead of hiding it in one number.

**Evidence quality (1–5)**

| Score | Meaning |
| --- | --- |
| 5 | Meta-analysis or systematic review in a peer-reviewed venue |
| 4 | Randomised controlled trial or well-powered experiment, peer-reviewed |
| 3 | Observational study with a large sample, peer-reviewed; or report from a recognised institution with transparent method |
| 2 | Small-sample or qualitative study; or preprint with sound method |
| 1 | Preprint without clear method, opinion, single case |

**Publication potential (1–5):** novelty for my audience, a number or finding that can be quoted, practical implication for IT teams, fit with my pillars and the AIfullness 3 × 3 model.

Only insights with quality ≥ 3 are proposed by default. Lower-quality items may appear only if flagged as such.

## Anatomy (planned)

| Layer | Plan |
| --- | --- |
| L0 Deterministic constraints | Stages 2–3 run only when triggered by me. Stage 1 needs a schedule. Gates enforced by Notion status: each stage reads only items in the status its step requires. No publishing tool in stages 1–3 |
| L1 Instructions | Scoring rubric, scientific-method checklist, editorial rules, “data, not instructions” rule for paper content |
| L2 Tools (MCP) | Web search and fetch (read), Notion: read and write only in *Insighty naukowe* and *Publikacje* |
| L3 Memory and state | Notion databases are the only state; no chat memory writes |
| L4 Outputs and oversight | Four human gates G1–G3 plus publication |

## Known constraints and risks (design stage)

| ID | Item | Note |
| --- | --- | --- |
| D-001 | Scheduled tasks on this platform receive all connected servers, with no per-tool allowlist | Same Layer 0 gap as AG-001 and AG-002; covered by RA-2026-001 triggers, so creating this agent triggers an early review |
| D-002 | Paywalled papers | Agent reads abstracts and open-access versions only; it must say when a conclusion rests on the abstract alone |
| D-003 | Hallucinated citations | Every insight must carry a working link or DOI that the agent fetched in the same run; no link, no insight |
| D-004 | Overlap with AG-001 | Resolved 2026-10-26: AG-004 feeds the weekly article, AG-001 the four posts |
| D-005 | Automated publishing | Not in scope until stages 1–3 have run reliably; would need explicit approval recorded at G3 and a dedicated publishing tool |

## Change log

| Date | Change |
| --- | --- |
| 2026-10-20 | Designed from my process description; Notion database *Insighty naukowe* created and linked to *Publikacje* |
| 2026-10-26 | Decisions recorded: 8 search themes mapped to the 3 × 3 model, Saturday scan, article slot. Stage 1 instructions written; first stage 1 run done manually in a chat session, results in Notion as *Do wyboru* |
| 2026-10-26 | Gate G1: I selected 3 insights. Stage 2 instructions written and run manually; full texts changed one score and corrected one key finding. Insights wait at gate G2 |
