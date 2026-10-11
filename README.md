# Job Search AI Agent

A local AI agent that finds software engineering jobs matching your profile.
It runs entirely inside [OpenCode](https://opencode.ai) — no web app, no server,
no account. Your resume and candidate data stay on your machine.

Give it a profile and it searches the web, filters out obvious mismatches,
removes duplicates, and writes a simple report of matching jobs with a direct
application link for each one.

## What it does

- **Build a profile** — run `/profile` and paste your resume. The agent writes a
  local candidate profile you can review and edit.
- **Search for jobs** — run `/jobs`. The agent searches across several queries
  and sources, keeps roles that match your profile, and drops obvious
  mismatches.
- **Read a simple report** — every selected job gets a company, title, location,
  work arrangement, a direct application link, and a short note on why it
  matches.

This is intentionally a small starting point. Scoring, richer filters,
sponsorship analysis, and custom report formats are all things you can add on
top of it.

## Requirements

- [OpenCode](https://opencode.ai) installed.
- A connected model provider (run `/connect` on first launch).
- Web search enabled in your OpenCode setup.

## Quick start

```bash
git clone <your-fork-url> job-search-ai-agent
cd job-search-ai-agent
opencode
```

Then, inside OpenCode:

1. `/connect` — connect a model provider.
2. `/profile` — paste your resume, or pass a file path inside the project (for
   example `/profile private/my-resume.pdf`). This writes
   `private/candidate-profile.md` and `private/resume.md`.
3. Review the files in `private/` and fix anything wrong or missing.
4. `/jobs` — search for matching jobs and write a report under `output/`.

## Commands

| Command | Purpose |
|---|---|
| `/profile` | Create or update your local candidate profile from your resume. |
| `/jobs` | Search for jobs matching your profile and write a report. |
| `/connect` | Built-in OpenCode command to connect a model provider. |

## How it works

`/profile` and `/jobs` are thin entry points. All behavior lives in
`.opencode/` as readable Markdown, so you can inspect and change it.

- `skills/profile-setup` parses resume material into your private profile.
- `skills/job-search` discovers jobs, filters obvious mismatches, removes
  duplicates, and writes the report.
- `agents/job-orchestrator.md` sequences the workflow.

## Privacy

- Your candidate data lives only in `private/`, which is gitignored.
- Generated reports go under `output/`, which is gitignored by default.
- The agent never applies to jobs, submits forms, contacts recruiters, or logs
  in anywhere. It never sends your resume to an external service.

## Extending it

The project is plain Markdown, so it is easy to fork and build on:

- Add a scoring or rating system by editing `skills/job-search/SKILL.md`.
- Add stronger filters or a sponsorship analysis.
- Change the report format in `skills/job-search/SKILL.md`.
- Add a new command under `.opencode/commands/` and a matching skill under
  `.opencode/skills/`.

Keep private data out of Git and never place real candidate data in `examples/`.

## License

MIT. See `LICENSE`.
