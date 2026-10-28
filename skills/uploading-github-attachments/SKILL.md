---
name: uploading-github-attachments
description: Use when asked to attach a screenshot or image to a GitHub PR, issue, or comment body; embed a local image file into a PR/issue description; or upload a file to GitHub without a human dragging it into the web UI. Also covers highlighting a region of a UI screenshot (e.g. a before/after comparison) so the change is obvious before it's uploaded.
---

# Uploading GitHub Attachments

Upload local image files to GitHub's undocumented attachment endpoint and embed the returned URLs into a PR/issue/comment body — no browser drag-and-drop needed.

Source technique: https://island94.org/2026/08/programmatically-upload-attachments-to-github-issues-pull-requests-comments

## Steps

1. Get the repo's numeric ID (the endpoint needs this, not `owner/repo`):
   `gh api repos/<owner>/<repo> --jq .id`
2. Get a bearer token: `gh auth token`
3. For each file, POST it to the upload endpoint and capture the returned URL:
   ```bash
   curl -s "https://uploads.github.com/user-attachments/assets?name=<file>&content_type=<mime>&repository_id=<repo_id>" \
     -X POST -H "Authorization: Bearer <token>" \
     -H "Accept: application/json" --data-binary "@<path-to-file>"
   ```
   Returns `{"url": "https://github.com/user-attachments/assets/<uuid>"}`. That URL is permanent and viewable with no further auth.
4. Fetch the PR/issue's **current** body before editing it — don't reuse a body you drafted earlier in the conversation. Something else may have changed it since (this happens same-day, mid-session): `gh pr view <n> --json body --jq .body > <file>`.
5. Edit that file to add or replace the image markdown (`![alt](url)`), leaving the rest of the body untouched.
6. Write it back: `gh pr edit <n> --body-file <file>` (or `gh issue comment --body-file <file>` for a comment).
7. Delete the local scratch files (downloaded body, image copies) once the edit is confirmed.

## Highlighting a region before upload

When the target of a change won't be obvious from the screenshot alone (a small addition in a long list, a one-line diff in a dense page), draw attention to it before uploading rather than describing it in prose after:

- Capture the screenshot via Playwright/Chrome MCP as normal.
- Before the final screenshot, inject a highlight directly on the live page: pick the DOM element that scopes the *whole* changed area, not just the one changed line — a box around a single row implies a 1:1 match between before/after that may not hold when items shift position. Set its `style.outline` (e.g. `3px solid #ff3b30`), `outlineOffset`, and a soft `boxShadow` via `page.evaluate`/`browser_evaluate`.
- Re-screenshot with the highlight applied, then upload that image, not the plain one.
- Use the *same* element/region for both the before and after shot so the reader's eye lands on the same place in each frame.

## Caveats

- The endpoint is unofficial and undocumented — it could change or stop working without notice.
- Re-editing a body to point at a new upload doesn't delete the old asset; it becomes unreferenced but stays live at its URL.
