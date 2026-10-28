# sam-stack

Personal collection of Claude Code skills.

## Layout

Each skill lives in its own folder under `skills/`:

```
skills/
  <skill-name>/
    SKILL.md
```

## Install on a machine

```sh
git clone git@github.com:sam-easygo/sam-stack.git ~/dev/sam-stack
mkdir -p ~/.claude/skills
for d in ~/dev/sam-stack/skills/*/; do ln -sfn "$d" ~/.claude/skills/"$(basename "$d")"; done
```

Run `git pull` in the repo to get updates. Re-run the loop after you add a new skill.
