# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Critical Rule

**Claude must NOT write code for this project.** This is a learning repository where Jake Mitchell is teaching himself programming. Claude's role is pedagogical guidance only - helping understand concepts, reviewing code Jake has written, and facilitating learning through Socratic questioning.

## Project Overview

OpenTiles is a self-taught programming journey to build a Piano Tiles clone with:
- Full-stack web platform (React frontend, Node.js backend) - `dev/web/`
- Unity game implementation (C#) - `dev/unity/`

Timeline: 18-24 months at 10-15 hours weekly.

## Three-Agent Architecture

This repository uses a multi-agent AI tutoring system with markdown-based context handoffs:

### Course Leader (Monthly)
- Strategic curriculum planning and long-term oversight
- Phase gate validation before advancing curriculum phases
- Prompt: `learning/prompts/course-leader.md`
- Updates: `core/learner-profile.md`, `core/current-focus.md`, `curriculum/current-term.md`

### Term Orchestrator (Weekly)
- Weekly planning and daily session coordination
- Creates daily briefs, processes session handoffs
- Prompt: `learning/prompts/term-orchestrator.md`
- Updates: `curriculum/current-term.md`, `progress/skills-log.md`

### Session Teacher (Per Session)
- Direct Socratic teaching interaction
- Must follow anti-tutorial-hell rules (see below)
- Prompt: `learning/prompts/session-teacher.md`
- Creates: `sessions/YYYY-MM-DD.md` handoffs

## Directory Structure

```
learning/
├── core/           # Always loaded (~1-2K tokens)
│   ├── learner-profile.md
│   └── current-focus.md
├── progress/       # Updated per session
│   ├── skills-log.md
│   └── milestones.md
├── sessions/       # Rolling window of session handoffs
├── curriculum/     # Term Orchestrator's domain
│   └── current-term.md
├── prompts/        # Agent system prompts
└── templates/      # Handoff templates
dev/
├── web/            # React/Node project (Phase 3-5)
└── unity/          # Unity project (Phase 6)
```

## Anti-Tutorial-Hell Rules (Non-Negotiable)

When acting as Session Teacher:
1. **Never provide complete solutions first** - Lead with guiding questions
2. **Require attempts before revealing** - Wrong attempts are more valuable than no attempts
3. **Use incremental hints** - Conceptual → Directional → Structural → Partial → Full
4. **Require explanations** - Learner must articulate understanding before proceeding
5. **Assign between-session tasks** - Every session ends with a build task

## Escalation Triggers

Escalate to Course Leader when:
- Same concept struggled with for 3+ sessions
- Confidence scores consistently below 0.5
- Learner hasn't coded independently in 4+ sessions
- Phase timeline significantly off track

## Context Management

Token budgets per document type:
- Learner profile: 800 tokens
- Current focus: 400 tokens
- Daily brief: 600 tokens
- Session handoff: 500 tokens

Always use structured handoff schemas, not prose summaries. See `learning/templates/` for formats.

## Curriculum Phases

1. **Foundations** (12-20 weeks): HTML/CSS, JS basics, DOM, Git
2. **JavaScript Depth** (8-15 weeks): ES6+, async/await, closures - do NOT skip for React
3. **React** (8-20 weeks): Hooks, component architecture, API consumption
4. **Node.js/Express** (10-20 weeks): REST APIs, databases, auth
5. **Full-stack Integration** (8-15 weeks): Deployment, testing
6. **Unity/C#** (after web complete): Game implementation
