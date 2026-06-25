# Contributing

This document describes the workflow for Phase 1 contributions.

---

## Step 1: Claim Papers

1. Go to the **Issues** tab of this repository.
2. Look for the issue titled **"Phase 1 — Paper Assignment"** (created by the instructor).
3. Comment on that issue with the papers you want to claim (by title or reference).
4. The instructor will confirm your assignment.

**Each student should aim for 3–5 papers.** If you want to read more, coordinate with the team.

---

## Step 2: Read and Document

1. Read the paper following the guidelines in [`docs/guidelines.md`](docs/guidelines.md).
2. Fill in a row in [`data/literature-tracker.csv`](data/literature-tracker.csv) for each paper.
3. Use [`templates/paper-entry.md`](templates/paper-entry.md) as your field-by-field reference.

> **Scope reminder:** This project focuses on **agent behavioral trajectory fingerprinting** — identifying agents by their action sequences and interaction dynamics. If a paper only analyzes text outputs or HTTP headers, note it briefly as B5 (background) or skip it.

---

## Step 3: Submit Your Work

1. **Create a branch:**

   ```bash
   git checkout -b phase1/<your-name>
   ```

2. **Commit your changes:**

   ```bash
   git add data/literature-tracker.csv
   git commit -m "Add literature entries: [paper1 short title], [paper2 short title]"
   ```

3. **Push and open a Pull Request:**

   ```bash
   git push -u origin phase1/<your-name>
   ```

   Then open a PR against `main` with:
   - **Title:** `Phase 1: Literature entries — <Your Name>`
   - **Description:** List the papers you documented and any notes for reviewers

---

## Step 4: Review

- A teammate or the instructor will review your PR.
- Address any feedback by pushing additional commits to the same branch.
- Once approved, your PR will be merged.

---

## CSV Formatting Rules

The `data/literature-tracker.csv` is the core deliverable. Follow these rules to keep it clean:

1. **One paper per row.** Do not merge multiple papers into one row.
2. **Commas inside fields must be quoted.** If a field contains a comma, wrap the entire field in double quotes:
   ```
   "Chen, J., Smith, A., et al."
   ```
3. **No line breaks within a field.** Keep each row on a single line.
4. **Use the sub-category codes** B1, B2, B3, B4, or B5 (see [`docs/TASK.md`](docs/TASK.md)). You may list multiple sub-categories separated by `/` (e.g., `B1/B2`).
5. **Replication suitability** must be one of: `✅ Suitable`, `⚠️ Conditional`, or `❌ High risk`.

### Tip: Use Google Sheets

You can import the CSV into Google Sheets for easier editing, then export back to CSV before committing. Make sure the export preserves quoting correctly.

---

## Pull Request Checklist

Before opening your PR, verify:

- [ ] All assigned papers have a complete row in `literature-tracker.csv`
- [ ] Every field is filled — no empty cells (if information is unavailable, write "Not described in paper")
- [ ] "Fingerprinting target," "Trajectory type," and "Input signal (features)" are specific (not vague)
- [ ] "Input signal (features)" lists concrete features, not just "behavioral features"
- [ ] "Replication suitability" includes a one-sentence reason
- [ ] Papers that conflate traditional bots with LLM agents are noted
- [ ] CSV is valid (opens correctly, no broken rows)
- [ ] No merge conflicts with `main`
