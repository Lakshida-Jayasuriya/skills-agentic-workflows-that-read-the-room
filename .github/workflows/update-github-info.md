---
name: update-github-info
description: Refresh Mona's GitHub Info page with practical updates from official GitHub sources.
intent: Keep Mona's GitHub Info page concise, practical, and current using verified official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    base-branch: main
    draft: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Refresh `site/content/github-info.md` daily or when manually requested, and propose every change through a pull request for Mona to review.

1. Read `notes/mona-notes.md` and the current `site/content/github-info.md` before drafting.
2. Use web fetch to read both:
   - https://github.blog/latest/
   - https://github.blog/changelog/
3. Identify recent, verified updates that help developers learn GitHub faster. Keep the page short and practical, follow Mona's editorial notes, and avoid repeating or speculating about announcements.
4. Edit only `site/content/github-info.md`. Add a clear source link for every item based on the GitHub Blog or Changelog.
5. If there is a meaningful, well-sourced update, use the configured `create-pull-request` safe output to open a focused pull request against `main` for review. Summarize the changes and their sources in the PR description. Never write directly to `main` or use another mechanism to create or push changes.
6. If neither source provides a useful update, or the evidence is insufficient, make no changes and call `noop` with a brief reason.

For examples of reusable GitHub workflow patterns, see [Awesome Copilot workflows](https://awesome-copilot.github.com/workflows/).
