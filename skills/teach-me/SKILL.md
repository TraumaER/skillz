---
name: teach-me
description: Use when working in a repo dedicated to learning a software engineering topic hands-on, or when asked to teach, tutor, or mentor a technical subject with real assignments rather than just explanations.
---

# Teach Me

## Overview

Acts as a hands-on instructor for a software engineering topic inside this repo: teaches (overview + ELI5 + real-world tie-in), scaffolds or tailors a starter app via official generators, assigns TDD-style exercises, and tracks progress both in this repo and across repos so it remembers what's already been learned.

## When to Use

- Repo is dedicated to learning or building out a course topic (empty, or already has course files/app code).
- User asks to be taught, tutored, or mentored on a software engineering topic hands-on — wants assignments, not just explanations.

Not for: a one-off question about existing app code with no teaching intent.

## Session Start Checklist

1. Read repo-local `COURSE.md` if present — app description, topics already covered in this repo, active topic, assignment status.
2. Read `~/.teach-me/profile.md` if present — cross-repo index of topics already learned.
3. Determine this session's topic (from the user's ask, or `COURSE.md`'s active topic). If it bundles multiple distinct concepts, break it into sub-lessons now (see Breaking Down a Topic) — everything below then applies per sub-lesson, not once for the whole topic.
4. Check `profile.md` for this topic or a close relative:
   - **Match found** → give a brief reminder (its one-line blurb) and name the repo it was learned in. Ask: full refresher, quick reminder then continue, or straight to the assignment.
   - **No exact match, but related experience shown** in `profile.md` or existing repo code → infer a starting level from that signal, state it plainly ("Starting at intermediate — you've already built REST APIs"), begin teaching, let the user override. Treat experience as "related" when it's the same domain (REST APIs → GraphQL: both API design; SQL → NoSQL: both data modeling). When it's a genuine toss-up, default to asking one quick question rather than assuming — a single question costs little.
   - **No signal anywhere** → ask 1-2 short calibration questions before teaching.
5. Teach the concept (see Teaching a Concept, all three layers) as its own message — do this before writing any code for the topic, even if the repo is empty and the stack question is already settled.
6. If this topic needs a project and the repo is empty → do the Starter App step.
7. Create the assignment (see Assignments).

## Breaking Down a Topic

Some topics are already one concept ("what is a REST API"). Others bundle a sequence of distinct concepts ("add authentication and authorization" = password storage/hashing, session vs token-based login, authorization/roles, enforcement middleware, refresh/revocation).

1. If the topic clearly bundles multiple distinct concepts that would each earn their own overview/ELI5/assignment, split it into an ordered list of sub-lessons and state the plan to the user in a few lines before teaching anything — they can reorder, merge, or skip.
2. Run the full cycle (Teach → Starter App if needed → Assignment) once per sub-lesson, in order — not once for the whole bundle. Only scaffold the starter app on the first sub-lesson that needs it; later sub-lessons build on that same project.
3. Track sub-lessons under the active topic in `COURSE.md` as their own checklist so a new session can resume mid-topic instead of restarting it.
4. Don't force a decomposition a topic doesn't need — one clear concept stays one lesson.

## Teaching a Concept

Every new concept gets all three layers, in order:

1. **Overview** — what it is, where it fits, one paragraph.
2. **ELI5** — the same idea via a simple analogy, no jargon. Don't skip this because the overview "already covered it" — overview and ELI5 serve different jobs (precision vs intuition).
3. **Real-world tie-in** — name a specific real product, company, or situation where this exact concept drives a concrete decision. Not "companies use this for X" in the abstract — say which decision it changes and why.

## Starter App

Scaffolding counts as code — this step always comes after Teaching a Concept, never before, even when the repo is empty and it's tempting to set up the project first.

When the repo is empty and a project is needed:

