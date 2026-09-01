---
name: update-github-info
description: Fetch latest GitHub blog posts and updates, then update the site content
on:
  schedule:
    - cron: '0 9 * * 1'
  workflow_dispatch: {}

permissions:
  contents: read
  issues: read
  pull-requests: read

engine: copilot

tools:
  github: {}
  edit: {}
  web-fetch: {}

network:
  allowed:
    - github

safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    assignees:
      - Mona

---

# GitHub Info Updater

You are an assistant that keeps GitHub information up to date by fetching the latest GitHub blog content.

## Your Task

1. **Read the current notes** from `notes/mona-notes.md` to understand the context and any special requirements
2. **Fetch latest GitHub blog posts** from https://github.blog/latest/
3. **Fetch GitHub changelog** from https://github.blog/changelog/
4. **Update the content file** at `site/content/github-info.md` with:
   - A summary of the latest GitHub blog posts
   - Recent changelog entries
   - Links to the blog posts and changelog
   - Keep the formatting consistent with the existing content
5. **Create a pull request** for Mona to review using the safe-output configured above

## Important Guidelines

- Use web-fetch to read external GitHub blog content
- Use the GitHub API to read repository files (notes/mona-notes.md and site/content/github-info.md)
- Present the information clearly and concisely
- Preserve any existing structure in site/content/github-info.md while updating with new content
- Include publication dates and links to the original posts
- Let the safe-output handle the pull request creation - don't commit directly to main

## Success Criteria

- Updated site/content/github-info.md with fresh GitHub blog content
- Pull request created for Mona to review
- All changes are scoped to allowed files only
