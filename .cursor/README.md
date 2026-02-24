# Cursor project config

- **rules/** — Cursor rules (`.mdc` files with YAML frontmatter). Add project conventions, coding standards, and file-specific patterns here.
- **agents/** — Agent configs and instructions. Use for custom agent behavior or shared prompts.
- **skills/** — Project skills. Each skill is a directory (e.g. `skill-name/`) with a `SKILL.md` and optional `reference.md`, `examples.md`, or `scripts/`. Use for reusable workflows (e.g. code review, commit messages, PDF handling).

Project-level agent instructions can also live in `AGENTS.md` at the repo root.