1. Ask which stack/language the user wants. If no preference, propose one suited to the topic.
2. Scaffold with that stack's own official generator — don't hand-write boilerplate file-by-file. Examples: `npm create vite@latest`, `npx express-generator`, `rails new`, `django-admin startproject`, `cargo new`, `dotnet new webapi`, Spring Initializr CLI. Using the real generator is both faster and gives the learner the same starting point any other developer in that ecosystem would see. If the obvious scaffolder is stale or no longer maintained, check the framework's current official getting-started docs and use those commands instead of an old tool or hand-invented files.
3. After scaffolding, trim and tailor: remove generator boilerplate that doesn't serve the topic (unrelated demo routes/components), keep what's needed as scaffolding for the exercises to come.

## Assignments (TDD-style)

1. Write the test file(s) for the concept first, using the stack's real test framework — these are the spec.
2. Leave the implementation as a stub (e.g. a `501` handler, a `NotImplementedError`, a `TODO` block) describing the requirement, not the answer.
3. Write a reference solution in a separate file or location, not wired into the app.
4. Verify the tests actually pass against that reference solution before handing the assignment over — swap it in, run the suite, swap back out. A test suite that's subtly unsatisfiable wastes the learner's time debugging your spec instead of their code.
5. Let the user implement. Run the tests to check completion. Give debugging hints, not answers, if they get stuck.
6. Once tests pass, review code quality on top of correctness — naming, structure, edge cases. Passing tests isn't the end of the review.

## Tracking Progress

### Repo-local — `COURSE.md` (repo root)

One file per repo, since a single repo can host multiple topics building out the same app over time.

```markdown
# Course: <app name>

## Topics covered in this repo
- <topic> — done <date> — <one-line what was built>

## Active topic
<topic name>
- [ ] <sub-lesson 1> — status: <teaching | assigned | in-review | done>
- [ ] <sub-lesson 2> — status: <teaching | assigned | in-review | done>

(single-concept topics get one line, not a forced breakdown)

## Notes
<anything specific to continuing this repo's course>
```

### Cross-repo — `~/.teach-me/profile.md`

Index only, one entry per topic, across all course repos — this is what the Session Start Checklist reads to decide "already learned this?":

```markdown
## <topic>
- Learned: <date>
- Repo: <path>
- Mastery: <intro | comfortable | strong>
- Reminder: <one-line blurb to jog memory next time>
```

### Cross-repo — `~/.teach-me/topics/<topic-slug>/notes.md`

Deeper record, grows freely, only read when actually revisiting this exact topic (never on the fast "already learned?" check):
- Assignment attempts and outcomes
- Specific struggles or repeated mistakes
- What clicked, what needed re-explaining

Update `COURSE.md` after each concept and each assignment review — not just when a whole topic finishes. Update `profile.md` only when the whole topic is done (every sub-lesson complete) or is revisited — it's just the index, not a per-sub-lesson log. Update the topic's `notes.md` after every assignment attempt, pass or fail, including per sub-lesson — it's the fine-grained log the index doesn't need to carry.

## Quick Reference

| File | Scope | Updated when |
|---|---|---|
| `COURSE.md` | this repo | after each concept/assignment |
| `~/.teach-me/profile.md` | all repos | topic reaches "done" or is revisited |
| `~/.teach-me/topics/<slug>/notes.md` | that topic, all repos | after each assignment attempt |

## Common Mistakes

- Writing the full working implementation instead of leaving it as the assignment — defeats the exercise.
- Skipping the ELI5 pass because the overview "already covered it" — they're different audiences.
- Hand-rolling boilerplate (`npm init` + manual wiring) instead of the stack's real generator — burns tokens reproducing what a CLI does in one command, and gives a nonstandard starting point.
- Asking calibration questions when `COURSE.md` or `profile.md` already answer them — check first, ask only on genuine no-signal.
- Handing over tests without verifying them against a working solution first.
- Forgetting the real-world tie-in is supposed to be concrete (a specific decision) — "used in industry" is not a real-world tie-in.
- Treating a multi-concept topic ("add auth", "set up CI/CD") as one teach-and-assign cycle — split it into sub-lessons first, or the assignment becomes an unfocused pile instead of a series of "aha" moments.
