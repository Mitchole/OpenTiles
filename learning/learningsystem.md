# Designing a multi-agent AI learning system for self-taught programming

A three-agent architecture using Claude with markdown-based context handoffs is viable and well-aligned with emerging best practices—but success depends critically on **structured state management**, **progressive context compression**, and **protecting against AI-dependency while learning**. The proposed Course Leader → Term Orchestrator → Session Teacher hierarchy maps well to proven patterns from both AI agent frameworks (LangChain, OpenAI Agents SDK) and human organizational handoffs (medical I-PASS protocol). With 10-15 hours weekly, expect **18-24 months** to full-stack competency.

## Context management determines multi-agent system success

Production multi-agent systems share a critical insight: **never pass raw conversation history between agents**. Research from LangChain's benchmarking shows that "clutter in the context can have outsized impacts on agent reliability"—even minor additions of irrelevant prior reasoning degrades downstream performance.

The dominant pattern across LangGraph, LlamaIndex AgentWorkflow, and Google ADK is **structured state objects** with selective exposure. Rather than passing full transcripts, agents write specific outputs to designated keys (like `current_focus`, `skill_progress`, `blockers`) that subsequent agents can read. This mirrors the OpenTiles architecture's markdown file approach but requires careful attention to what goes where.

**Token budget recommendations** from production systems:

| Context Tier | Target Size | Purpose |
|--------------|-------------|---------|
| Core context (always included) | 1-2K tokens | Learner profile, active goals, key preferences |
| Working context (per session) | 4-8K tokens | Recent progress, current blockers, session notes |
| Summary prompt | 500-1,500 tokens | Compressed briefing for each agent handoff |
| Full archive | Unlimited | Searchable via retrieval, not loaded directly |

The **"lost in the middle" effect** (Stanford research) means LLMs perform poorly when relevant information sits in the middle of long contexts. Structure documents so critical facts appear at the beginning or end. Claude's auto-compact triggers at **95% context utilization**—designing documents well under that threshold prevents forced lossy summarization.

## AI tutoring works, but cognitive offloading is the enemy

A 2025 meta-analysis of 51 studies found ChatGPT interventions produce **large positive effects on learning performance (g = 0.867)**. However, this masks a critical distinction: perceived learning often exceeds actual learning. A controlled study on LLM-driven tutors found most sessions received positive satisfaction scores while actual accuracy improvements remained "marginally significant."

The core tension is **cognitive offloading**. AI reduces extraneous cognitive load (syntax recall, boilerplate), freeing working memory—this is genuinely helpful. But it can simultaneously eliminate **germane load** (productive struggle that builds lasting schema). A Microsoft/Carnegie Mellon study found developers who leaned heavily on AI tools engaged in less critical thinking, making it harder to summon those skills when needed.

**Evidence-based mitigations the system should enforce:**

- **Socratic prompting over direct answers**: Session Teacher should ask guiding questions first, not provide solutions immediately. Research on "SocraticLLM" shows structured questioning improves pedagogical quality.
- **Incremental hints**: Subtle clues → partial code snippets → full solutions, only after multiple attempts. Georgia State/MIT research validated this five-level approach.
- **Mandatory "no-AI sessions"**: Reserve 2-3 hours weekly for manual coding—reading errors fully, using actual documentation. This prevents the "skill atrophy" practitioners widely report.
- **Pre-attempt requirement**: The learner should spend 15-30 minutes investigating problems independently before consulting AI. Research by Akgun and Toker found pretesting before AI use significantly improved retention.

The system should track which skills the learner frequently delegates to AI—these are **knowledge gaps to address**, not validate.

## Documentation architecture must prevent context bloat

The **MemGPT-inspired memory hierarchy** provides the clearest model for long-running learning contexts:

```
/opentiles-learning/
├── core/                          # Always in prompt (~1-2K tokens)
│   ├── learner-profile.md         # Goals, level, preferences, constraints
│   └── current-focus.md           # Active objective, immediate blockers
├── progress/                      # Updated per session
│   ├── skills-log.md              # Skill levels with timestamps
│   └── milestones.md              # Completed achievements
├── sessions/                      # Rolling window (last 5-10 sessions)
│   └── YYYY-MM-DD.md              # Individual session notes
├── curriculum/                    # Term Orchestrator's domain
│   ├── current-term.md            # Weekly plan, daily briefs
│   └── term-history/              # Archived term summaries
├── llms.txt                       # Navigation index for all agents
└── archives/                      # Compressed older content
```

The **llms.txt standard** (emerging convention from Jeremy Howard) provides an excellent navigation pattern—a machine-readable index file that tells agents what context files exist and when to load them. This prevents agents from needing the full archive in every prompt.

**YAML frontmatter** should encode structured metadata that's easily parseable:

```yaml
---
type: session-brief
date: 2025-12-19
term: 3
week: 2
day: thursday
learner_state: progressing
current_module: react-state-management
blockers: ["useState async behavior confusion"]
confidence: 0.7
token_count: 847
---
```

