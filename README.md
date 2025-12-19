# OpenTiles

A self-taught programming journey to build a Piano Tiles clone, guided by a multi-agent AI tutoring system designed to prevent tutorial hell.

## What Is This?

OpenTiles is both a destination and a journey:

- **The Goal**: Build a fully functional Piano Tiles clone with a React/Node.js web platform and a Unity game implementation
- **The Method**: Learn programming from scratch using a structured AI tutoring system that emphasizes understanding over completion

This repository contains the learning infrastructure and (eventually) the code projects themselves.

## Project Structure

```
OpenTiles/
├── learning/                   # AI tutoring system
│   ├── core/                   # Core context files (~1-2K tokens)
│   │   ├── learner-profile.md  # Goals, level, preferences
│   │   └── current-focus.md    # Active objective, blockers
│   ├── progress/               # Progress tracking
│   │   ├── skills-log.md       # Skill levels with timestamps
│   │   └── milestones.md       # Phase gate checkpoints
│   ├── curriculum/             # Term planning
│   │   └── current-term.md     # Weekly plan, daily briefs
│   ├── prompts/                # Agent system prompts
│   │   ├── course-leader.md    # Monthly strategic planning
│   │   ├── term-orchestrator.md# Weekly coordination
│   │   └── session-teacher.md  # Per-session teaching
│   ├── templates/              # Handoff document templates
│   ├── sessions/               # Session handoff files
│   ├── llms.txt                # AI navigation index
│   └── learningsystem.md       # System design document
├── dev/                        # Code projects
│   ├── web/                    # React/Node platform (Phase 3-5)
│   └── unity/                  # Unity game (Phase 6)
└── CLAUDE.md                   # AI assistant instructions
```

## The Three-Agent Tutoring System

This learning system uses three specialized AI agents with markdown-based context handoffs:

### Course Leader (Monthly)
- Strategic curriculum planning and long-term oversight
- Phase gate validation before advancing
- Maintains the "north star" goal alignment

### Term Orchestrator (Weekly)
- Creates weekly learning plans
- Generates daily session briefs
- Processes session handoffs and tracks patterns

### Session Teacher (Per Session)
- Direct Socratic teaching interaction
- Guides through questions, not answers
- Enforces productive struggle

## Curriculum Phases

| Phase | Focus | Duration |
|-------|-------|----------|
| 1 | **Foundations**: HTML/CSS, JS basics, DOM, Git | 12-20 weeks |
| 2 | **JavaScript Depth**: ES6+, async/await, closures | 8-15 weeks |
| 3 | **React**: Hooks, components, API consumption | 8-20 weeks |
| 4 | **Node.js/Express**: REST APIs, databases, auth | 10-20 weeks |
| 5 | **Full-stack Integration**: Deployment, testing | 8-15 weeks |
| 6 | **Unity/C#**: Game implementation | After web complete |

**Timeline**: 18-24 months at 10-15 hours weekly

## Anti-Tutorial-Hell Principles

The system enforces rules to prevent passive learning:

1. **No complete solutions first** — Guide with questions before showing code
2. **Require attempts** — Wrong attempts are more valuable than no attempts
3. **Incremental hints** — Conceptual → Directional → Structural → Partial → Full
4. **Require explanations** — Must articulate understanding before proceeding
5. **Build constantly** — Every session ends with a coding task

## Getting Started

### Prerequisites

- Claude Desktop or access to Claude
- A code editor (VS Code recommended)
- Basic computer literacy

### Running the Agents

**Course Leader Session** (monthly):
1. Start a new Claude conversation
2. Load the Course Leader prompt from `learning/prompts/course-leader.md`
3. Include context files: `learner-profile.md`, `current-focus.md`, `milestones.md`

**Term Orchestrator Session** (weekly):
1. Start a new Claude conversation
2. Load the Term Orchestrator prompt from `learning/prompts/term-orchestrator.md`
3. Include context files: `learner-profile.md`, `current-focus.md`, `current-term.md`, `skills-log.md`

**Session Teacher Session** (each learning session):
1. Start a new Claude conversation
2. Load the Session Teacher prompt from `learning/prompts/session-teacher.md`
3. Include context files: `learner-profile.md`, `current-focus.md`, today's daily brief

### First Steps

1. Review `learning/core/learner-profile.md` and customize if needed
2. Run a Course Leader session to generate the Phase 1 curriculum
3. Follow the daily briefs and conduct Session Teacher sessions
4. Complete between-session coding tasks independently

## Key Metrics

The system tracks:

- **Skills demonstrated independently** vs. with AI help
- **Build time** vs. tutorial/learning time
- **No-AI practice hours** logged weekly
- **Tutorial-to-build ratio** (flag if > 3:1)

## Escalation Triggers

Issues escalate to Course Leader when:

- Same concept struggled with for 3+ sessions
- Confidence scores consistently below 0.5
- No independent coding in 4+ sessions
- Phase timeline significantly off track

## Philosophy

> Build OpenTiles from scratch, understanding every line of code written.
> The goal is competency, not just completion.

This system is designed for genuine skill development, not impressive output. AI assists learning—it doesn't replace it.

## License

This learning system design is available for personal use and adaptation.
