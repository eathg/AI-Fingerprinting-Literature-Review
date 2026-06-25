# Summary Memo Template

> **Length:** 1–2 pages (approximately 500–1000 words)
>
> **Format:** Markdown, placed at [`memo/memo.md`](../memo/memo.md)
>
> **Deadline:** Day 6 of Phase 1 (see [README](../README.md#timeline))

---

## Purpose

The memo synthesizes what the team learned from the literature mapping. It is **not** a literature survey in academic form. It is a **decision-support document** that helps the team choose what to replicate in Phase 2.

Write in clear, direct prose. Every claim should reference specific papers from the tracker (by short title or row number).

---

## Structure

### 1. Scope of Review (1 short paragraph)

- How many papers were reviewed
- Which categories (A–E) are represented and how many in each
- Any notable gaps (e.g., "we found very few papers in Category D — agent provenance")

### 2. Most Common Fingerprinting Signals (1 paragraph + optional table)

Answer: **Across all papers, what input signals appear most frequently?**

Consider creating a simple frequency table:

| Signal type | # of papers | Example papers |
|-------------|-------------|----------------|
| Text outputs / log-probabilities | X | [paper1], [paper2] |
| UI interaction traces (clicks, scrolls) | X | [paper3] |
| Timing / behavioral biometrics | X | [paper4] |
| Browser/device attributes | X | [paper5] |
| Cryptographic / watermark signals | X | [paper6] |

Then write 2–3 sentences interpreting the pattern.

### 3. Methods Most Feasible for Replication (1 paragraph)

Answer: **Which 2–3 papers have the clearest setup and are most feasible for our team to reproduce?**

For each recommended paper, state:
- Paper name and category
- Why it is feasible (data available, method simple, evaluation clear)
- What we would need to replicate it (compute, data, tools)

### 4. Methodological Risks (1 paragraph)

Answer: **Which papers have data leakage, unclear evaluation, or other red flags?**

Be specific. Name the papers and the exact concern:
- "Paper X reports 95% accuracy but does not describe how train/test were split"
- "Paper Y evaluates only on 2 agent types, making generalization unclear"
- "Paper Z uses proprietary data that cannot be reproduced"

### 5. Recommended Next Step (1 paragraph)

Answer: **Which category and approach should we prioritize for Phase 2?**

This is the most important paragraph. State:
- Which category (A–E) is most promising and why
- Which specific method/paper to replicate first
- What the Phase 2 experiment would look like (briefly)

---

## Example Memo Opening

> In Phase 1, we reviewed 18 papers across five categories: 6 on LLM identity fingerprinting (A), 4 on agent behavioral traces (B), 3 on human-vs-agent distinction (C), 1 on agent provenance (D), and 4 on related topics including watermarking and bot detection (E). The most common signal across all categories is **text-based features** (appearing in 12/18 papers), followed by **behavioral timing data** (8/18). Notably, only 1 paper addresses agent provenance, suggesting this is an underexplored area...
