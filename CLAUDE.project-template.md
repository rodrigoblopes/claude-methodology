# Project — `<PROJECT_NAME>`

> This file is the living **technical** spec for this project. It is loaded
> by Claude Code at every session and read before each significant action.
> Keep it current. When something changes (a new pattern emerges, a hurdle
> is solved, a service is added), update this file as part of that change.
>
> **What does NOT belong here:** business reasoning, pricing logic, real
> client names or identifiable client context, competitive positioning,
> revenue-relevant decisions, sales notes. Those live in `BUSINESS.md`
> outside the repository entirely. See "Content classification" in the
> global `CLAUDE.md` for the rules.
>
> If you find yourself writing "the business case for this is…" or "we
> charge…" or "client X wants…" — stop. That content goes elsewhere.

---

## Project tier

**Tier:** `<1 — Sandbox | 2 — Learning | 3 — Earning | 4 — Blocs Production>`

**Rationale:** `<one-line justification for why this tier>`

The tier governs how strictly the global methodology is enforced. See the
global `CLAUDE.md` for what each tier requires.

---

## Repository hosting

**Host:** `<public personal account | Blocs private org | non-Blocs private space>`
**Visibility:** `<public | private>`
**Owner identity:** `<which account/org owns this — must match tier>`
**Public-readable artefacts:** `<which parts of this project, if any, are
intended to be visible to outside readers — e.g. "README only", "all of
it", "nothing">`

This must match the tier's hosting requirements in the global `CLAUDE.md`.
A Tier 3 or 4 project on a public host, or a Tier 1/2 project that nobody
can see, is a misconfiguration that needs fixing before further work.

---

## Personal data handled

**Third-party personal data stored:** `<none | list the kinds — e.g.
emails, phone numbers, location, payment details, private messages>`
**Applicable regulation:** `<none | LGPD | GDPR | ...>`
**Minors among users?** `<yes | no | unknown>`
**Encrypted at rest:** `<which fields, and how>`

If this is anything other than "none", the project meets the full Tier 3
security baseline whatever its tier. See "Third-party personal data
overrides the tier" in the global `CLAUDE.md`.

---

## One-line description

`<What this project is, in one sentence. If you can't explain it in one
sentence, you don't understand it well enough yet.>`

---

## Goals and non-goals

**Goals:**
- `<What this project must accomplish.>`
- `<Specific, observable outcomes.>`

**Non-goals:**
- `<What this project explicitly will not do. Equally important — prevents
  scope creep and clarifies decisions.>`

---

## Architecture overview

`<High-level description of how the system is structured. What are the
major components? How do they communicate? Where does data flow? What's
synchronous vs asynchronous? Diagram in ASCII or a description in prose
— whichever communicates better.>`

---

## Tech stack

**Languages:** `<e.g. Python 3.12, TypeScript 5.4>`
**Frameworks:** `<e.g. FastAPI, React 18>`
**Data stores:** `<e.g. PostgreSQL 16, Redis 7>`
**Background jobs:** `<e.g. Celery, Sidekiq, none>`
**Deployment target:** `<e.g. Docker on Hetzner VPS via Kamal, none yet>`
**Testing:** `<e.g. pytest + pytest-asyncio, vitest>`
**Test oracle:** `<what tests check against — real system, reference data,
spec, known-good output>`
**Linting / formatting:** `<e.g. ruff, prettier>`
**CI:** `<e.g. GitHub Actions — runs tests on every push, deploys only on
green; none yet>`
**Verification commands:** `<exact commands the agent runs to test, lint
and build — e.g. "pytest -q", "npm run lint">`
**Other notable tooling:** `<e.g. Pax8 SDK, SentinelOne API, ...>`

---

## Environment variables

Every variable the project reads. Never commit actual values — this is the
contract, not the secret store.

| Variable | Purpose | Required? | Example / default |
|---|---|---|---|
| `EXAMPLE_VAR` | What it controls | Yes/No | `placeholder` |

Secrets are managed via `<password manager / vault / .env (gitignored)>`.

---

## Directory structure

```
<project-root>/
├── README.md
├── CLAUDE.md                # this file
├── AGENTS.md                # optional: symlink/copy of CLAUDE.md for other agents
├── DECISIONS.md             # architectural decisions log (Tier 4)
├── <src or app dir>/
│   ├── ...
├── tests/
│   ├── unit/
│   ├── integration/
│   └── ...
├── docs/
└── ...
```

