# Phase 1: Literature Mapping & Problem Scoping
## Focus: Agent Behavioral Trajectory Fingerprinting

---

## 1. Task Description

You are assigned a set of papers, technical reports, and system documents related to **agent behavioral trajectory fingerprinting** — identifying, classifying, or attributing AI agents by analyzing the **sequences of actions they produce** during task execution (clicks, scrolls, keystrokes, navigations, API calls, timing patterns, error recovery, etc.).

Your job is to read each assigned source and document it using a **standard template** so that the team builds a shared, searchable knowledge base. You are **not** expected to critique the papers deeply or propose new ideas. You **are** expected to record information accurately and flag methodological concerns (e.g., unclear data construction, missing baselines, evaluation gaps).

---

## 2. What We Mean by "Behavioral Trajectory"

A **behavioral trajectory** is the observable record of an agent's actions during a task episode. It is not the agent's text output or internal reasoning — it is **what the agent physically does** in the environment. Common forms include:

| Trajectory type | Example elements |
|-----------------|------------------|
| **Web interaction trace** | Click targets (element type, x/y coordinates), scroll depth, keystroke sequences, page transitions, DOM state changes |
| **Timing / temporal dynamics** | Inter-action pause durations, action speed distributions, session duration, burst patterns |
| **Navigation / task path** | Sequence of pages visited, task completion route, backtrack/retry patterns, error-recovery sequences |
| **API / tool-call sequence** | Function call order, argument patterns, call frequency, retry behavior |
| **Mouse / cursor movement** | Raw cursor trajectories, movement entropy, acceleration profiles, hovering behavior |

The key distinction: we care about **behavioral traces**, not text content. A paper that only analyzes the *text* an LLM generates belongs to a different research area (model output fingerprinting). We want papers where the **primary signal is the action sequence or interaction pattern**.

> **Borderline note:** Some papers use behavioral signals *alongside* text or system features. Include these if behavioral/trajectory data is a **primary** input. Exclude papers where behavior is incidental or not analyzed as a signal.

---

## 3. Sub-Category Taxonomy

Every paper you read should be assigned to **one primary sub-category** (and optionally one or more secondary) from the taxonomy below. All sub-categories fall under the umbrella of **behavioral trajectory fingerprinting** — the difference is *what* the trajectory is used to identify.

### B1 — Agent Framework / System Identification

Identifying **which agent system or framework** produced a given behavioral trace.

- **Target:** The specific agent framework or system (e.g., Browser-Use vs. Skyvern vs. a custom Playwright agent vs. a Claude Computer-Use agent)
- **Typical signals:** Action sequence patterns, tool-call signatures, navigation structure, error-handling style
- **Key question:** "Given this browsing trace, can we tell which agent framework drove it?"

### B2 — Agent-vs-Human Behavioral Distinction

Detecting whether a behavioral trace was produced by an **AI agent** or a **human user**.

- **Target:** Binary or multi-class classification (human vs. one or more agent types)
- **Typical signals:** Interaction speed, movement entropy, pause distributions, error patterns, task-path regularity
- **Key question:** "Is this web session driven by a human or an automated AI agent?"
- **Note:** This is *behavioral* human-vs-agent distinction, not content-based (e.g., "is this text AI-generated?"). The signal must come from interaction dynamics.

### B3 — Agent Strategy / Task-Path Fingerprinting

Characterizing or clustering agents by their **task-solving strategy** — the route they take through a task, independent of framework identity.

- **Target:** Task-solving approach, navigation pattern, or behavioral "style"
- **Typical signals:** Page-transition graphs, action-frequency distributions, exploration vs. exploitation patterns
- **Key question:** "Do different agents solve the same task in systematically different ways?"

### B4 — Agent Provenance via Behavioral Traces

Using behavioral traces to establish **provenance or auditability** — proving that a specific trace came from a particular agent system, version, or configuration.

- **Target:** Attribution of a behavioral trace to a specific agent version/configuration
- **Typical signals:** Version-specific behavioral signatures, configuration-dependent action patterns, watermark-like behavioral artifacts
- **Key question:** "Can we prove this behavioral trace was produced by Agent X version Y?"

### B5 — Background & Adjacent Methods

Papers on related problems that provide **signal types, features, or evaluation methodologies** we can borrow, even if they are not directly about AI agents.

- **Sub-topics:**
  - **Traditional bot detection** — behavioral bot/human classifiers (mouse movement, click patterns) developed before AI agents existed
  - **Browser fingerprinting** — device/browser identification via technical attributes (may provide complementary signals)
  - **Behavioral biometrics** — human identity verification via interaction dynamics (feature engineering inspiration)
  - **Human web browsing analysis** — models of human browsing behavior (useful as baselines or comparison points)
  - **Watermarking (behavioral)** — embedding detectable patterns in agent behavior (if any such work exists)

---

## 4. Standard Reading Template

For **every** source you read, fill in the following fields. Use the spreadsheet row format in [`data/literature-tracker.csv`](../data/literature-tracker.csv) for the tracker, and refer to [`templates/paper-entry.md`](../templates/paper-entry.md) for detailed guidance and examples.

