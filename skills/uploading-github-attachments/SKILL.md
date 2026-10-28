---
name: uploading-github-attachments
description: Use when attaching a screenshot, image, or video to a GitHub PR, issue, or comment, or embedding a local image in a PR or issue body. Also covers highlighting the changed area of a UI screenshot before upload.
---

# Uploading GitHub attachments

Use the `--attach` flag (gh 2.99+, GitHub.com only). It works on
`gh pr` and `gh issue` `create`, `edit`, and `comment`. Repeat it for more files.

```sh
gh pr edit 23 --attach './after.png#Login error after the fix'
gh pr comment 23 --attach ./before.png --attach ./after.png
```

- Text after `#` is the alt text. Videos have no alt text.
- To place an image, put `![alt](./after.png)` in the body and pass the same
  path to `--attach`. gh replaces the path with the uploaded URL. It appends
  files that the body does not reference.
- `edit --attach` with no body flag keeps the current body.
- A non-zero exit can mean some files uploaded. Check the PR before you retry.

## Highlight the change

If the change is hard to see, outline it on the live page before the
screenshot. Use `page.evaluate` or `browser_evaluate` to set
`outline: 3px solid #ff3b30` on the element that contains the whole changed
area. Use the same element for the before and after screenshots.
