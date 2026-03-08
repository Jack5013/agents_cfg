# Repo Split Plan

## Target Layout

- `agent_cfg` (current repository)
  - keep: `AGENTS.md`, `opencode.json`, `.opencode/`, `memory/`, docs
  - ignore: `projects/`
- `projects/<name>`
  - each project is an independent git repository
  - each project has its own remote

## Execution Steps

1. In `agent_cfg`, keep `.gitignore` with `/projects/`.
2. For each project directory:
   - run `git init -b main`
   - add files and commit
   - add remote and push
3. Keep cross-project standards in `agent_cfg` docs/templates only.

## Per-Project Bootstrap Commands

```bash
cd projects/<project-name>
git init -b main
git add .
git commit -m "chore: initialize project repository"
git remote add origin <project-remote-url>
git push -u origin main
```

## Notes

- Do not force-push by default.
- Keep credentials out of repo files.