`<Annotate non-obvious directories. Note conventions: where do new modules
go? Where do migrations live? Where does generated content go?>`

---

## Services, jobs, and models

### Services

`<For each major service / module: name, responsibility, key public
interface, dependencies. One paragraph each.>`

### Background jobs

`<For each scheduled or async job: name, schedule (cron expression or
trigger), what it does, idempotency notes, failure mode.>`

### Data models

`<For each significant model / entity: name, key fields, relationships,
invariants. Not exhaustive — focus on the ones whose shape matters for
reasoning about the system.>`

---

## Design patterns used in this project

`<The specific patterns and conventions this project follows. Not generic
patterns from a textbook — the ones we've actually decided on for this
codebase. Examples: "All external API calls go through a single
ResilientClient wrapper", "Domain errors inherit from DomainError, never
raise stdlib exceptions across module boundaries", "Repository pattern
for data access — no ORM calls in service layer".>`

---

## Pipeline / schedule

`<If this project has a recurring pipeline (a weekly newsletter, a daily
ingest, a build/deploy cadence), document the full cycle here with times
and dependencies.>`

Example shape:

| Time (local) | Step | Owner | Notes |
|---|---|---|---|
| Mon 06:00 | Step 1 | system | What runs, what it produces |
| Mon 06:30 | Step 2 | system | Depends on step 1 |

---

## Common hurdles and their solutions

> Curated list of problems we've hit and how we solved them. Future-you
> and the agent both consult this before re-debugging things we've
> already debugged. Keep it current, not append-only: merge duplicates
> and remove entries that no longer apply (a dependency was dropped, the
> code was rewritten). Stale entries are noise that crowds out the useful
> ones.

### `<short title of the problem>`

**Symptom:** `<what you observe>`
**Cause:** `<what's actually happening>`
**Solution:** `<what to do>`
**Why this isn't obvious:** `<why we got tripped up — helps recognise the
shape of the problem next time>`

---

## Open threads

> Unfinished work, pending decisions and known follow-ups, so a new
> session (or you after a break) can pick up without the old
> conversation. Remove an item when it's done.

- `<YYYY-MM-DD — what's pending, and where it stands>`

---

## Post-implementation checklist

Before any feature is considered "done", verify:

- [ ] All new behaviour covered by tests; tests pass locally.
- [ ] Every bug fixed in this change has a regression test that failed
      before the fix.
- [ ] Linter and formatter clean.
- [ ] (Tier 3+, recommended for Tier 2) CI is green on the pushed
      commit.
- [ ] No hardcoded secrets, credentials, or environment-specific paths.
- [ ] Security checks reported as what was actually run and what was
      not — never as "it's secure".
- [ ] Any new personal data collected is declared in "Personal data
      handled", is actually needed, and is encrypted at rest.
- [ ] Error paths handled — what happens when this fails?
- [ ] Idempotency considered — what happens if this runs twice?
- [ ] Logs at appropriate level — enough to debug, not so much it's noise.
- [ ] Documentation updated — README, this file, runbook if applicable.
- [ ] Commits are small, well-titled, and tell a coherent story.
- [ ] `CLAUDE.md` updated if architecture, stack, env, or patterns changed,
      stale entries trimmed, and "Open threads" current.
- [ ] (Tier 3+) Deployment notes updated.
- [ ] (Tier 4) `DECISIONS.md` updated if a significant choice was made.

---

## Project-specific overrides

`<Any places where this project deliberately diverges from the global
methodology. Each override must be justified — "we're doing X because Y"
— not just declared. If a deviation comes up repeatedly without
justification, that's a sign the global methodology needs revisiting,
not that this project should ignore it.>`

---

## Notes for the agent

`<Free-form section for technical things that don't fit elsewhere but
matter for working on this project. Things like: "the Pax8 sandbox
sometimes returns stale data for 30 seconds after a write — don't
immediately re-query to verify", or "the API rate-limits aggressively at
the /threats endpoint, batch reads".>`

`<Things that do NOT go here: anything about why the business is shaped
the way it is, what clients want, what's being charged, who the
competition is. Those go in BUSINESS.md outside the repo.>`
