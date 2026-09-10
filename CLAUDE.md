# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Quick Orient (every session)

1. Read `plan/roadmap.md` - find the current sprint
2. Read the active sprint file in `plan/sprints/` - macro goals + task list
3. Check `plan/tasks/` for any open ticket referenced by the sprint
4. Read `.GCC/main.md` + the last few entries of `.GCC/log.md` - recent decision trail
5. If `MEMORY.md` exists: read it for cross-session user state
6. Start working on the first non-completed task

## Project

**Status:** <!-- e.g. Phase 1 in progress. Sprint 1.2 active. -->
**Owner:** <!-- Name -->

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | <!-- e.g. Next.js 15, TypeScript --> |
| Backend | <!-- e.g. Python / Flask --> |
| Database | <!-- e.g. Supabase PostgreSQL --> |
| Auth | <!-- e.g. Supabase Auth --> |

## Commands

```bash
# Setup
# <!-- fill in -->

# Run
# <!-- fill in -->

# Build / verify
# <!-- fill in -->
```

## Key Files

| File | Role |
|------|------|
| <!-- path --> | <!-- purpose --> |

## Gotchas

- <!-- e.g. Score column is `overall_score` (NOT `score`) -->

## plan/ - Single Source of Truth

If it's not in `plan/`, it doesn't exist.

| Need | Read |
|------|------|
| Navigation hub | `plan/README.md` |
| Vision + revenue + core features | `plan/PRODUCT_VISION.md` |
| Client deliverables + milestones | `plan/DELIVERABLES.md` |
| Current phase + what's next | `plan/roadmap.md` |
| What tech and why? | `plan/techstack.md` |
| How a component works | `plan/architecture/` |
| Why a decision was made | `plan/decisions/` |
| External services & APIs | `plan/providers/` |
| Research findings | `plan/research/` |
| Sprint overview (macro) | `plan/sprints/sprint-X.Y-*.md` |
| Individual tickets (micro) | `plan/tasks/task-XXX-*.md` |
| Old / superseded docs | `plan/archive/` |

### sprints/ vs tasks/ - macro/micro split

- **`sprints/`** - macro. One file per sprint. Goal, context, task list with acceptance criteria, done-when.
- **`tasks/`** - micro. GitHub-ticket-style. One file per item that earns its own page: detailed spec, investigation notes, open questions, cross-sprint follow-ups.

Small items stay inline in the sprint file. Promote to `tasks/` only when an item outgrows its bullet.

## .GCC/ - AI Decision Memory

Two files, committed to git. Survives token limits, lets a new agent pick up where you left off.

```
.GCC/
├── main.md          # Objectives, milestones, active experiment branches
├── log.md           # OTA decision trail (max 50 entries)
└── branches/        # Experiment isolation (create only when spiking)
    └── <name>/
        ├── summary.md
        └── log.md
```

### When to append to `log.md`

Every meaningful decision point. **If you skip this, you lose the next session.** Trigger moments:

- Chose approach A over B (why)
- Hit a dead-end and pivoted (what you learned)
- Session ends mid-investigation (what you were about to try next)
- Discovered a non-obvious constraint

Format:

```
---
**[OTA-###]** YYYY-MM-DDTHH:MM:SSZ
- **Observation:** what you noticed
- **Thought:** your reasoning
- **Action:** what you did (or left for next session)
```

Max 50 entries. Drop the oldest when you exceed.

### When to update `main.md`

- Sprint completed → add a milestone line
- New experiment branch → add to Active Branches
- Branch merged/abandoned → remove from Active Branches

### Experiment branches

When you want to try a risky/parallel approach without polluting the main trail:

```bash
mkdir -p .GCC/branches/try-websockets
# Add an Active Branches entry in .GCC/main.md
# All OTA logging during the experiment goes to .GCC/branches/try-websockets/log.md
# When done: write summary.md, merge findings into main.md, remove from Active
```

## MEMORY.md - Cross-Session User Memory

If `MEMORY.md` exists (repo root or `~/.claude/projects/<slug>/memory/`), read it for:

- Current phase / sprint (user-maintained view)
- Key gotchas not obvious from code
- User preferences, past feedback
- Links to per-topic memory files

Update on sprint close.

## While Writing Code

- Follow patterns already in the codebase
- Don't add features or "improvements" beyond the task
- Don't add comments, docstrings, or type annotations to code you didn't change
- Keep solutions simple - three similar lines beat a premature abstraction

## Sprint Close Checklist

Single source of truth. `README.md` links here.

1. Mark all sprint tasks `completed` in the sprint file
2. `plan/roadmap.md` - mark sprint done, update phase summary, add date
3. **This file (`CLAUDE.md`)** - update Status line
4. Move sprint file: `plan/sprints/sprint-X.Y-*.md` → `plan/sprints/archive/`
5. Move resolved tickets: `plan/tasks/*.md` → `plan/tasks/archive/`
6. `.GCC/main.md` - add milestone line
7. `MEMORY.md` (if using auto-memory) - update Current State
8. Merge branch to `main`

## Git Workflow

- Branch per sprint: `sprint/X.Y-short-name`
- Merge to main when complete and tested
- Don't push to main directly
