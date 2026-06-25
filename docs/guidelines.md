# Reading Guidelines for First-Year Students

## Your Role

You are a **research assistant** on a literature mapping project. Your primary contribution at this stage is **accurate documentation**, not critical innovation. This document explains exactly how to approach each paper.

---

## How to Read Each Paper

You do **not** need to understand every equation or implementation detail. Focus on extracting structured information. Here is a recommended reading order:

### Step 1 — Skim (5 minutes)

- Read the **title**, **abstract**, and **section headings**
- Look at **Table 1** or the main results table
- Check: is this paper about fingerprinting/identifying AI agents or models? If not, note it as Category E (related work)

### Step 2 — Extract Key Fields (15–20 minutes)

Fill in the standard template. Focus on these questions in order:

1. **What is being fingerprinted?** (model identity? agent behavior? human-vs-agent? provenance?)
2. **What data/signal does the method use?** (text? clicks? timing? browser attributes?)
3. **How was the data collected?** (This is critical — if you can't tell, flag it)
4. **What metric do they report?** (accuracy? F1? AUC?)
5. **Is the setup reproducible?** Could you re-run this experiment given the information in the paper?

### Step 3 — Assess Replication Risk (5 minutes)

Apply the checklist from [`TASK.md` §4](TASK.md#4-replication-risk-assessment-guide).

---

## Common Pitfalls to Avoid

### 1. "High accuracy" does not mean "good paper"

A paper reporting 99% accuracy is **not automatically** trustworthy. Ask:
- How was the test set constructed? Was it separate from training?
- Is there a realistic adversary, or is the setting too easy?
- Could the model be memorizing rather than generalizing?

If the answer is unclear, mark as **❌ High risk**.

### 2. Vague "Input signal" entries

❌ Bad: "Behavioral data"
✅ Good: "Mouse movement trajectories (x,y coordinates at 60Hz) and click timestamps"

❌ Bad: "Text features"
✅ Good: "Token-level log-probabilities from the target model, averaged over 5 probe queries"

Be specific about **what raw data** the method actually consumes.

### 3. Copying the abstract for "Main finding"

Do not paste the abstract. Write **your own** 1–2 sentence summary of the key result. Example:

❌ Bad (abstract copy): "We propose a novel framework for agent identification that achieves state-of-the-art results across multiple benchmarks..."

✅ Good (your summary): "A random forest classifier trained on click-sequence features (clicks/min, scroll distance, inter-action pause) distinguishes 4 browser-automation agents with 87% F1 on a self-collected dataset of 2,000 sessions."

### 4. Missing the "Limitations" field

Every paper has limitations. If the paper's authors don't state them clearly, identify them yourself:
- Small dataset?
- Only tested on one model/agent?
- No comparison to baselines?
- Evaluation metric not standard?

---

## How Much Detail Is Enough?

| Field | Expected effort |
|-------|----------------|
| Paper title, year, authors | Copy exactly — 1 minute |
| Category | Read abstract + intro, decide — 2 minutes |
| Fingerprinting target | 1–2 sentences — 2 minutes |
| Input signal | **Be specific** — 3 minutes (this is the most important field) |
| Method | 1–2 sentences — 3 minutes |
| Dataset / environment | Look for data section — 3 minutes |
| Evaluation metric | Check results table — 1 minute |
| Main finding | Write your own summary — 3 minutes |
| Limitations | Read discussion section + your own observation — 3 minutes |
| Replication suitability | Apply checklist — 2 minutes |

**Total: ~20–25 minutes per paper.** This is a documentation task, not a deep reading task.

---

## When You're Unsure

- **Unsure about category?** Read the intro and conclusion. If still unsure, pick the closest fit and note your uncertainty in the "Limitations" field.
- **Can't find the dataset description?** Mark replication risk as ❌ and note "dataset construction not described."
- **Don't understand the method?** Write what you *do* understand (e.g., "uses a neural network classifier, architecture details not fully clear") and note it.
- **Paper is not about fingerprinting at all?** Assign Category E and document it briefly — it may still provide useful signal types or evaluation methods.

**When in doubt, document honestly.** Flagging "I couldn't find this information" is more valuable than guessing.
