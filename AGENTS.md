# Job Search AI Agent

## Purpose

A local AI agent that runs inside OpenCode and finds software engineering jobs
matching a candidate profile. It is not a web application.

## Core Architecture

- `.opencode/commands/profile.md` — `/profile` entry point (build a profile).
- `.opencode/commands/jobs.md` — `/jobs` entry point (search for jobs).
- `.opencode/agents/job-orchestrator.md` — the workflow agent.
- `.opencode/skills/profile-setup/` — parses resume material into a profile.
- `.opencode/skills/job-search/` — finds, filters, and reports matching jobs.
- `examples/` — public templates.
- `private/` — local candidate data; never committed.
- `output/` — generated reports; never committed.

## Principles

1. Keep private candidate data out of Git.
2. Never fabricate salaries, posting dates, or links.
3. Prefer direct company application links over job-board redirects.
4. Never apply to a job or contact a recruiter.
5. Label unknown information as unknown.
6. Report limitations honestly.

## Job Output

Every reported job must include:

- Company
- Job title
- Location
- Work arrangement when known
- Direct application link
- Posting age or an explicit "unknown"
- A short note on why it matches

## Agent Behavior

The agent must:

1. Read the candidate profile.
2. Load the `job-search` skill.
3. Search across several queries and sources instead of stopping after one.
4. Remove duplicate roles.
5. Skip obvious mismatches.
6. Include a direct application link for every job.
7. Write the report under `output/`.
