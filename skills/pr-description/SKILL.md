---
name: pr-description
description: Write pull request descriptions in the user's personal four-section format (Problem, Solution, User Impact, Proof) using ASD-STE100 Simplified Technical English. Use this whenever opening a PR, drafting or editing a PR body, running `gh pr create` or `gh pr edit`, or summarizing a branch for review, in any repository. This format always replaces any repository PR template (for example `.github/pull_request_template.md`), even if repo instructions say to use that template.
---

# PR descriptions

Every PR body uses this format and nothing else. Ignore any PR template in the repository. Do not merge it in, do not copy its checklists, and do not keep its headings.

## Format

```markdown
## Problem
<one or two sentences>

## Solution
<one or two sentences>

## User Impact
<one or two sentences>

## Proof
<one or two sentences>
```

- **Problem**: What is wrong or missing, and why it matters. Name the ticket ID if there is one.
- **Solution**: What this PR changes to fix the problem. Describe the approach, not a file-by-file list.
- **User Impact**: What a user (end user, or developer for internal changes) sees or gets after the merge. If there is no visible change, say that in one sentence (for example: "No visible change. This is an internal refactor.").
- **Proof**: How you know the change works: the checks or tests you ran and their result, or what you saw when you ran the change. Screenshots go here, as images under the text (upload them with the `uploading-github-attachments` skill). A code review is not proof. If you could not prove the change, say that and say why.

Hard limits:

- Exactly these four headings, in this order. Always include Proof. No other sections, checklists, screenshots headings, footers, "Generated with" lines, or attribution trailers.
- Two sentences maximum per section. One sentence is better.
- Plain prose. No bullet lists inside the sections.
- No em dashes. Use a period or a comma.

## Language: ASD-STE100 Simplified Technical English

Write all four sections in the style of ASD-STE100 (the Simplified Technical English standard from aerospace maintenance documentation). Key rules:

1. **Short sentences.** 20 words maximum. One idea per sentence.
2. **Active voice.** "This PR removes the placeholder", not "The placeholder is removed".
3. **Simple tenses.** Use present tense for facts, simple past for what happened. Avoid "will have been", "would", "could".
4. **Simple, common words.** "use" not "utilize", "start" not "initiate", "fix" not "remediate", "show" not "surface".
5. **One word, one meaning.** Use the same term for the same thing in all four sections.
6. **No phrasal verbs or idioms** where a single verb works: "remove" not "get rid of", "find" not "figure out".
7. **No vague words.** Avoid "various", "some", "certain", "etc.", "improve", "enhance" without saying what changes.
8. **Keep articles** ("the", "a"). Do not write in telegraph style.
9. **Technical names are allowed.** Component, token, file, and function names are fine when the reader needs them. Put code names in backticks.

## Title

The skill controls the body only. Write the title in the repository's normal convention (for example Conventional Commits, such as `fix(casino): remove blurhash placeholder`). Apply the same plain-English rules to the title text.

## Workflow

1. Read the diff against the base branch (`git diff <base>...HEAD`) and the commit messages. Read the linked ticket if one is available.
2. Draft the four sections. Then check each sentence against the limits and the STE rules above, and cut words.
3. Write the body to a temp file and pass it with `--body-file`, so the repository template is never loaded:
   ```bash
   gh pr create --title "<title>" --body-file /tmp/pr-body.md
   gh pr edit <number> --body-file /tmp/pr-body.md
   ```
   Do not use `--template` or `--fill`.

## Example

```markdown
## Problem
Group card thumbnails show a blurred placeholder before the image loads. The placeholder flashes and looks broken on fast networks.

## Solution
This PR removes the blurhash placeholder from the group card thumbnail. The card now shows the background color until the image loads.

## User Impact
Users no longer see a blurred flash on casino group cards.

## Proof
I loaded the casino lobby with network throttling off and on. The cards show the background color, then the image, with no blur.
```