**Progressive summarization** (Tiago Forte's method) applies directly: maintain five compression layers where Layer 0 is raw notes, and Layer 4 is executive summary. Older content automatically compresses—sessions from 30+ days ago become single-paragraph summaries; sessions from 90+ days ago become single-line milestones.

## Curriculum should span 18-24 months with deliberate phase gates

Analysis of freeCodeCamp, The Odin Project, and bootcamp curricula reveals strong consensus on skill progression for self-taught full-stack development:

**Phase 1: Foundations (12-20 weeks)**
HTML/CSS fundamentals, JavaScript basics, DOM manipulation, Git/command line

**Phase 2: JavaScript depth (8-15 weeks)**  
ES6+ features, async/await, closures, error handling—**do not skip this for React**

**Phase 3: React (8-20 weeks)**
JSX, hooks (useState, useEffect), component architecture, React Router, API consumption

**Phase 4: Node.js/Express (10-20 weeks)**
Server creation, RESTful API design, database basics (SQL concepts, then MongoDB), authentication

**Phase 5: Full-stack integration (8-15 weeks)**
Connecting front-end to back-end, deployment, testing fundamentals

For the **OpenTiles Piano Tiles clone**, a realistic timeline at 10-15 hours weekly:

| Months | Focus | OpenTiles Progress |
|--------|-------|-------------------|
| 1-6 | Foundations through basic React | Core web skills building |
| 7-9 | React projects, patterns | Simple Piano Tiles UI prototype |
| 10-12 | Node.js backend fundamentals | Track editor backend scaffolding |
| 13-15 | Full-stack integration | Functioning web platform |
| 16-21 | C#/Unity (separate track) | Game implementation |

**Unity requires C#**, a different language from JavaScript. However, programming fundamentals transfer well—estimate 3-6 additional months for basic Unity competency after web foundation is solid. **Sequence web platform first**, then Unity.

## Tutorial hell is the primary failure mode to design against

The single most cited sticking point in self-taught programming is **tutorial hell**: "a state of being stuck in a cycle of constantly consuming tutorials without being able to apply knowledge in the real world." Tutorials handle debugging, problem-solving, and decision-making for learners—students never develop independent skills.

The three-agent system should explicitly counter this through **Session Teacher design**:

1. **Never provide complete solutions first**—always guide through questions
2. **Require learner to attempt before revealing**—even a wrong attempt is better than passive reception
3. **Track tutorial-to-build ratio**—flag if learner hasn't independently coded in >3 sessions
4. **Assign micro-builds constantly**—"before next session, modify this component to add X feature"

Other documented sticking points the curriculum should account for:

- **JavaScript fundamentals gaps**: Learners rush to React without understanding closures, promises, `this`. Build in explicit JavaScript-only milestones before framework introduction.
- **Blank editor paralysis**: Start projects with pseudocode planning. Session Teacher should walk through problem decomposition before any coding.
- **Learning plateaus**: Research shows progress follows S-curves with intervals of no visible improvement. Term Orchestrator should vary modalities when progress stalls (switch from building to reading, or pair programming simulation).

## Handoff protocols must use structured schemas, not free-form summaries

The "telephone game" effect—information degradation across handoff chains—is well-documented in both human organizations and LLM systems. Research on LLMs playing telephone games found they exhibit "cultural attractors" (biases that amplify across iterations), causing systematic drift from original meaning.

**Prevention requires structured handoff schemas** rather than prose summaries. Adapting the medical I-PASS protocol:

```markdown
## Session Handoff to Term Orchestrator

**Illness Severity (Priority)**: routine | attention-needed | escalate
**Patient Summary (Learner State)**: 
- Completed: [specific objectives achieved]
- Demonstrated: [skills shown]
- Struggled with: [specific concepts]
**Action List (Pending)**:
- [ ] Outstanding task 1
- [ ] Practice assignment given
**Situation Awareness (Risks)**:
- Potential blocker: [identified risk]
- Misconception detected: [if any]
**Synthesis (Confidence)**: 0.8 - learner on track for weekly goal
```

**Essential information for each handoff type:**

| Handoff | Must Include | Can Omit |
|---------|--------------|----------|
| Session → Term | Session outcome, blockers hit, skills demonstrated, next session prep needs | Verbose explanations, debugging transcripts |
| Term → Course Leader | Week summary, milestone progress, trend assessment, curriculum adjustment needs | Daily details, specific code examples |
| Course Leader → Term | Updated goals, curriculum modifications, term objectives | Historical context already documented |
| Term → Session | Daily brief, specific learning objectives, context needed, suggested approach | Prior term history, archived sessions |

**Escalation triggers** (when Session Teacher or Term Orchestrator should escalate to higher agent):

- **Repeated failure**: 3+ sessions struggling with same concept without progress
- **Confidence degradation**: Agent confidence score falls below 0.4
- **Scope confusion**: Task requirements unclear or conflicting with stated goals
- **Curriculum mismatch**: Learner demonstrating mastery beyond current placement, or severe struggle indicating prerequisite gaps
- **Time-based**: Monthly check-in regardless of progress (Course Leader cadence)

## Recommended cadence aligns with learning research

Based on synthesis of AI agent patterns and self-directed learning research:

**Course Leader**: Monthly + triggered escalations
- Conducts comprehensive progress review
- Adjusts multi-month curriculum arc
- Receives: Term summaries (4-5 per check-in)
- Produces: Updated learner profile, next term objectives, curriculum modifications

**Term Orchestrator**: Weekly planning + daily brief generation
- Creates weekly learning plan each Sunday
- Generates daily session briefs (pre-populated for each session)
- Receives: Session handoffs after each session
- Produces: Daily briefs, weekly summary, escalation flags

**Session Teacher**: Each learning session (2-4 hours)
- Conducts actual teaching interaction
- Receives: Daily brief + core context (~2-3K tokens total)
- Produces: Session handoff document

**Document size constraints based on research:**

| Document | Max Tokens | Update Frequency |
|----------|------------|------------------|
| Learner profile | 800 | Monthly (Course Leader) |
| Current focus | 400 | Weekly (Term Orchestrator) |
| Daily brief | 600 | Per session (Term Orchestrator) |
| Session handoff | 500 | Per session (Session Teacher) |
| Weekly summary | 800 | Weekly (Term Orchestrator) |
| Term summary | 1,000 | Per term (Term Orchestrator) |

## Alternative architectures to consider

**1. Collapsed two-agent model**: Merge Course Leader and Term Orchestrator into a single "Curriculum Manager" role. Simpler handoffs, but loses separation between strategic (monthly) and tactical (weekly) planning. Consider this if three-agent coordination proves too complex initially.

**2. Session continuity model**: Rather than fresh Session Teacher instances, maintain rolling session context within a single conversation for 3-5 sessions, then compress and start fresh. OpenAI Agents SDK does this naturally with conversation history nesting. Reduces handoff overhead at cost of eventual context bloat.

**3. Human-in-the-loop checkpoints**: Add explicit human review points rather than relying solely on AI escalation detection. Weekly self-assessment prompts the learner completes, feeding into Term Orchestrator. Catches issues AI might miss.

**4. Retrieval-augmented approach**: Instead of passing context via markdown files, use vector embeddings of all learning history with RAG retrieval into each session. More scalable for very long learning journeys, but adds infrastructure complexity. Tools like LlamaIndex support this natively.

**5. Dual-track parallel agents**: Run two Session Teachers with different pedagogical styles (one more Socratic, one more direct), let learner choose which is helping more. Research shows learner preference for feedback style varies significantly.

## Critical failure modes the system must address

**1. AI dependency spiral**: The system itself could accelerate skill atrophy. Mitigation: Enforce "productive struggle" periods, track AI-delegation patterns, require independent attempts before AI assistance.

**2. Context document bloat**: Without aggressive pruning, markdown files grow unbounded. Mitigation: Hard token limits per document type, automatic summarization triggers at 80% capacity, time-based archival policies.

**3. Handoff information loss**: Summaries lose nuance; receiving agents miss critical context. Mitigation: Structured schemas over prose, preserve original sources in archives, bidirectional verification where receiving agent confirms key facts.

**4. Curriculum drift**: Without strong anchoring, incremental adjustments could drift far from original goals. Mitigation: Course Leader maintains immutable "north star" goal definition; monthly reviews compare against original objectives.

**5. Learner disengagement detection failure**: AI may not recognize when learner is going through motions without genuine learning. Mitigation: Periodic "no-AI" assessments where learner must demonstrate skills independently; require explanations of code in learner's own words.

**6. Tutorial hell enablement**: Session Teacher could inadvertently provide too much help, recreating tutorial dynamics. Mitigation: Explicit prompting rules requiring questions before answers, incremental hints, attempt-first requirements.

## Synthesis: What will make this system work

The three-agent architecture is sound, but implementation details will determine success:

1. **Structured over prose**: Use typed schemas for all handoffs, not narrative summaries
2. **Small context, frequently refreshed**: Keep documents under token limits, update often
3. **Protect the struggle**: The hardest design challenge is helping without over-helping; build friction intentionally
4. **Build constantly**: Every session should produce code the learner wrote, not just consumed
5. **Reset to source**: Periodically reload from authoritative documents (learner profile, original goals) to prevent drift
6. **Track the right metrics**: Not "sessions completed" but "concepts demonstrated independently"

The 18-24 month timeline for the OpenTiles project is realistic. The multi-agent system provides structure that self-directed learning often lacks—but the agents must be designed as **facilitators of learning**, not providers of answers.