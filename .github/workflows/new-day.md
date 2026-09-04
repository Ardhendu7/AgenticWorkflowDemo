---
name: New Day
description: Add the current UTC date to the site's daily updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
strict: true
tools:
  edit: true
safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - index.html
---

# New Day

Update the repository's daily update UI for this workflow run.

1. Determine the workflow run's UTC date by running `date -u +%Y-%m-%d` and
   format it using the existing date wording convention in `index.html` (for
   example, `1st of August`). Use that same wording everywhere for this update.
2. Inspect `index.html` and follow its existing HTML structure, ID conventions,
   accessibility attributes, and class names exactly. Do not modify `styles.css`.
3. Add one navigation control for the UTC date to the existing `Daily Updates`
   navigation, preserving every existing daily update and control.
4. Add one matching accessible `<dialog>` for the date. The control's
   `aria-controls` must point to the dialog ID, and the dialog must use matching
   `aria-labelledby` and `aria-describedby` IDs consistent with the existing
   dialog. Give the update a concise confirmation message that the daily update
   ran.
5. Before editing, search for the UTC date, its navigation control, and its dialog
   IDs. If the date is already present, make no change and call `noop`.
6. Do not duplicate any date, navigation control, or dialog. Do not remove or
   alter any existing daily update. Do not change files other than `index.html`.

Create at most one pull request containing the `index.html` change. If no change
is needed because the UTC date is already present, do not create a pull request.