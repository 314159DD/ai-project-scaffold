# plan/ - Project Documentation Hub

**Updated:** <!-- YYYY-MM-DD -->

This folder is the **single source of truth** for the project. A dev or PM should be able to open this folder and understand what's being built, what's shipped, and what's next - without reading code.

## Where to Find Things

| Need | Read |
|------|------|
| What are we building and why? | [PRODUCT_VISION.md](PRODUCT_VISION.md) |
| What did the client agree to? | [DELIVERABLES.md](DELIVERABLES.md) |
| Current phase + what's next | [roadmap.md](roadmap.md) |
| Tech choices and rationale | [techstack.md](techstack.md) |
| How a component works | [architecture/](architecture/) |
| Why a decision was made | [decisions/](decisions/) |
| External services & APIs | [providers/](providers/) |
| Research findings | [research/](research/) |
| Sprint overview (macro) | [sprints/](sprints/) |
| Individual tickets (micro) | [tasks/](tasks/) |
| Superseded docs | [archive/](archive/) |

## Folder Structure

```
plan/
├── README.md              ← you are here
├── PRODUCT_VISION.md      # Vision, revenue, core features, success criteria
├── DELIVERABLES.md        # Client deliverables + acceptance (drop for non-client work)
├── roadmap.md             # Feature table + phase summaries
├── techstack.md           # Stack + key tech decisions
│
├── architecture/          # One doc per major component
├── decisions/             # Architectural Decision Records
├── providers/             # External services, APIs, dependencies
├── research/              # Research briefs, results, corrections
│
├── sprints/               # Macro: one file per sprint
│   ├── _TEMPLATE.md
│   └── archive/           # Completed sprint files
│
├── tasks/                 # Micro: one file per ticket (GitHub-issue style)
│   ├── _TEMPLATE.md
│   └── archive/
│
└── archive/               # Superseded docs (old specs, concept docs)
```

## sprints/ vs tasks/

- **`sprints/`** - macro. One file per sprint. Goal, context, inline task list, done-when. This is the view a PM asks about: "what's this sprint shipping?"
- **`tasks/`** - micro. GitHub-ticket-style. One file per item that earns its own page - detailed spec, investigation, open questions.

Start items inline in the sprint file. Promote to `tasks/` only when an item outgrows its bullet or needs a life beyond one sprint.

## Rules

- **One source per concept** - no duplicate tables across files. Link instead.
- **Archive, don't delete** - superseded docs go to `archive/`, not the trash.
- **Scaffold only what's used** - if you don't have research yet, leave `research/` with just the template. Empty folders are fine.
- **Keep roadmap lean** - details live in sprint files, not the roadmap.
