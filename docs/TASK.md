# Phase 1: Literature Mapping & Problem Scoping

## 1. Task Description

You are assigned a set of papers, technical reports, and system documents related to **agentic AI fingerprinting** — the broad problem of identifying, attributing, and distinguishing AI agents from their observable characteristics.

Your job is to read each assigned source and document it using a **standard template** so that the team builds a shared, searchable knowledge base. You are **not** expected to critique the papers deeply or propose new ideas. You **are** expected to record information accurately and flag methodological concerns (e.g., unclear data construction, missing baselines, evaluation gaps).

---

## 2. The Five-Category Taxonomy

Every paper you read should be assigned to **one primary category** (and optionally one or more secondary categories) from the taxonomy below.

### Category A — LLM / Model Identity Fingerprinting

Identifying *which* underlying language model produced a given output, typically using a small number of input–output pairs.

- **Fingerprinting target:** the base model (e.g., GPT-4 vs. Claude vs. Llama)
- **Typical signals:** text outputs, token-level statistics, response patterns to specific probes
- **Example questions:** "Can we determine which API is behind this chatbot from 5 queries?"

### Category B — Agent Behavioral Trajectory Fingerprinting

Identifying or characterizing an AI agent by its *interaction trace* — the sequence of actions it takes while completing a task.

- **Fingerprinting target:** agent framework, task-solving strategy, or specific agent system
- **Typical signals:** browser interactions (clicks, scrolls, keystrokes), navigation paths, API call sequences, dwell/pause times, error-recovery patterns
- **Example questions:** "Can we tell if this web session was driven by Browser-Use vs. Skyvern vs. a custom agent?"

### Category C — Human-vs-Agent Distinction

Detecting whether a given visitor, session, or content creator is a **human** or an **automated AI agent**.

- **Fingerprinting target:** human vs. AI agent (binary or multi-class)
- **Typical signals:** interaction speed, mouse movement entropy, CAPTCHA-like behavioral probes, content style, timing distributions
- **Example questions:** "Is this website visitor a human or a browser-automation agent?"

### Category D — Agent Provenance & Auditability

Establishing **provenance** — proving that a given behavior, text, or decision originated from a specific agent system, and enabling after-the-fact auditing.

- **Fingerprinting target:** attribution of outputs/actions to a specific agent or system version
- **Typical signals:** logs, cryptographic attestations, watermark signals, execution traces
- **Example questions:** "Can we cryptographically prove this decision was made by Agent X version Y?"

### Category E — Related but Distinct Problems

Papers on adjacent topics that inform our work but are **not** directly about fingerprinting agents. These provide background, signal types, and evaluation methodologies.

- **Sub-topics:**
  - **Watermarking** — embedding detectable signals into LLM outputs
  - **Bot detection** — traditional web bot vs. human classification
  - **Browser fingerprinting** — identifying browsers/devices via technical attributes
  - **Prompt leakage detection** — detecting if a system prompt has been extracted
  - **Authorship attribution** — attributing text to specific authors or models

---

## 3. Standard Reading Template

For **every** source you read, fill in the following fields. Use the spreadsheet row format in [`data/literature-tracker.csv`](../data/literature-tracker.csv) for the tracker, and refer to [`templates/paper-entry.md`](../templates/paper-entry.md) for detailed guidance on each field.

| Field | What to record |
|-------|---------------|
| **Paper title** | Full title |
| **Year** | Publication year |
| **Authors / institution** | First author + et al., and affiliation if notable |
| **Category** | A / B / C / D / E (primary) + secondary if applicable |
| **Fingerprinting target** | What exactly is being identified or attributed? Be specific: model identity? agent framework? human-vs-agent? specific agent version? |
| **Input signal** | What data does the method consume? Text outputs? UI interaction traces? browser attributes? timing data? API call logs? |
| **Method** | 1–2 sentences on the approach (e.g., "fine-tuned classifier on click sequences", "probing queries + logistic regression on response features") |
| **Dataset / environment** | What data was used? Was it collected by the authors? Public benchmark? Synthetic? How many samples? |
| **Evaluation metric** | Accuracy? F1? AUC? Precision/Recall? TPR at fixed FPR? |
| **Main finding** | The headline result (1–2 sentences) |
| **Limitations** | What the paper itself acknowledges as limitations, PLUS what you notice (small dataset? only one agent type? no held-out test set?) |
| **Replication suitability** | One of: ✅ **Suitable** / ⚠️ **Conditional** / ❌ **High risk** — with a one-sentence reason |

> **The two most important fields are "Fingerprinting target" and "Input signal."** These directly determine what experiments we can design later. Be precise.

---

## 4. Replication Risk Assessment Guide

As a first-year student, your main analytical contribution is the **replication risk assessment**. For each paper, ask yourself:

### ✅ Mark as "Suitable for replication" if:
- The dataset is clearly described or publicly available
- The method is explained in enough detail to re-implement
- Train/test splits are described (no obvious leakage)
- Evaluation metrics are standard and reproducible
- The setup is simple enough for a small team to reproduce

### ⚠️ Mark as "Conditional" if:
- Data is partially described but some details are missing
- The method is complex but re-implementable with effort
- Some hyperparameters or prompts are not fully specified
- The evaluation is mostly sound but has minor gaps

### ❌ Mark as "High risk" if:
- The paper reports high accuracy but **does not explain** how the dataset was constructed
- There is no clear train/test separation (data leakage risk)
- The method depends on proprietary tools or APIs that may change
- Key experimental details are missing
- Only one model or agent type is tested, making results hard to generalize

> **When in doubt, be conservative.** A paper that says "we achieved 98% accuracy" without explaining data splits should be flagged as high risk — even if the result looks impressive.

---

## 5. What the Summary Memo Should Cover

After all papers are documented, the team produces a **1–2 page memo** (see [`templates/memo.md`](../templates/memo.md)) that answers:

1. **Most common fingerprinting signals:** Across all papers you read, what input signals appear most frequently? (text? UI traces? timing? browser attributes?)
2. **Easiest methods to replicate:** Which 2–3 papers have the clearest setup and are most feasible for a small team to reproduce?
3. **Methodological risks:** Which papers have data leakage risks, unclear evaluation, or other red flags? Be specific.
4. **Recommended next step:** Based on everything, which category (A–E) and which specific approach should we prioritize for Phase 2 replication experiments, and why?

The memo should be **concrete and evidence-based** — cite specific papers from the tracker to support each claim. Do not write vague generalizations.

---

## 6. Evaluation Checklist (How Your Work Will Be Graded)

Your Phase 1 work will be evaluated against this checklist:

- [ ] Every assigned paper has a complete entry in the tracker (all fields filled)
- [ ] "Fingerprinting target" and "Input signal" fields are specific and accurate
- [ ] Category assignment is correct (A–E) with justification
- [ ] Replication risk assessment includes a one-sentence rationale
- [ ] Papers with unclear methodology are flagged (not silently accepted)
- [ ] The summary memo references specific papers and answers all four questions
- [ ] All work is submitted via Pull Request before the deadline
