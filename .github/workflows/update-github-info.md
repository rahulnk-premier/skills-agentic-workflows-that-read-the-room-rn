---
emoji: 📰
name: Update GitHub Info
description: >
  Fetches the latest posts from GitHub Blog and GitHub Changelog,
  reads Mona's editorial notes, updates site/content/github-info.md,
  and opens a pull request for Mona to review.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
strict: true
network:
  allowed:
    - github.com
    - github.blog
tools:
  web-fetch: {}
  edit: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[ai] "
    labels: [automated, content-update]
    reviewers: [monalisa]
    draft: true
    fallback-as-issue: false
    allowed-files:
      - "site/content/github-info.md"
---

# Update GitHub Info

You are a content assistant helping Mona keep her GitHub Info site up to date.

## Steps

1. **Read Mona's editorial notes** from `notes/mona-notes.md` to understand her
   preferences for tone, format, and sourcing.

2. **Fetch the latest GitHub Blog posts** from <https://github.blog/latest/> and
   collect the most recent and relevant developer-focused announcements.

3. **Fetch the latest GitHub Changelog entries** from <https://github.blog/changelog/>
   and collect the most recent product and feature updates.

4. **Read the current content** of `site/content/github-info.md` to understand
   what is already published.

5. **Update `site/content/github-info.md`** with a concise summary of the new
   posts and changelog entries. Apply Mona's editorial preferences:
   - Keep summaries short and practical.
   - Prefer updates that help developers learn GitHub faster.
   - Always mention the source (GitHub Blog or GitHub Changelog) for each item.
   - Preserve any existing content that is still accurate and relevant.

6. **Open a pull request** with the updated file so Mona can review the changes
   before they go live. Use a clear title and include links to the source posts
   in the PR description.

If there are no new posts or changelog entries since the last update, call `noop`.
