# sam-stack

Personal collection of agent skills, installed with [`npx skills`](https://github.com/vercel-labs/skills).

## Layout

Each skill lives in its own folder under `skills/`. The folder name must match the `name` in the frontmatter.

```
skills/
  <skill-name>/
    SKILL.md
```

## Install

```sh
npx skills add git@github.com:sam-easygo/sam-stack.git -g -s '*' -a claude-code codex -y
```

This copies each skill into `~/.agents/skills` (read by Codex) and symlinks it into `~/.claude/skills` (read by Claude Code). The SSH URL is used because the repo is private.

## Update

| Change in this repo | Command                                                              |
| ------------------- | -------------------------------------------------------------------- |
| Edit a skill        | `npx skills update -g`                                               |
| Add a skill         | Run the install command again. `update` does not pick up new skills. |
| Remove a skill      | `npx skills update -g` without `-y`, then confirm the prompt.        |

`update` only removes local copies after you confirm. With `-y`, or without a TTY, it lists the deleted skills and keeps them. To remove one by hand, run `npx skills remove -g <name> -y`.

## Third-party skills

These skills come from [t3dotgg/tstack](https://github.com/t3dotgg/tstack/tree/92e38e2/skills) at commit `92e38e2`, under the MIT license in [`licenses/tstack-LICENSE`](licenses/tstack-LICENSE):

- `leaving-pr-comments`: unchanged.
- `babysit-pr`: changed to drop the Macroscope and CodeRabbit notes, and so `pr-wait` exits on PRs without CI or review bots.
- `file-pr`: changed to write PR descriptions with `pr-description` and to run `sol-loop` first.
- `sol-loop`: changed to run before any PR, at high effort in fast mode, and to not add a review note to the PR.
- `full-stop`: merged with tstack's `full-send` into one skill, without permission to merge.
