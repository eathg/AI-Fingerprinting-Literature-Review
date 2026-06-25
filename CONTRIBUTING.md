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
4. **Use the category codes** A, B, C, D, or E (see [`docs/TASK.md`](docs/TASK.md)). You may list multiple categories separated by `/` (e.g., `A/B`).
5. **Replication suitability** must be one of: `✅ Suitable`, `⚠️ Conditional`, or `❌ High risk`.

### Tip: Use Google Sheets

You can import the CSV into Google Sheets for easier editing, then export back to CSV before committing. Make sure the export preserves quoting correctly.

---

## Pull Request Checklist

Before opening your PR, verify:

- [ ] All assigned papers have a complete row in `literature-tracker.csv`
- [ ] Every field is filled — no empty cells (if information is unavailable, write "Not described in paper")
- [ ] "Fingerprinting target" and "Input signal" are specific (not vague)
- [ ] "Replication suitability" includes a one-sentence reason
- [ ] CSV is valid (opens correctly, no broken rows)
- [ ] No merge conflicts with `main`
