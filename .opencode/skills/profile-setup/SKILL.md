---
name: profile-setup
description: Builds a local candidate profile from pasted resume text or a resume file. Use when the user runs /profile, asks to create or update their candidate profile, or provides a resume to onboard into this job-search project. Writes private/resume.md and private/candidate-profile.md locally.
license: MIT
compatibility: opencode
metadata:
    domain: job-search
    stage: onboarding
---

# Profile Setup Skill

## Purpose

Convert resume material into two private files the job search depends on:

- `private/resume.md`
- `private/candidate-profile.md`

This skill performs setup only. It does not search for jobs, apply to anything,
or contact anyone.

## Privacy Rules

1. Resume material is personal data. Never send it to any external service.
2. Write private data only under `private/`. Never write it to a public path or
   `examples/`.
3. Never commit anything.
4. Do not store secrets, tokens, or credentials.

## Required Outputs

| File | Source |
|---|---|
| `private/resume.md` | parsed resume material |
| `private/candidate-profile.md` | parsed resume + user answers |

Keep the field names and section structure used by
`examples/resume.example.md` and `examples/candidate-profile.example.md`.

## Accepted Inputs

1. Pasted resume text in the chat.
2. A local file inside this project (for example `private/my-resume.pdf`).
3. Pasted LinkedIn profile content.

If a source is a file, record its path in the profile. Leave the original file
where it is.

## Workflow

1. Check for an existing profile. If `private/candidate-profile.md` exists, ask
   whether to overwrite, update, or cancel. Never silently overwrite.
2. Collect the resume material from the user.
3. Parse it without inventing anything. Write `unknown` for anything absent.
4. Ask the user for job-search preferences: target roles, target levels,
   locations, remote or hybrid preference, immigration needs, compensation,
   company preferences, and hard exclusions.
5. Write `private/resume.md`, then `private/candidate-profile.md`.
6. Tell the user to review the files, then run `/jobs`.

## Parsing Rules

- Use only what is present in the material. Write `unknown` for absent values.
- Never fabricate dates, salaries, titles, employers, or links.
- Preserve metrics exactly as written.
- If two sources conflict, keep the newer or more complete one.

## Candidate Profile Shape

Follow `examples/candidate-profile.example.md`. At minimum capture:

- Current level and total experience
- Target roles in priority order
- Target levels (preferred, stretch, exclude)
- Preferred technologies
- Location and remote or hybrid preference
- Immigration needs
- Compensation expectations
- Company preferences
- Hard exclusions

## Completion

Setup is complete when both files exist under `private/`, no fabrication is
present, unknown fields are labeled, and the user has been told to review the
files and run `/jobs`.
