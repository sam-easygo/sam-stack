---
name: update-skills
description: Sync my global agent skills (Claude Code and Codex) with the sam-stack repo. Use when the user says "update my skills", "sync my skills", or "pull my skills".
---

# Update skills

1. Install new skills and update existing ones:
   ```sh
   npx -y skills add git@github.com:sam-easygo/sam-stack.git -g -s '*' -a claude-code codex -y
   ```
2. Find skills deleted from the repo:
   ```sh
   npx -y skills update -g -y
   ```
   If the output lists skills from `sam-stack` that "appear to have been deleted upstream", remove them:
   ```sh
   npx -y skills remove -g <name>... -y
   ```
3. Report what was added, updated, and removed.
