# AI Project Scaffold

Minimal project scaffolding for AI-assisted development. Two layers:

1. **`plan/`** - project management (committed). A dev or PM can open this folder and immediately understand what's being built, what's shipped, and what's next.
2. **`.GCC/`** - AI decision memory (committed). Two files that let a new agent pick up where the last one left off without re-reading the whole project.

## Structure

```
your-project/
├── CLAUDE.md                  # AI entry point - read every session
├── .gitignore
├── .env.example               # Copy to .env.local and fill in
│
├── plan/                      # Project management
│   ├── README.md              # Navigation hub - PM starts here
│   ├── PRODUCT_VISION.md      # Vision, revenue, core features, success
│   ├── DELIVERABLES.md        # Client deliverables + acceptance (client work only)
│   ├── roadmap.md             # Feature table + phase summaries (stays lean)
│   ├── techstack.md           # Tech choices + rationale
│   │
│   ├── architecture/          # One doc per major component
│   ├── decisions/             # ADRs - why non-obvious choices were made
│   ├── providers/             # External services & API dependencies
│   ├── research/              # Research briefs, findings, corrections
│   │
│   ├── sprints/               # Macro: one file per sprint
│   │   ├── _TEMPLATE.md
│   │   └── archive/
│   ├── tasks/                 # Micro: one file per ticket (when earned)
│   │   ├── _TEMPLATE.md
│   │   └── archive/
│   │
│   └── archive/               # Superseded docs
│
└── .GCC/                      # AI decision memory
    ├── main.md                # Objectives, milestones, active branches
    ├── log.md                 # OTA decision trail (max 50)
    └── branches/              # Experiment isolation (only when spiking)
```

## The Two Splits

### plan/ - macro / micro

- **Sprint file (macro)** - the "what are we doing this week" view. Goal, context, task list. 3–7 inline tasks.
- **Task file (micro)** - the GitHub-ticket view. Detailed spec, investigation notes, open questions.

**Rule:** start items inline. Promote to `tasks/` only when a single item would dominate the sprint file or needs a life beyond one sprint.

### .GCC/ - roadmap / trail

- **`main.md`** - what this project is and where it's been. Read once per session.
- **`log.md`** - OTA decision trail. Append when a choice is non-obvious or a session ends mid-investigation.

Without the log, the next agent has to rebuild context from scratch. One paragraph at the right moment saves 20 minutes next time.

## Day-to-Day Workflow

### Starting a sprint

```bash
# 1. Add sprint row to plan/roadmap.md feature table
# 2. Create the sprint file
cp plan/sprints/_TEMPLATE.md plan/sprints/sprint-X.Y-name.md
# 3. Create branch
git checkout -b sprint/X.Y-name
# 4. Fill in goal, context, tasks with acceptance criteria
```

### Promoting a task

When a sprint item outgrows its bullet:

```bash
cp plan/tasks/_TEMPLATE.md plan/tasks/task-042-name.md
# Link to it from the sprint bullet
```

### During a sprint

- Update task statuses in the sprint file (`pending` → `in_progress` → `completed`)
- Append to `.GCC/log.md` at decision points (don't skip - that's how context leaks)
- Cross-reference any promoted tickets

### Closing a sprint

Follow the **Sprint Close Checklist** in [CLAUDE.md](CLAUDE.md) - single source, no drift.

## Anti-Bloat Rules

These prevent the organic sprawl that kills token efficiency over time:

1. **`roadmap.md` stays lean** - summary table + short phase sections. Details live in sprint files.
2. **Archive completed sprints and tickets** - keeps active lists short.
3. **No duplicate docs** - the sprint file IS the task list. No TASKS.md, implementation_plan.md, VERIFICATION_CHECKLIST.md.
4. **One concept, one home** - `PRODUCT_VISION.md` owns vision+features; `techstack.md` owns tech; don't duplicate tables.
5. **Architecture docs when earned** - create a component doc when you've built something worth documenting. Don't pre-document planned components.
6. **Decisions when non-obvious** - ADRs capture *why* for choices where the rationale would be lost.
7. **Research when external** - for handoffs, findings, or audits. Internal exploration lives in sprint files.
8. **Providers when complex** - document external deps with gotchas, rate limits, or tradeoffs.
9. **Archive, don't delete** - outdated specs go to `plan/archive/`.

## Setup for a New Project

```bash
# 1. Copy this template
cp -r ai-project-scaffold/ your-project/
cd your-project/

# 2. Initialize git
git init

# 3. Fill in the placeholders
#    - CLAUDE.md: status, tech stack, commands, gotchas
#    - plan/PRODUCT_VISION.md: vision, core features, success criteria
#    - plan/roadmap.md: feature table, Phase 1 outline
#    - plan/techstack.md: technology choices with rationale
#    - .env.example: list required env vars

# 4. Create first sprint
cp plan/sprints/_TEMPLATE.md plan/sprints/sprint-1.1-name.md
git checkout -b sprint/1.1-name
```

## Project Kickoff from Client Handoff

When you receive a kickoff document (PDF, brief, SOW) from sales or a client, use this prompt to have an agent flesh out the `plan/` folder:

```
Clone <GITHUB_LINK> as the project scaffold. Read the attached kickoff
document. Then work through the plan/ folder in this order:

1. DELIVERABLES.md first - extract every client-facing deliverable,
   deadline, and acceptance criterion from the handoff
2. PRODUCT_VISION.md - vision, core features, success metrics, revenue
3. techstack.md - stack decisions with rationale
4. roadmap.md - map deliverables to phases and sprints
5. Create the first sprint file from sprints/_TEMPLATE.md

Flag anything ambiguous or missing as Open Questions in DELIVERABLES.md.
Do not guess - surface unknowns.
```

**Why this order:**
- **Deliverables first** - otherwise agents skip what the client actually expects to receive.
- **Vision before roadmap** - strategy informs phasing. Skip it and agents jump to the most "actionable" thing and backfill strategy poorly.
- **Flag ambiguity** - forces open questions so missing info surfaces before sprint 1.

After the agent fills everything out, review `DELIVERABLES.md` and the open questions before greenlighting sprint 1.

## Credits

`.GCC/` is inspired by [Git Context Controller](https://github.com/faugustdev/git-context-controller) (faugustdev), based on [arxiv.org/abs/2508.00031](https://arxiv.org/abs/2508.00031) - slimmed to the two files that earn their keep in practice.

## License

MIT. See [LICENSE](LICENSE).
