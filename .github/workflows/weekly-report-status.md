---
name: Weekly Report Status
description: Publish a concise report of repository activity from the previous seven days.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
strict: true
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Generate and publish a concise activity report for the previous seven full days,
ending at the workflow start time in UTC. Use the GitHub tools to inspect repository
commits, issues, and pull requests in that window.

Create exactly one new issue with a title beginning with `[weekly-report] `. The
issue must:

- Clearly state the reporting window in UTC.
- Summarize commits, issues, and pull requests separately, including useful counts
  and concise details.
- State clearly that no activity occurred for any category with no matching items.
- State clearly when there was no activity in all three categories.
- Remain concise and use headings for easy scanning.

Do not modify existing issues, pull requests, or repository contents. Do not create
an issue if the safe-output limit would be exceeded.