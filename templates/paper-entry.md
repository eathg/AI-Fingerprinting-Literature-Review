# Paper Entry Template

Use this as a reference when filling in each row of [`data/literature-tracker.csv`](../data/literature-tracker.csv). Below is the standard template with example entries and guidance for each field.

---

## Template

```
Paper title:
Year:
Authors / institution:
Sub-category:              [B1 / B2 / B3 / B4 / B5 — see docs/TASK.md §3]
Fingerprinting target:     [What exactly is being identified? Be specific.]
Trajectory type:           [Web interaction? Timing? Navigation path? API calls? Mouse movement?]
Input signal (features):   [What specific features are extracted from the trace? Be granular.]
Method:                    [1–2 sentences on the approach]
Dataset / environment:     [What data? How collected? How many sessions? How many agent types? Which websites/tasks? How were traces recorded?]
Evaluation metric:         [Accuracy? F1? AUC? TPR@FPR? Per-class breakdown?]
Main finding:              [1–2 sentence summary in your own words — do NOT copy the abstract]
Limitations:               [What the paper acknowledges + what you notice]
Replication suitability:   [✅ Suitable / ⚠️ Conditional / ❌ High risk — with 1-sentence reason]
```

---

## Example Entry 1 — Sub-Category B1 (Agent Framework Identification)

```
Paper title: Behavioral Signatures of Web Automation Agents
Year: 2025
Authors / institution: Patel & Kim, Lab Y
Sub-category: B1 (primary), B2 (secondary)
Fingerprinting target: Which agent framework (Browser-Use, Skyvern, custom Playwright) drove a given web browsing session — 3-way agent classification
Trajectory type: Web interaction traces (DOM-level events) + inter-action timing
Input signal (features): Sequence of DOM interactions encoded as (element_type, action_type) tuples, padded to 200 steps; element types = {button, link, input, div, img}; action types = {click, type, scroll, select}; separate pause-duration histogram (20 bins, 0–5s range)
Method: Two-branch neural network: 1D-CNN over action-sequence embeddings + MLP over pause histogram; softmax over 4 classes (3 agents + human)
Dataset / environment: Self-collected; 1,500 sessions (300 per agent × 3 + 600 human); 10 e-commerce websites; agents run with default configs; human data from lab study (12 participants); traces recorded via Playwright CDP interception. 80/10/10 train/val/test split, stratified by website
Evaluation metric: 4-class accuracy + per-class F1
Main finding: 84% accuracy overall; humans easily separated (F1=0.97); Browser-Use and custom Playwright frequently confused (F1=0.71); Skyvern distinct due to unique scroll-then-click pattern (F1=0.89)
Limitations: Only 3 agent frameworks; all agents run with default configs (no prompt variation tested); data from only e-commerce sites (generalization to other site types unknown); human traces from lab setting may not reflect natural behavior
Replication suitability: ✅ Suitable — agents are open-source and runnable, trace collection via Playwright CDP is reproducible, method is a standard CNN, dataset construction is clearly described
```

---

## Example Entry 2 — Sub-Category B2 (Agent-vs-Human Distinction)

```
Paper title: Detecting AI Web Agents via Interaction Timing Analysis
Year: 2025
Authors / institution: Garcia, L., et al., University Z
Sub-category: B2 (primary)
Fingerprinting target: Binary classification: is this web session driven by an AI agent or a human user?
Trajectory type: Temporal dynamics — inter-action pause durations and action speed
Input signal (features): 15 handcrafted timing features: mean/median/std of inter-action pauses, action burst rate (actions per 10s window), pause distribution skewness, maximum pause duration, click-to-scroll time ratio, session completion time
Method: Gradient-boosted decision trees (XGBoost) on the 15 timing features; 5-fold cross-validation
Dataset / environment: Self-collected; 2,000 sessions total (1,000 agent, 1,000 human); agents = GPT-4 + Browser-Use on 20 web tasks from WebArena; humans = Amazon Mechanical Turk workers on same tasks; timing recorded via instrumented Chrome extension. No explicit mention of train/test split beyond cross-validation
Evaluation metric: Accuracy, AUC-ROC, TPR at 1% FPR
Main finding: 93% accuracy, AUC 0.96; AI agents show significantly lower pause-variance and higher action-burst rates than humans; timing features alone outperform content-based features by 8 points AUC
Limitations: Only one agent framework (Browser-Use + GPT-4) tested; cross-validation but no held-out test set or cross-task generalization test; "agent" label does not distinguish different LLM backends; MTurk workers may behave differently from natural users
Replication suitability: ⚠️ Conditional — features are simple and clearly listed, but data collection is labor-intensive (need to run agents + recruit humans); no public dataset release; cross-validation only (no proper held-out evaluation)
```