| Field | What to record |
|-------|---------------|
| **Paper title** | Full title |
| **Year** | Publication year |
| **Authors / institution** | First author + et al., and affiliation if notable |
| **Sub-category** | B1 / B2 / B3 / B4 / B5 (primary) + secondary if applicable |
| **Fingerprinting target** | What exactly is being identified or attributed? Be specific: which agent framework? human-vs-agent? task strategy? agent version? |
| **Trajectory type** | What kind of behavioral trace? Web interaction (clicks/scrolls)? Timing? Navigation path? API calls? Mouse movement? |
| **Input signal (features)** | What specific features are extracted from the trajectory? Be granular: "inter-action pause durations", "click-target element types", "scroll depth per page", "action sequence n-grams" |
| **Method** | 1–2 sentences on the approach (e.g., "1D-CNN over action sequences", "XGBoost on handcrafted timing features", "sequence matching with DTW") |
| **Dataset / environment** | What data? Self-collected or public? How many sessions/traces? How many agent types or human subjects? What websites/tasks? How were traces recorded (extension, proxy, instrumented browser)? |
| **Evaluation metric** | Accuracy? F1? AUC? TPR@FPR? Per-class breakdowns? |
| **Main finding** | The headline result (1–2 sentences, in your own words) |
| **Limitations** | What the paper acknowledges + what you notice (small dataset? only one agent type? no held-out test set? traces collected in unrealistic conditions?) |
| **Replication suitability** | ✅ **Suitable** / ⚠️ **Conditional** / ❌ **High risk** — with a one-sentence reason |

> **The three most important fields are "Fingerprinting target," "Trajectory type," and "Input signal (features)."** These directly determine what experiments we can design later. Be precise and specific.

---

## 5. Replication Risk Assessment Guide

As a first-year student, your main analytical contribution is the **replication risk assessment**. For each paper, ask yourself:

### ✅ Mark as "Suitable for replication" if:
- The dataset is clearly described or publicly available
- The trajectory collection method is explained (how were traces recorded?)
- The feature extraction pipeline is described in enough detail to re-implement
- Train/test splits are described (no obvious leakage — e.g., sessions from the same user in both train and test)
- Evaluation metrics are standard and reproducible
- The setup is simple enough for a small team to reproduce

### ⚠️ Mark as "Conditional" if:
- Data is partially described but some details are missing (e.g., number of sessions stated but collection method unclear)
- Feature engineering is described but not fully specified (e.g., "behavioral features" without listing them)
- The method is complex but re-implementable with effort
- Some hyperparameters or model details are not specified
- The evaluation is mostly sound but has minor gaps

### ❌ Mark as "High risk" if:
- The paper reports high accuracy but **does not explain** how traces were collected or how the dataset was constructed
- There is no clear train/test separation (e.g., sessions from the same task/website split across both)
- The method depends on proprietary tools, commercial detection systems, or APIs that may change
- Key experimental details are missing (how many agents? which versions? what tasks?)
- Only one agent type or one website is tested, making results hard to generalize
- The "agent" label conflates traditional bots (scrapers, crawlers) with modern LLM-driven agents

> **When in doubt, be conservative.** A paper that says "we achieved 98% accuracy" without explaining data splits or trace collection should be flagged as high risk — even if the result looks impressive.

---

## 6. What the Summary Memo Should Cover

After all papers are documented, the team produces a **1–2 page memo** (see [`templates/memo.md`](../templates/memo.md)) that answers:

1. **Most common trajectory types and features:** Across all papers, what behavioral signals are extracted most frequently? (click sequences? timing? navigation graphs? mouse movement?) Are there signal types that are consistently informative across papers?
2. **Easiest methods to replicate:** Which 2–3 papers have the clearest setup — clear data collection, simple feature pipelines, standard evaluation — and are most feasible for a small team to reproduce?
3. **Methodological risks:** Which papers have data leakage risks, unclear trace collection, conflation of bots and AI agents, or other red flags? Be specific.
4. **Recommended next step:** Based on everything, which sub-category (B1–B4) and which specific approach should we prioritize for Phase 2 replication experiments, and why?

The memo should be **concrete and evidence-based** — cite specific papers from the tracker to support each claim. Do not write vague generalizations.

---

## 7. Evaluation Checklist (How Your Work Will Be Graded)

Your Phase 1 work will be evaluated against this checklist:

- [ ] Every assigned paper has a complete entry in the tracker (all fields filled)
- [ ] "Fingerprinting target," "Trajectory type," and "Input signal (features)" are specific and accurate
- [ ] Sub-category assignment is correct (B1–B5) with justification
- [ ] Replication risk assessment includes a one-sentence rationale
- [ ] Papers with unclear methodology or trace collection are flagged (not silently accepted)
- [ ] Papers that conflate traditional bots with AI agents are noted
- [ ] The summary memo references specific papers and answers all four questions
- [ ] All work is submitted via Pull Request before the deadline
