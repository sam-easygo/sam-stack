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

These skills are copied unchanged from [t3dotgg/tstack](https://github.com/t3dotgg/tstack/tree/92e38e2/skills) at commit `92e38e2`, under the MIT license in [`licenses/tstack-LICENSE`](licenses/tstack-LICENSE):

`full-stop`, `full-send`, `sol-loop`, `file-pr`, `babysit-pr`, `leaving-pr-comments`
