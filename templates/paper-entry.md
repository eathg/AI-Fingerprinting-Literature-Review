# Paper Entry Template

Use this as a reference when filling in each row of [`data/literature-tracker.csv`](../data/literature-tracker.csv). Below is the standard template with example entries and guidance for each field.

---

## Template

```
Paper title:
Year:
Authors / institution:
Category:              [A / B / C / D / E — see docs/TASK.md §2]
Fingerprinting target: [What exactly is being identified? Be specific.]
Input signal:          [What raw data does the method consume? Be specific.]
Method:                [1–2 sentences on the approach]
Dataset / environment: [What data? How collected? How many samples? Public or private?]
Evaluation metric:     [Accuracy? F1? AUC? TPR@FPR?]
Main finding:          [1–2 sentence summary in your own words — do NOT copy the abstract]
Limitations:           [What the paper acknowledges + what you notice]
Replication suitability: [✅ Suitable / ⚠️ Conditional / ❌ High risk — with 1-sentence reason]
```

---

## Example Entry 1 — Category A (Model Identity)

```
Paper title: Identifying the Source Language Model from Output Text
Year: 2024
Authors / institution: Chen et al., University of X
Category: A (primary)
Fingerprinting target: Which specific LLM (among 6 candidate models) generated a given text passage
Input signal: Token-level log-probability scores obtained by sending 5 probe prompts to the target; plus stylometric features (sentence length, vocabulary richness)
Method: Logistic regression classifier on a 47-dimensional feature vector (log-probs + stylometrics), trained on 10k samples per model
Dataset / environment: 6 open-weight LLMs (Llama-2-7B, Mistral-7B, etc.); 10,000 generations per model from Alpaca-style prompts; 80/10/10 train/val/test split
Evaluation metric: Top-1 accuracy and macro-F1
Main finding: 91% accuracy in identifying the source model among 6 candidates using only 5 probe queries; stylometric features alone achieve 73%
Limitations: Only tested on open-weight models with known tokenizers (log-prob access required); closed APIs may not expose log-probs; no adversarial setting
Replication suitability: ✅ Suitable — open-weight models available, method is simple logistic regression, dataset construction is clearly described
```

---

## Example Entry 2 — Category B (Agent Behavioral Trace)

```
Paper title: Behavioral Signatures of Web Automation Agents
Year: 2025
Authors / institution: Patel & Kim, Lab Y
Category: B (primary), C (secondary)
Fingerprinting target: Which agent framework (Browser-Use, Skyvern, custom Playwright script) drove a given web browsing session
Input signal: Sequence of DOM interactions (element type, x/y coordinates, action type) + inter-action pause durations; extracted from browser extension logs
Method: 1D-CNN over action sequences (padded to 200 steps), with separate branch for pause-duration histogram
Dataset / environment: Self-collected — 1,500 sessions across 3 agents and 50 human users on 10 e-commerce websites; no train/test contamination described
Evaluation metric: 4-class accuracy (3 agents + human) and per-class F1
Main finding: 84% accuracy distinguishing 3 agent frameworks; confusion mainly between Browser-Use and custom Playwright; humans easily separated (F1=0.97)
Limitations: Dataset construction not clearly described (how were sessions sampled? were the same tasks used?); only 3 agent frameworks; potential task-specific overfitting
Replication suitability: ⚠️ Conditional — method is reproducible but dataset construction is underspecified; would need to re-collect data from scratch
```

---

## Example Entry 3 — Category E (Related: Bot Detection)

```
Paper title: Advanced Bot Detection Using Behavioral Biometrics
Year: 2023
Authors / institution: Garcia et al., Company Z
Category: E (related — bot detection)
Fingerprinting target: Whether a web visitor is a bot or a human (binary)
Input signal: Mouse movement entropy, click speed distribution, scroll patterns, dwell time per page
Method: Gradient-boosted trees (XGBoost) on 23 handcrafted behavioral features
Dataset / environment: Proprietary dataset from a CDN provider; 500K sessions; labels from CAPTCHA outcomes; not publicly available
Evaluation metric: AUC-ROC and TPR at 0.1% FPR
Main finding: AUC 0.97; behavioral features outperform IP/header-based features by 12 points AUC
Limitations: Dataset is proprietary and not reproducible; "bot" label conflates scrapers, crawlers, and AI agents — does not distinguish AI agents specifically; deployed in production so details are sparse
Replication suitability: ❌ High risk — proprietary dataset, production system, no reproducible setup; useful only as background on signal types
```

---

## Field-by-Field Guidance

### Fingerprinting target
This is the **single most important field**. Ask: "After running this method, what do we know that we didn't know before?"

- ❌ "Identifies agents" (too vague)
- ✅ "Identifies which of 4 specific agent frameworks drove this web session"
- ✅ "Determines whether a given text was written by GPT-4 or a human"

### Input signal
List the **actual raw data** the method consumes, not the abstract concept.

- ❌ "Behavioral features"
- ✅ "Mouse (x,y) coordinates sampled at 60Hz + click timestamps + scroll depth per page"

### Replication suitability — one-sentence reason
Always include a brief justification.

- ✅ "Suitable — open models, simple method, clear data splits"
- ⚠️ "Conditional — method is clear but dataset is proprietary"
- ❌ "High risk — no data description, no train/test split, proprietary system"
