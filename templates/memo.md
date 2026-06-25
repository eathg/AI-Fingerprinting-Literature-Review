# Summary Memo Template

> **Length:** 1–2 pages (approximately 500–1000 words)
>
> **Format:** Markdown, placed at [`memo/memo.md`](../memo/memo.md)
>
> **Deadline:** Day 6 of Phase 1 (see [README](../README.md#timeline))

---

## Purpose

The memo synthesizes what the team learned from the literature mapping on **agent behavioral trajectory fingerprinting**. It is **not** a literature survey in academic form. It is a **decision-support document** that helps the team choose what to replicate in Phase 2.

Write in clear, direct prose. Every claim should reference specific papers from the tracker (by short title or row number).

---

## Structure

### 1. Scope of Review (1 short paragraph)

- How many papers were reviewed
- Which sub-categories (B1–B5) are represented and how many in each
- Any notable gaps (e.g., "we found very few papers in B4 — agent provenance via traces" or "most B5 papers study traditional bots, not LLM agents")

### 2. Most Common Trajectory Types and Features (1 paragraph + table)

Answer: **Across all papers, what behavioral signals are extracted most frequently, and which appear most informative?**

Consider creating a frequency table:

| Trajectory type / feature | # of papers | Appears informative? | Example papers |
|---------------------------|-------------|----------------------|----------------|
| Inter-action pause durations / timing | X | Yes — top feature in [paper1], [paper2] | [paper1], [paper2] |
| Click-target element sequences | X | Yes for framework ID; less for human-vs-agent | [paper3] |
| Mouse movement (curvature, entropy) | X | Yes in B5 bot detection; untested for LLM agents | [paper4] |
| Page-transition graphs | X | Mixed — task-dependent | [paper5] |
| Action-sequence n-grams | X | Yes, but requires fixed action vocabulary | [paper6] |

Then write 2–3 sentences interpreting the pattern. Which signal types are consistently informative across papers? Which are promising but undertested?

### 3. Methods Most Feasible for Replication (1 paragraph)

Answer: **Which 2–3 papers have the clearest experimental setup and are most feasible for our team to reproduce?**

For each recommended paper, state:
- Paper name and sub-category
- Why it is feasible (open-source agents? traces collectible via Playwright? simple features? public dataset?)
- What we would need to replicate it (compute, agent frameworks, human data, websites/tasks)
- Estimated effort (how many traces to collect, how complex the pipeline is)

### 4. Methodological Risks (1 paragraph)

Answer: **Which papers have data leakage, unclear trace collection, bot/agent conflation, or other red flags?**

Be specific. Name the papers and the exact concern:
- "Paper X reports 95% accuracy but does not describe how traces were collected or how train/test were split"
- "Paper Y evaluates only on Selenium bots — results may not transfer to LLM-driven agents"
- "Paper Z uses cross-validation but no held-out test set or cross-website generalization test"
- "Paper W does not vary agent prompts or configurations — signatures may be prompt-specific, not framework-specific"

### 5. Recommended Next Step (1 paragraph)

Answer: **Which sub-category and approach should we prioritize for Phase 2 replication?**

This is the most important paragraph. State:
- Which sub-category (B1 framework ID? B2 agent-vs-human? B3 strategy fingerprinting?) is most promising and why
- Which specific method/paper to replicate first, or which features to combine
- What the Phase 2 experiment would look like (briefly): which agents, which tasks/websites, which features, which evaluation protocol
- What data collection infrastructure we need to build (e.g., Playwright-based trace recorder)

---

## Example Memo Opening

> In Phase 1, we reviewed 15 papers on agent behavioral trajectory fingerprinting. The breakdown by sub-category: 4 on agent framework identification (B1), 3 on agent-vs-human behavioral distinction (B2), 2 on task-strategy fingerprinting (B3), 0 on provenance via traces (B4 — a clear gap), and 6 on related background including traditional bot detection and behavioral biometrics (B5). The most consistently informative signal across B1–B2 papers is **inter-action timing** (pause durations, burst rates), appearing as a top feature in 5/7 core papers. Mouse-movement features dominate B5 bot detection but have not been tested against LLM-driven agents. Notably, no paper in our set addresses agent provenance via behavioral traces (B4), suggesting an opportunity for novel contribution...
