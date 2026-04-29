# Claude Code Methodology

Personal methodology for working with Claude Code across all projects.

This repo is the source of truth for two things:

1. **`CLAUDE.global.md`** — installed at `~/.claude/CLAUDE.md` on every
   machine where I run Claude Code. Defines the methodology, project
   tiers, and warning behaviour. Identical across all machines.

2. **`CLAUDE.project-template.md`** — copied into the root of each new
   project as `CLAUDE.md` and filled in for that project. Captures
   architecture, stack, env vars, services, hurdles, and post-implementation
   checklist for that specific project.

Influences: Fábio Akita's writing on AI-paired Extreme Programming
(particularly the M.Akita Chronicles series at akitaonrails.com) and the
"Método Fábio Akita" video discussion.

---

## Installation

On each machine:

```sh
mkdir -p ~/.claude
cp CLAUDE.global.md ~/.claude/CLAUDE.md
```

Re-run after every update to this repo. (A small shell function or
`make install` target can automate this — left as a future improvement.)

---

## Starting a new project

```sh
cd <project-root>
git init                                         # if not already a repo
cp <path-to-this-repo>/CLAUDE.project-template.md CLAUDE.md
# Fill in project name, tier, stack, etc.
git add CLAUDE.md
git commit -m "chore: add project CLAUDE.md"
```

The project's `CLAUDE.md` is mandatory before any other work begins.

---

## Updating the methodology

The global file evolves. When something here proves wrong, missing, or
unclear in real project work:

1. Open a branch: `git checkout -b improve/<short-name>`
2. Edit the file. Commit with a clear `docs:` or `chore:` message
   explaining *why* it changed, not just *what*.
3. Merge to `main`.
4. Re-install on each machine.

The git history of this repo is itself a record of how my engineering
thinking has evolved. Treat it as such.

---

## Project tiers (summary)

| Tier | Name | Examples | TDD | Deploy | Security | Hosting |
|---|---|---|---|---|---|---|
| 1 | Sandbox | CTF, vulnerable VMs, spikes | Optional | Optional | Shortcuts allowed | Public personal account |
| 2 | Learning | Personal tools, study projects | Enforced for reusable code | Optional | Basic hygiene | Public personal account |
| 3 | Earning | Freelance, paid content | Full | Disciplined | Full baseline | Private (Blocs org or non-Blocs private space) |
| 4 | Blocs Production | Blocs services, client environments | Full + integration | Change-managed | Full + audit | Blocs private org only |

See `CLAUDE.global.md` for the full tier and hosting definitions.
