# Agent Behavioral Trajectory Fingerprinting — Research Project

> **Phase 1 (Current):** Literature Mapping & Problem Scoping
>
> **Timeline:** 7 days from assignment
>
> **Audience:** Undergraduate research assistants

---

## Project Overview

This repository hosts a multi-phase research project on **agent behavioral trajectory fingerprinting** — the problem of identifying, classifying, and attributing AI agent systems by analyzing their **observable behavioral traces** during task execution.

An agent's behavioral trajectory is the sequence of actions it takes while completing a task: clicks, scrolls, keystrokes, page navigations, API calls, dwell times, error-recovery patterns, and more. The central question of this project is:

> **Given a behavioral trace from a web interaction or task episode, can we determine which agent system produced it, distinguish it from a human, or attribute it to a specific agent version?**

This is distinct from text-output fingerprinting (which model wrote this text?) or browser fingerprinting (which device/browser is this?). We focus specifically on **what the agent *does*** — its action sequence and interaction dynamics.

| Phase | Title | Status | Deliverable |
|-------|-------|--------|-------------|
| **1** | Literature Mapping & Problem Scoping | 🟡 **Active** | Structured literature tracker + 1–2 page memo |
| 2 | Method Replication & Benchmarking | ⬜ Upcoming | TBD |
| 3 | Novel Experiments | ⬜ Upcoming | TBD |

---

## Phase 1: Literature Mapping & Problem Scoping

### Objective

Read, categorize, and systematically document papers related to **agent behavioral trajectory fingerprinting** and adjacent areas. The goal is **not** to produce novel research in this phase — it is to build a **structured knowledge base** that the team will use to design experiments in later phases.

By the end of Phase 1, the team should be able to answer three questions:

1. **What behavioral signals** do existing methods extract from agent traces? (click sequences, timing distributions, navigation graphs, DOM interactions, API call patterns)
2. **What is being identified** — agent framework, specific agent system, human-vs-agent, or something else?
3. **Which methods** have the clearest experimental setup and are feasible for our team to replicate?

### Deliverables

| # | Deliverable | Format | Location |
|---|-------------|--------|----------|
| 1 | **Literature Tracker** — one row per paper, filled using the standard template | CSV (Google Sheets compatible) | [`data/literature-tracker.csv`](data/literature-tracker.csv) |
| 2 | **Summary Memo** — 1–2 pages answering the three key questions | Markdown | [`memo/memo.md`](memo/memo.md) |

### Timeline

| Day | Milestone |
|-----|-----------|
| Day 1 | Read [`TASK.md`](docs/TASK.md); claim papers via Issues; set up shared sheet |
| Day 2–4 | Read and document assigned papers using the [entry template](templates/paper-entry.md) |
| Day 5 | Cross-check sub-categories; flag replication-risk papers; peer review within the team |
| Day 6 | Draft the summary memo |
| Day 7 | Final review, submit PR |

---

## Repository Structure

```
agentic-ai-fingerprinting/
├── README.md                        # You are here — project overview
├── CONTRIBUTING.md                  # How to submit your work (workflow, PR rules)
├── LICENSE                          # MIT
├── docs/
│   ├── TASK.md                      # Full Phase 1 task description + taxonomy
│   └── guidelines.md                # Reading guidelines & rubric for first-year students
├── templates/
│   ├── paper-entry.md               # Standard template for each paper entry
│   └── memo.md                      # Template + prompts for the summary memo
├── data/
│   └── literature-tracker.csv       # The main spreadsheet (CSV, one row per paper)
└── memo/
    └── memo.md                      # The final summary memo goes here
```

---

## Getting Started (For Students)

1. **Clone this repository.**

   ```bash
   git clone https://github.com/jzrz-bot/agentic-ai-fingerprinting.git
   ```

2. **Read [`docs/TASK.md`](docs/TASK.md)** in full — it contains the task description, the sub-category taxonomy, and the reading template.

3. **Read [`CONTRIBUTING.md`](CONTRIBUTING.md)** — it explains how to claim papers and submit your work.

4. **Claim papers** by opening an Issue (see Contributing). Each student should aim for **3–5 papers** depending on length.

5. **Fill in the [`data/literature-tracker.csv`](data/literature-tracker.csv)** for each paper you read, following the [entry template](templates/paper-entry.md).

6. **Submit a Pull Request** when your entries are complete.

---

## License

[MIT](LICENSE)
