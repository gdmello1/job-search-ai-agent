---
description: Create or update your local candidate profile from your resume
---

Set up the candidate profile for this job-search project.

Optional material supplied for this run:

$ARGUMENTS

If the arguments contain a file path, read that file as the resume source. The
file must be inside this project (for example `private/my-resume.pdf`). If the
arguments contain pasted resume text, use it directly. Otherwise, ask the user
to share their resume material.

Load the `profile-setup` skill and follow it exactly. It performs onboarding
only: it parses resume material and writes the private profile files. It must
not search for jobs.

Use these files as structural templates:

@examples/resume.example.md

@examples/candidate-profile.example.md

Create `private/` if it does not exist, then write:

- `private/resume.md`
- `private/candidate-profile.md`

Never fabricate any detail. Label unknown values as unknown. Keep all private
data local to `private/`, never send it to any external service, and never
commit it.

After writing the files, ask the user to review them and fix anything wrong or
missing, then run `/jobs` when ready.