---

## Example Entry 3 — Sub-Category B5 (Background: Traditional Bot Detection)

```
Paper title: Behavioral Bot Detection Using Mouse Dynamics
Year: 2023
Authors / institution: Wang et al., Security Lab Q
Sub-category: B5 (background — traditional bot detection)
Fingerprinting target: Binary classification: bot vs. human (bots = Selenium scripts, headless browsers, HTTP crawlers — NOT LLM agents)
Trajectory type: Mouse movement trajectories (raw cursor paths)
Input signal (features): 23 handcrafted features from mouse trajectories: total path length, direction changes, curvature, speed mean/std/max, acceleration mean/std, pause count, click duration, movement entropy (Shannon), straightness index
Method: Random forest classifier (100 trees) on the 23 features; threshold tuned for low FPR
Dataset / environment: Proprietary dataset from a CDN security product; 500K sessions; bot labels from CAPTCHA outcomes + heuristic rules; human labels from confirmed-human sessions; data not publicly available
Evaluation metric: AUC-ROC and TPR at 0.1% FPR
Main finding: AUC 0.97; movement entropy and direction-change count are the top features; Selenium-based bots show near-zero curvature variance; does NOT address LLM-driven agents
Limitations: Dataset is proprietary and not reproducible; "bot" label conflates scrapers, crawlers, and headless browsers — no LLM agents included; deployed in production so method details are sparse; no feature ablation
Replication suitability: ❌ High risk — proprietary dataset, no LLM agents in data, production system. BUT: feature engineering approach (23 mouse-dynamics features) is clearly listed and could be adapted for our agent-vs-human experiments
```

---

## Field-by-Field Guidance

### Sub-category (B1–B5)

Pick the **primary** sub-category and optionally list a secondary:
- **B1:** The paper identifies *which* agent framework/system produced a trace
- **B2:** The paper distinguishes AI agents from humans based on behavior
- **B3:** The paper characterizes *how* agents solve tasks (strategy/path patterns)
- **B4:** The paper attributes traces to specific agent versions/configurations
- **B5:** The paper is about traditional bots, browser fingerprinting, or behavioral biometrics — useful as background

### Fingerprinting target
Ask: "After running this method, what do we know that we didn't know before?"

- ❌ "Identifies agents" (too vague)
- ✅ "Identifies which of 4 agent frameworks (Browser-Use, Skyvern, AgentE, custom) drove this web session"
- ✅ "Binary: human vs. LLM-driven web agent"
- ✅ "Clusters agents by task-solving strategy (exploratory vs. direct-path)"

### Trajectory type
Identify the modality of the behavioral trace:
- Web interaction (clicks, scrolls, keystrokes, DOM events)
- Timing / temporal dynamics (pauses, speeds, burst rates)
- Navigation / page-transition sequences
- Mouse / cursor movement
- API / tool-call sequences

A paper may use multiple modalities — list all that apply.

### Input signal (features)
This is the **most important field**. List the actual features extracted from the trace, as granularly as the paper allows.

- ❌ "Behavioral features"
- ✅ "Inter-action pause durations (ms, binned to 10ms intervals); click-target element types; scroll depth per page (px); action-sequence 3-grams"

If the paper lists features in a table, copy the key ones. If described only as "behavioral features," note that — it affects replication risk.

### Dataset / environment — trace collection is critical
Look specifically for:
- **How were traces recorded?** (browser extension, Playwright CDP, proxy, lab instrument, production logs)
- **How many sessions/traces?**
- **How many agent types and/or human subjects?**
- **Which websites or tasks?**
- **Was the data made public?**

If the trace collection method is not described, this is a major red flag for replication.

### Replication suitability — one-sentence reason
Always include a brief justification:
- ✅ "Suitable — open-source agents, Playwright trace collection is reproducible, method is a standard CNN"
- ⚠️ "Conditional — features are clear but data collection requires running agents + recruiting humans; no public dataset"
- ❌ "High risk — proprietary dataset, no trace collection method described, only traditional bots tested"
