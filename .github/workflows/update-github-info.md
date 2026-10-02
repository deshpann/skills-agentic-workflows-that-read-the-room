---
name: update-github-info
description: Refresh Mona's GitHub Info page with concise, source-linked updates from the GitHub Blog and Changelog.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
tools:
  edit:
  web-fetch:
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    max: 1
    allowed-files:
      - "site/content/github-info.md"
---

# Update GitHub Info for Mona

Refresh the site's GitHub information page using current, verifiable information.

## Steps

1. Read `notes/mona-notes.md` and `site/content/github-info.md`. Preserve Mona's editorial angle, existing useful material, and concise practical style.
2. Use web-fetch to read both `https://github.blog/latest/` and `https://github.blog/changelog/`.
3. Select only recent items that offer practical value to developers and fit the page's existing themes. Verify every detail against its source; do not infer or invent facts.
4. Update only `site/content/github-info.md`. Keep additions short and include the direct source URL for every item based on the GitHub Blog or Changelog. Retain relevant existing content and avoid duplicating items already covered.
5. If there is no useful, non-duplicative update, make no change and do not open an empty pull request.
6. When the page changes, use the `create-pull-request` safe output to open one pull request against the repository's default branch for Mona to review. Summarize the updates and cite their sources in the pull request description. Never merge the pull request or write directly to the default branch.
