---
name: job-search
description: Finds recent software engineering jobs matching a candidate profile, filters obvious mismatches, removes duplicates, and writes a simple Markdown report with direct application links.
license: MIT
compatibility: opencode
metadata:
    domain: job-search
    stage: discovery
---

# Job Search Skill

## Purpose

Find recent, active job postings that match the candidate profile and produce a
simple, honest list the candidate can act on.

## Required Inputs

Read:

- `private/candidate-profile.md`
- `private/resume.md`

Extract target titles, target levels, locations, remote or hybrid preference,
required immigration support, preferred technologies, and hard exclusions.

## Search

Run several searches instead of stopping after one.

1. Start with the freshest postings (last 24 hours).
2. Widen to the last 3 days if needed.
3. Widen to the last 7 days if still needed.

Search across multiple source categories:

- Search-engine results
- Company career pages
- ATS-hosted job pages (Greenhouse, Lever, Ashby) when they appear
- LinkedIn, Indeed, and Glassdoor as discovery sources

Prefer a direct company or ATS application link over a job-board redirect.

## Filtering

Skip a job when any of the following is true:

- It requires an active security clearance.
- It explicitly requires United States citizenship.
- It is clearly below the candidate's target level.
- It is primarily QA, support, sales engineering, customer success, or DevRel.
- It is from a staffing agency or consulting body-shop.
- It has no verifiable active application page.
- It is a duplicate of a stronger result.

Remove duplicate roles: the same company and substantially similar title in the
same location should appear once.

## Output Fields

For every retained job, record:

- Company
- Job title
- Location
- Work arrangement (remote, hybrid, onsite, or unknown)
- Direct application link
- Job listing link
- Posting age or `unknown`
- A short note on why it matches
- Any important gap

Use `unknown` when information cannot be verified. Never guess.

## Link Validation

Before including a job, open the direct application link and confirm the page is
accessible and matches the company and title. Drop inactive or expired pages.

## Report

Write the report to `output/YYYY-MM-DD-jobs.md`. If that file already exists,
write `output/YYYY-MM-DD-jobs-2.md` and continue incrementing. Never overwrite an
existing report.

Structure:

```markdown
# Job Search Report — YYYY-MM-DD

## Profile
<Target roles, target levels, locations, key constraints>

## Matches

### <Company> — <Title>
- Location: <location>
- Work arrangement: <remote | hybrid | onsite | unknown>
- Posted: <posting age or "unknown">
- Apply: <direct application link>
- Listed at: <job listing link>
- Why it matches: <short note>
- Gap: <important gap or "none noted">

## Limitations
<Sources or information that could not be verified, and any reason the result
count was lower than expected.>
```

## Evidence Rules

- Never display an invented salary or posting date.
- Never call sponsorship guaranteed.
- Do not hide important qualification gaps.
- Prefer a direct company URL.
- Clearly label inference as inference.

## Completion

The search is complete when several queries have been run, duplicates and
obvious mismatches are removed, every retained job has a direct application
link, and the report is saved under `output/`.
