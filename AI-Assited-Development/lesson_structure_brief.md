# Interactive Lesson Structure & Implementation Brief
## Session: AI-Assisted Development, Current Landscape & Future of SWE with AI

*Planning document for the implementing agent. Hand this off along with `session_planning_notes.md` as research source-of-truth.*

---

# 0. INSTRUCTIONS TO THE IMPLEMENTING AGENT (read this first)

## You will NOT be able to build this in one pass

This lesson is too large and too richly interactive to ship in a single generation. If you try to one-shot it you will:
- Run out of context window mid-way and produce a partial file
- Make every interactive element shallow or broken
- Lose the design coherence across sections
- Skip the live simulations that are the actual point of the lesson

**Do not try.** Instead, plan and execute incrementally.

## The required incremental approach

**Phase 1 — Skeleton & design system (1 work session)**
- Single-file HTML scaffold (`<!DOCTYPE html>...`) with embedded CSS and JS — Ashan's established preference
- Build the design system: CSS variables, typography (Fraunces for headings, Space Grotesk for body, JetBrains Mono for code — matches his Week 4 brief), color palette, spacing scale
- Navigation: slide-counter, prev/next, keyboard shortcuts (arrow keys, space), section progress bar, "jump to section" menu
- Slide container with smooth transitions
- Placeholder slides (just title + section marker) for every slide listed below
- Verify navigation works end-to-end before any content
- Save as v0.1

**Phase 2 — Static content pass (one section at a time)**
- Work act-by-act (Acts 1 through 10). Do not jump around.
- For each act: write the prose, list content, callouts, citations. No interactive widgets yet.
- Commit/save after each act. Test the full deck loads and reads coherently.
- Output v0.2, v0.3, v0.4 ... one per act.

**Phase 3 — Illustrations & static SVG diagrams**
- Go back through and add inline SVG diagrams where described.
- Use the design system colors. No external image dependencies.
- Each diagram should be hand-authored SVG (no Figma exports, no PNGs).
- This is also where you embed Chart.js bar/line charts for the data slides.

**Phase 4 — Interactive elements (the hard part — one per session)**
- Each interactive widget gets its own work session. Do not batch them.
- Test each one in isolation before integrating.
- Specifically: the timeline scrubber, the AGENTS.md before/after, the capability-spectrum slider, the multi-agent token-cost simulator, the kanban demo, the model picker quiz. These are individual mini-projects.

**Phase 5 — Polish pass**
- Animation timing, transition smoothness
- Responsive layout for projector vs laptop
- Speaker notes (hidden until "n" key pressed)
- Accessibility (keyboard nav, alt text)
- Print-friendly fallback for any participant who wants the PDF

## Technical constraints

- **Single HTML file**, self-contained. No build step. Ashan deploys these via eLearning.lk / STEMLink.
- **CDN-only dependencies allowed**: Chart.js (for data), highlight.js (for code blocks). Nothing else unless you have a strong reason.
- **No frameworks** (React, Vue, etc.). Vanilla JS only. This is non-negotiable — Ashan teaches with these as reference material and participants need to read the source.
- **Embedded fonts via Google Fonts CDN**: Fraunces, Space Grotesk, JetBrains Mono.
- **Total file size budget**: aim for under 2MB. SVG illustrations should be hand-tuned, not exported.
- **Browser target**: latest Chrome, Firefox, Safari. No IE.

## Design language (match Ashan's established style)

- Editorial typography, generous whitespace
- Hierarchy through type size and weight, not boxes everywhere
- Dark mode primary (Ashan's previous decks have used a dark editorial style); offer a light-mode toggle
- One accent color used sparingly (orange/coral works against dark)
- Diagrams should feel hand-drawn-but-precise, not corporate
- Code blocks: real, copy-pasteable, syntax-highlighted

## Voice and tone (critical)

Ashan teaches by leading with the concrete example or narrative, then building abstraction on top. Definitions go LAST, not first. Every section should:
1. Open with a story, anecdote, or concrete moment
2. Show the thing (demo, diagram, code)
3. Then name and abstract it

If you find yourself writing "X is defined as..." as a slide opener — rewrite it.

## Output expectations

When you finish each phase, output:
- The current HTML file
- A short changelog explaining what got built in this phase
- A list of "decisions made" that Ashan should sanity-check
- A list of "deferred decisions" needing his input before next phase

---

# 1. SESSION ARC & TIMING

**Duration target**: 3–4 hours (matches AI Engineer 2.0 Day 1 format)
**Slide count**: ~55 slides organized into 10 acts plus interstitials
**Pace**: ~3-4 min average per slide; demo slides 8-12 min

## The 10 Acts at a glance

| Act | Title | Slides | ~Time |
|-----|-------|--------|-------|
| 1 | The Reset | 4 | 15 min |
| 2 | The Landscape (current AI) | 6 | 25 min |
| 3 | The Capability Spectrum | 5 | 20 min |
| 4 | The Tool Stack | 8 | 30 min |
| 5 | Conventions Agents Understand | 7 | 30 min |
| 6 | Starting a Project (the workflow) | 6 | 25 min |
| 7 | The Command Center | 5 | 25 min |
| 8 | Multi-Agent Orchestration | 4 | 20 min |
| 9 | Models & Future Gossip | 4 | 15 min |
| 10 | Good, Bad, Dangerous, Honest | 5 | 20 min |
| 11 | Future of SWE & Wrap-up | 3 | 15 min |

**Buffer for Q&A, hands-on, breaks**: 25-30 min built into the schedule, not slides.

---

# 2. SLIDE-BY-SLIDE STRUCTURE

Each slide entry below uses this format:

```
### SLIDE N: Title
PURPOSE: Why this slide exists in the session arc
CONTENT: What goes on the slide
ILLUSTRATION: What visual/interactive element accompanies it
RESEARCH NOTES: Specific facts/quotes from the planning notes to include
```

---

## ACT 1 — THE RESET (Slides 1-4)

The goal of Act 1 is to break participants out of "AI = autocomplete" mode. Open with a story that lands emotionally before any content.

### SLIDE 1: Title slide
**PURPOSE**: Set tone, establish that this is a 2026-current session, not generic AI hype.

**CONTENT**:
- Title: "Agentic Engineering"
- Subtitle: "AI-assisted development, the current landscape, and where software is going"
- Presenter line: Ashan Hewa, CoDev Labs
- Date and venue
- A single quote underneath: *"You can outsource your thinking but you can't outsource your understanding."* — from Karpathy's Sequoia AI Ascent 2026 talk

**ILLUSTRATION**:
- Minimalist, full-bleed background. Subtle animated SVG of dots forming a network/graph that slowly resolves. No corporate stock art.
- Or: a slow type-in animation of the title in Fraunces.

**RESEARCH NOTES**: 
- Confirm Karpathy quote citation (April 29, 2026, Sequoia AI Ascent talk with Konstantine Buhler)

---

### SLIDE 2: The 15-month story
**PURPOSE**: This is the rug-pull. Establish that the field reversed itself in 15 months. Make participants feel the velocity.

**CONTENT**:
A scrolling/animated timeline with five anchored moments:
1. **Feb 2, 2025** — Karpathy coins "vibe coding": *"There's a new kind of coding I call 'vibe coding,' where you fully give in to the vibes, embrace exponentials, and forget that the code even exists."*
2. **Mid-2025** — Vibe coding goes mainstream. Cursor, Windsurf, Bolt, Lovable explode. Everyone is "vibe coding."
3. **December 2025** — Karpathy's own workflow tips: "In November, I wrote 80% of my code manually; in December, only 20%. The ability to write code manually is gradually atrophying."
4. **Feb 10, 2026** — Karpathy declares vibe coding dead, renames it "agentic engineering": *"the new default is that you are not writing the code directly 99% of the time, you are orchestrating agents who do and acting as oversight."*
5. **May 19, 2026** — Karpathy joins Anthropic. *("Four days ago.")*

**ILLUSTRATION**:
- Horizontal interactive timeline scrubber. As participant drags, each milestone fades in with its quote.
- Or auto-advance with a "drag to explore" affordance.
- This is one of the must-build interactive elements.

**RESEARCH NOTES**: All five moments are verifiable from the planning doc sources.

---

### SLIDE 3: Reality check (audience mirror)
**PURPOSE**: Force self-reflection. Don't just tell them where the industry is — make them locate themselves.

**CONTENT**:
A self-assessment grid the audience can mentally check off:
- "I use AI for autocomplete and quick lookups" → tier 0
- "I use Cursor/Copilot/Claude Code for active editing" → tier 1
- "I write specs and let agents implement" → tier 2
- "I run multiple agents in parallel via kanban" → tier 3
- "I assign GitHub issues to cloud agents and review PRs" → tier 4

**ILLUSTRATION**:
- A staircase or escalator graphic showing the five tiers. Each step is wider/larger as you go up.
- Interactive: clicking a tier highlights that step and shows tools/practices for that tier (no detail yet — just the title).

**SPEAKER NOTE**: Pause here. Ask the room. "Hands up — who's at tier 0? Tier 1? Tier 2?" Audience calibration.

---

### SLIDE 4: What this session will and won't do
**PURPOSE**: Set expectations. Be honest.

**CONTENT**:
Two columns.
- **Will**: reset your mental model, walk the actual 2026 tool stack, show how to start a project agent-ready, give you the conventions, name the dangers honestly.
- **Won't**: turn you into an expert in 4 hours, replace hands-on practice, give you a "best tool" answer (because there isn't one).

End with: *"Pick one tool. Use it on real work for three to four weeks. Evaluate by what you actually shipped, not what the demo looked like."* — Codegen blog.

**ILLUSTRATION**: Two side-by-side cards with checks and crosses. Simple.

---

## ACT 2 — THE CURRENT LANDSCAPE (Slides 5-10)

Establish the state of the AI model wars as of May 23, 2026. Set the context for everything else.

### SLIDE 5: The model wars — five months, four frontier launches
**PURPOSE**: Show the release cadence has gone supernatural.

**CONTENT**:
Calendar grid (Dec 2025 → May 2026) marked with major releases:
- Dec 2025: Claude Opus 4.6, GPT-5.2, Gemini 3 Pro
- Feb 2026: Claude Sonnet 4.6, Gemini 3.1 Pro, GPT-5.3-Codex
- Mar 2026: GPT-5.4
- April 2026: Claude Opus 4.7, GPT-5.5, Grok 4.20
- May 2026: GPT-5.5 Instant, Antigravity 2.0, Gemini 3.5 Flash, MCP 2026-07-28 RC
- Marked separately: Claude Mythos Preview (April 7) — *not released publicly*

**ILLUSTRATION**:
- A vertical or horizontal "tape" with each release marked as a bubble. Bubble size = market impact. Color = vendor.
- Hover reveals one-line summary.

**RESEARCH NOTES**: Cross-check release dates from planning doc.

---

### SLIDE 6: The current frontier (the "Big Three" + the gated one)
**PURPOSE**: Name the models and what they're for.

**CONTENT**:
Four cards side by side:
1. **Claude Opus 4.7** — Anthropic — 87.6% SWE-bench Verified, 70% CursorBench, $5/$25 per 1M tokens, xhigh effort level, new tokenizer (35% more tokens caveat)
2. **GPT-5.5** — OpenAI — Terminal-Bench 2.0 82.7%, agentic computer use, 4M Codex users, multi-tool tasks
3. **Gemini 3.1 Pro** — Google — 94.3% GPQA Diamond, 1M token context, $2/$12 per 1M tokens, three thinking levels
4. **Claude Mythos Preview** — Anthropic — *gated*. Found thousands of zero-days. Project Glasswing only. Foreshadow Slide 49.

**ILLUSTRATION**:
- Four cards with vendor color stripe. Mini-benchmark bar chart in each card. The Mythos card is visually "behind glass" — frosted/dimmed to communicate gated access.

---

### SLIDE 7: Cadence chart
**PURPOSE**: Drive home that "model selection is now versioning hell" if you hardcode.

**CONTENT**:
Time-series line chart of model releases per quarter, 2023-Q1 2026. The curve goes exponential.

**ILLUSTRATION**:
- Chart.js line chart with three series (OpenAI, Anthropic, Google). Annotate inflection points.

Key callout: *"GPT-5.4 → 5.5 in six weeks. Build model-agnostic infrastructure or face recurring migration projects."*

**RESEARCH NOTES**: Sourced from Fortune coverage of GPT-5.5 cadence claim.

---

### SLIDE 8: Industry-level moves (the M&A and partnership beat)
**PURPOSE**: Show this isn't just models — it's industries restructuring.

**CONTENT**:
Five news bites, presented as headlines:
- **Dec 2025**: Cognition (Devin) acquires Windsurf for $250M after OpenAI's $3B bid collapsed. Google poached the founders separately.
- **Jan 2026**: Infosys + Cognition strategic collaboration. Devin deploys across global enterprise.
- **Q1 2026**: Mercedes-Benz deploys Devin + Windsurf across global engineering org.
- **April 23, 2026**: Cognition in talks to raise hundreds of millions at $25B valuation.
- **May 6, 2026**: SpaceX–Anthropic compute deal. 300+ MW, 220,000+ NVIDIA GPUs via Colossus datacenter.

**ILLUSTRATION**:
- "Newspaper clipping" style cards in a slight scatter layout. Each clipping has a date stamp.

---

### SLIDE 9: The Karpathy joins Anthropic moment
**PURPOSE**: This is the punchline of Slide 2's timeline. Make it a single, quiet slide.

**CONTENT**:
Quote on dark background:
> "Personal update: I've joined Anthropic. I think the next few years at the frontier of LLMs will be especially formative. I am very excited to join the team here and get back to R&D."
> — Andrej Karpathy, May 19, 2026

Underneath: *"The same person who coined 'vibe coding' fifteen months ago — and renamed it 'agentic engineering' three months ago — now works at the lab building Claude."*

**ILLUSTRATION**:
- No illustration. Just typography. This slide should breathe.

---

### SLIDE 10: Where we are right now (one-slide summary of Act 2)
**PURPOSE**: Compress the landscape into a sentence the audience can remember.

**CONTENT**:
- AI-authored code: 27% of production (up from 22% last quarter)
- Daily AI users: ~30% of merged code is AI-generated
- 92% of devs use AI tools in some part of their workflow
- 96% don't fully trust AI output

Big line at bottom: *"The question is no longer 'should I use AI for code?' It's 'how do I orchestrate it without breaking things?'"*

**ILLUSTRATION**:
- Four large stat cards. Each stat counts up animation on slide enter.

---

## ACT 3 — THE CAPABILITY SPECTRUM (Slides 11-15)

The conceptual scaffolding for the rest of the session.

### SLIDE 11: From autocomplete to autonomy
**PURPOSE**: Introduce the spectrum.

**CONTENT**:
Single sentence: *"There is no 'AI coding tool' anymore. There is a spectrum from autocomplete to autonomous engineering, and every tool sits somewhere on it."*

**ILLUSTRATION**:
- Empty horizontal axis: "Autonomy →"
- Animation: dots appear one at a time, each labeled with a tier.

---

### SLIDE 12: The seven-tier capability spectrum
**PURPOSE**: Give them the mental model they'll reuse for every tool decision.

**CONTENT**:
Seven labeled tiers along the autonomy axis:
1. **Tab autocomplete** — Copilot classic
2. **Inline edit** — Cmd+K in Cursor, focused changes
3. **Multi-file agent** — Cursor Composer, Copilot Edits, Windsurf Cascade
4. **Agent mode** — Claude Code, Copilot Agent Mode (plans, edits, runs, iterates)
5. **Parallel local agents** — Claude Squad, Vibe Kanban (worktree-isolated)
6. **Cloud agents** — Devin, Claude Code Web, Copilot Coding Agent, Jules, Codex Web
7. **Multi-agent orchestration** — Anthropic Agent Teams, Antigravity Manager surface

Each tier shows: what it does, example tools, when to use it.

**ILLUSTRATION**:
- **Interactive slider** along the autonomy axis. As the participant drags the slider, the corresponding tier expands to show details + a tiny example animation. This is one of the must-build interactives.

---

### SLIDE 13: The Addy Osmani three-tier framing (simpler)
**PURPOSE**: Compress seven into three for daily decisions.

**CONTENT**:
Three vertical lanes:
- **Tier 1 — Conductor**: one terminal, one agent. Interactive work.
- **Tier 2 — Parallel local**: 3–10 agents in worktrees. Parallel sprints.
- **Tier 3 — Cloud delegation**: assign and walk away. Backlog drain.

Quote underneath: *"Most developers in 2026 will use all three tiers — Tier 1 for interactive work, Tier 2 for parallel sprints, Tier 3 to drain the backlog overnight."* — Addy Osmani

**ILLUSTRATION**:
- Three columns with a representative person/agent icon and a sample task.

---

### SLIDE 14: The orchestra metaphor
**PURPOSE**: Make Tier 2/3 land emotionally. Ashan teaches by analogy — this is one.

**CONTENT**:
Two side-by-side panels:
- **Conductor**: one violin, real-time, every note watched. (Image: one player, conductor watching)
- **Orchestrator**: full ensemble, async, you set the score and trust the sections. (Image: full orchestra)

Quote: *"Six months ago, most of us worked with a single AI coding assistant in a tight synchronous loop. The codebase becomes your canvas, not a conversation thread."* — htdocs.dev / orchestrator essay.

**ILLUSTRATION**:
- Stylized SVG illustration of both panels. Hand-drawn feel.

---

### SLIDE 15: Where each big tool sits on the spectrum
**PURPOSE**: Now place actual products on the axis. Transition into Act 4.

**CONTENT**:
The capability spectrum from Slide 12, with logos placed where tools sit:
- Copilot (autocomplete + agent mode = spans tiers 1-4)
- Cursor (tiers 2-5)
- Windsurf (tiers 2-5)
- Claude Code (tiers 4-7)
- Devin (tiers 6-7)
- Vibe Kanban (tier 5)

**ILLUSTRATION**:
- The spectrum axis with tool icons placed along it. Many tools span multiple tiers — show that explicitly with bars, not points.

---

## ACT 4 — THE TOOL STACK (Slides 16-23)

This is where you go deep on actual products. Don't be neutral; be opinionated where the data supports it.

### SLIDE 16: The four tool categories
**PURPOSE**: Frame what's coming. Avoid the "10 tools you must know" listicle trap.

**CONTENT**:
Four categories with one-line definitions:
1. **Agentic IDEs** — full editor, agent built-in
2. **Agentic CLIs** — terminal-first, scriptable
3. **Cloud autonomous engineers** — assign-and-walk-away
4. **Orchestration / Command Center** — manage multiple agents
5. *Plus*: IDE extensions, prompt-to-app builders (mention but don't deep-dive)

**ILLUSTRATION**:
- 2x2 grid with quick icons for each category. Use real shapes (terminal prompt for CLI, browser window for cloud, kanban board for orchestration).

---

### SLIDE 17: Agentic IDEs — Cursor, Windsurf, Antigravity
**PURPOSE**: Compare the three main IDEs honestly. No marketing.

**CONTENT**:
Three columns, head-to-head:
- **Cursor 3** (April 2026): Composer 2 model (200+ tok/s, 86% cheaper than 1.5), Plan Mode, Agents Window, Design Mode, Background Agents, cloud-to-local handoff. $20-200/mo. Anysphere valued up to $60B. JetBrains survey: 18% adoption, tied with Claude Code.
- **Windsurf** (Cognition-owned): Cascade agent, SWE-1.5 model (13x faster than Sonnet 4.5 — Cognition's claim), Codemaps, integrated Devin coming. $15/mo Pro.
- **Google Antigravity 2.0** (I/O 2026, May 19): standalone desktop app, Manager surface vs Editor view, Gemini 3.5 Flash default, Antigravity CLI, SDK, Managed Agents API. Killed Gemini CLI (cutoff June 18, 2026).

**ILLUSTRATION**:
- Three IDE screenshot mockups (hand-drawn SVG, not real screenshots). Each highlights the IDE's signature feature.

---

### SLIDE 18: Agentic CLIs — terminal is back
**PURPOSE**: Show the terminal renaissance and the five major CLIs.

**CONTENT**:
Five cards in a row:
- **Claude Code** (Anthropic) — consensus default. CLAUDE.md, sub-agents, agent teams, /effort, plan mode, plugins, Ultraplan, Routines, mobile push.
- **OpenAI Codex** (GPT-5.5) — multi-surface platform, 4M users
- **OpenCode** (open-source) — 147K stars, 6.5M monthly devs, growing 4.5x faster than Claude Code in star velocity. Provider-agnostic.
- **Aider** — git-native, repomap, automatic commits
- **Antigravity CLI** (`agy`) — replaces Gemini CLI

**ILLUSTRATION**:
- A row of terminal-window mockups. Each terminal shows that tool's distinctive prompt/command.
- The "Gemini CLI shutdown — June 18, 2026" urgency callout below.

---

### SLIDE 19: Cloud autonomous engineers
**PURPOSE**: Introduce the "assign and walk away" tier.

**CONTENT**:
Walk through the workflow with the major players:
- **Devin 2.2** (Cognition): assigns via Slack-like interface or GitHub/Jira ticket → plans → codes → reviews own output → opens PR. Devin Search (ask codebase), Devin Wiki (auto-docs every few hours). 3x faster startup. $20 entry tier; ACU-based pricing.
- **Claude Code Web**: parallel cloud sessions, mobile notifications, auto-fix CI failures, auto-respond to PR comments
- **Copilot Coding Agent** (GitHub): assign GitHub Issue → autonomous PR, runs in GitHub Actions sandbox. GA since Sept 2025.
- **Jules** (Google), **Codex Web** (OpenAI), **Genie**

**ILLUSTRATION**:
- Sequence diagram-style flow: Developer → Issue assigned → Cloud sandbox spins up → PR appears in inbox. Animated.

---

### SLIDE 20: Orchestration / Command Center tools
**PURPOSE**: The newest category. Probably most participants haven't heard of these yet.

**CONTENT**:
- **Vibe Kanban** (BloopAI, Rust) — Kanban board for agents, git worktree per agent, diff review surface
- **Cline Kanban** + Cline CLI — speaks Claude Code and Codex, mixed fleets, dependency chains
- **Conductor** family (conductor.build, Code Conductor, Microsoft Conductor)
- **Claude Squad**, **Crystal/Nimbalyst**, **Agent Kanban**, **Bernstein**
- **Anthropic Agent Teams** (built into Claude Code v2.1.32+): Team Lead → Shared Task List → Teammates (tmux panes), peer-to-peer messaging

**ILLUSTRATION**:
- Mockup of a kanban board with several agents working in parallel. Each card shows agent status, branch name, diff line count, "review" button. Hand-drawn SVG.
- This sets up the live demo concept in Act 7.

---

### SLIDE 21: IDE extensions and prompt-to-app builders
**PURPOSE**: Briefly cover the categories you won't deep-dive.

**CONTENT**:
Two compact columns.
- **IDE extensions** (the in-place tier): GitHub Copilot (~15M devs, agent mode GA in VS Code + JetBrains), Cline / Roo Code (BYOK), Continue, Amazon Q, Gemini Code Assist (retiring).
- **Prompt-to-app builders**: Bolt.new, Lovable, v0 (Vercel), Replit Agent, Firebase Studio, AI Studio (Android app + Antigravity export, May 2026).

**ILLUSTRATION**:
- Two compact grids of logos with one-line descriptions.

---

### SLIDE 22: How to pick a stack (decision tree)
**PURPOSE**: Don't leave them with FOMO. Give a recommended path.

**CONTENT**:
A flowchart-style decision tree:
- "Are you doing focused, interactive work?" → Claude Code or Cursor
- "Do you have a backlog of well-specified tickets?" → Devin or Copilot Coding Agent
- "Do you have multiple parallel features in flight?" → Vibe Kanban or Cline Kanban
- "Are you building from a designer's spec?" → Cursor Design Mode or Lovable
- "Do you need free / open source?" → OpenCode + Aider + Gemini CLI (until June 18)

**ILLUSTRATION**:
- Interactive flowchart. Click a question, branch lights up, end node highlights recommended tool.

---

### SLIDE 23: The minimum daily-driver stack (Ashan's recommendation)
**PURPOSE**: Concrete take-home.

**CONTENT**:
Four tools covering all four tiers:
1. **Claude Code** (CLI tier) — daily driver
2. **Cursor 3** or **Windsurf** (IDE tier) — visual work
3. **Vibe Kanban** (orchestration tier) — parallel sprints
4. **Copilot Coding Agent** (cloud tier) — backlog drain

End line: *"Start with one. Add the next within 30 days. Don't try to learn all four at once."*

**ILLUSTRATION**:
- Four pillars/columns diagram with the tools.

---

## ACT 5 — CONVENTIONS AGENTS UNDERSTAND (Slides 24-30)

The under-appreciated part. Most participants will be weakest here. Spend real time.

### SLIDE 24: Why agents need conventions
**PURPOSE**: Open with the painful concrete example.

**CONTENT**:
A story panel:
> "Drop a senior developer into a Next.js codebase with Cursor's agent mode and the same pattern surfaces inside ten minutes: the agent generates class components instead of functional ones, types `var` where the codebase uses `const`, and runs `npm test` when the project uses `pnpm test`. Every fix requires another prompt. Every prompt burns another context window." — Particula.tech

End line: *"This is what conventions fix."*

**ILLUSTRATION**:
- Two-column "with vs without" comparison. Same prompt. Bad output left, good output right.

---

### SLIDE 25: AGENTS.md — the unified standard
**PURPOSE**: This is the most important slide in the session. Treat it that way.

**CONTENT**:
- One-line definition: *"A README for agents."*
- Backed by: Google, OpenAI, Factory, Sourcegraph, Cursor — jointly launched.
- Works with: Claude Code, Codex, Cursor, Windsurf, Copilot, Aider (--read flag), Gemini CLI/Antigravity, Amp, Factory, and more.
- Lives at: repo root, plain markdown.

Inline example AGENTS.md snippet (real, copy-pasteable, syntax-highlighted):
```markdown
# Project: TaskManager Web App

## Setup
- Use `pnpm install` (NOT npm, NOT yarn)
- Node 20.x required
- Copy `.env.example` to `.env.local` before first run

## Build & Test
- `pnpm dev` to run dev server
- `pnpm test -- --run` for one-shot tests (NOT `pnpm test`, which is watch mode)
- `pnpm lint --fix` before any commit

## Code style
- Functional React components only. No classes.
- Types in same file as component, not separate `.types.ts`
- Tailwind classes; no inline styles

## Boundaries
- Never commit `.env.local` or any file in `secrets/`
- Never modify migrations in `prisma/migrations/` — generate new ones
- Ask before adding a new top-level dependency
```

**ILLUSTRATION**:
- The code block. Maybe a small "compatible with" logo strip beneath it.

---

### SLIDE 26: The counterintuitive AGENTS.md research
**PURPOSE**: Don't just say "write one." Tell them what NOT to do, with citations.

**CONTENT**:
Three findings from research:
1. *"LLM-generated context files reduced task success rates by approximately 3% on average, increased inference costs by over 20%, and required 2-4 additional reasoning steps."* — ETH Zurich (Gloaguen et al., 2026, 138 repos). **Don't auto-generate. Hand-curate.**
2. *"One real code snippet beats three paragraphs of style description."* — GitHub, analyzing 2,500+ repos. **Show, don't tell.**
3. *"Never commit secrets"* was the single most common constraint across all 2,500+ analyzed repos. **Three-tier boundaries: must-do / must-not-do / ask-first.**

**ILLUSTRATION**:
- Three callout cards with the source attribution clearly visible.

---

### SLIDE 27: AGENTS.md before/after — live demo
**PURPOSE**: Show, don't tell. Make them feel the difference.

**CONTENT**:
A side-by-side, interactive demo:
- **Left**: same prompt to an agent, no AGENTS.md. Agent guesses wrong package manager, wrong style, runs wrong test command.
- **Right**: same prompt, AGENTS.md present. Agent runs the right commands first try.

**ILLUSTRATION**:
- **Interactive widget** — must-build. Two terminal panels. A "Run" button starts a simulated agent session in each. Lines stream in. The left one shows multiple corrections/retries. The right one runs cleanly. Same wall-clock time animation so they finish together for impact.

---

### SLIDE 28: Skills — Anthropic's progressive disclosure model
**PURPOSE**: Introduce Skills (and by extension the same idea in other tools' "rules", "playbooks").

**CONTENT**:
The three-level loading model:
1. **Metadata always loaded** — name + description, ~50-100 tokens per skill
2. **SKILL.md body** loaded when triggered
3. **Reference files / scripts** loaded only when used

Inline SKILL.md example (compact):
```markdown
---
name: pr-review
description: Reviews pull requests for security, style, and architectural fit. Use when reviewing PRs before merge.
---

# PR Review

Process:
1. Check for hardcoded secrets (`grep -r "sk-\|API_KEY=" .`)
2. Verify tests cover new logic
3. Check style matches existing patterns in same directory
...
```

Cross-tool note: same idea, different filenames — Cursor uses `.cursor/rules/`, Windsurf uses `.windsurf/rules/`, all converging.

**ILLUSTRATION**:
- A funnel diagram: top-wide "100 skills installed" → narrows to "1 SKILL.md body loaded" → narrows further to "specific reference file read". Token budget shown at each level.

---

### SLIDE 29: MCP — the universal connector
**PURPOSE**: This is the protocol that connects all of it. Explain via analogy first.

**CONTENT**:
- **Analogy first**: USB-C for AI. One protocol, any tool plugs into any model.
- **What it is**: open standard from Anthropic (Nov 2024), now under Linux Foundation governance (Dec 2025).
- **Scale**: 97M installs as of March 2026. 3,000+ servers. 19,700+ on mcp.so, 7,000+ on Smithery.
- **Examples**: Playwright (browser), Figma (design), Postgres (DB), GitHub (PRs), Vercel (deploys), Stripe, Slack, Docker, Kubernetes.
- **Latest**: 2026-07-28 spec RC announced May 21 — stateless core, Tasks, MCP Apps (server-rendered UIs), OAuth/OIDC alignment.

**ILLUSTRATION**:
- USB-C connector + AI cloud illustration. Several tool icons plugging into the same connector.
- Or: a hub-and-spoke diagram with model in center, tools radiating out.

---

### SLIDE 30: Spec-driven development
**PURPOSE**: Bridge from "AGENTS.md is your project memory" to "specs are your task memory."

**CONTENT**:
The workflow:
**Specify → Plan → Code → Verify**

- **Specify**: Define the user journey, goals, success metrics, desired architecture
- **Plan**: Define the implementation plan as the agent reads it
- **Code**: Hand to agent. Agent executes.
- **Verify**: Tests pass, intent matched.

Tools: GitHub **Spec Kit**, **OpenSpec**, Kiro.

Quote: *"Karpathy himself: 'we are entering the age of agentic engineering — orchestrating agents against detailed specifications with human oversight.'"*

**ILLUSTRATION**:
- Four-step cycle diagram. Maybe animated arrows showing iteration loops.

---

## ACT 6 — STARTING A PROJECT, AGENT-READY (Slides 31-36)

This is the most-focus area per Ashan's brief. Spend real time. Concrete walkthroughs.

### SLIDE 31: The five must-do practices
**PURPOSE**: Give them the checklist before the walkthrough.

**CONTENT**:
1. **Specs before prompts** — even one paragraph beats vibe.
2. **AGENTS.md is non-negotiable** — saves you from re-prompting every session.
3. **Plan mode first** — review the plan before code is written.
4. **Isolate** — git worktrees, sandboxes, Docker.
5. **Review diffs, not transcripts** — diffs are the truth.

**ILLUSTRATION**:
- Five numbered cards with simple icons. Hand-drawn.

---

### SLIDE 32: New project — 10-minute setup walkthrough
**PURPOSE**: Show the concrete steps. End-to-end.

**CONTENT**:
Numbered walkthrough with code blocks:
1. `mkdir my-project && cd my-project && git init`
2. Write `.specs/constitution.md` — 1 page. Mission, stack, constraints.
3. Write `AGENTS.md` at root — use template from Slide 25.
4. `mkdir -p .specs/features` for per-feature specs.
5. `claude` (or open Cursor) → "Read the constitution and AGENTS.md. Confirm you understand the stack."
6. Write first feature spec at `.specs/features/001-auth.md`.
7. Switch to Plan Mode. Agent reads spec, drafts plan.
8. Review plan. Edit if needed.
9. Approve → agent codes.
10. Review diff. Test. Commit.

**ILLUSTRATION**:
- Terminal-style walkthrough panel. Each step animates in. Real commands. Copy-pasteable.

---

### SLIDE 33: Existing codebase — onboarding the agent
**PURPOSE**: Different workflow. Cover it.

**CONTENT**:
- Step 1: **Run `/init` or equivalent** — but treat output as a *draft*. (Per the ETH research from Slide 26 — auto-generated AGENTS.md hurts performance.)
- Step 2: **Strip what the agent can discover**. README content, file tree — agent finds these alone.
- Step 3: **Keep only the tribal knowledge**: gotchas, non-obvious conventions, deployment quirks.
- Step 4: **Show one real snippet per convention.**
- Step 5: **Commit. Iterate.**

**ILLUSTRATION**:
- Two-column "before/after AGENTS.md content": the bloated auto-generated version (100+ lines, mostly redundant) vs the lean curated version (20 lines, all signal).

---

### SLIDE 34: What to delegate vs keep
**PURPOSE**: Give them a heuristic, not a rule.

**CONTENT**:
Two columns:
- **Delegate**: boilerplate, scaffolding, migrations, test writing, doc generation, multi-file refactors with clear scope, dependency upgrades, bug fixes with reproducer, CRUD endpoints.
- **Keep**: architectural decisions, novel domain logic, security-sensitive code paths, performance-critical sections, *anything where wrong-but-plausible would land in prod.*

Reference quote: *"AI excels at implementation. Human creativity remains irreplaceable for breakthrough innovation."* — Ox Security report

**ILLUSTRATION**:
- Two columns visually divided. Each has a stack of task cards.

---

### SLIDE 35: Workflow patterns by task type
**PURPOSE**: Concrete recipes.

**CONTENT**:
Five mini-recipes:
- **Greenfield prototype**: Bolt/v0/Lovable → export → AGENTS.md → continue in IDE
- **Feature in existing codebase**: spec → AGENTS.md exists → Plan Mode → Code → diff review
- **Bug fix**: assign to Copilot Coding Agent or Devin → review PR
- **Migration / refactor**: parallel agents on worktrees via Vibe Kanban
- **Backlog drain**: Devin or Codex Web overnight

**ILLUSTRATION**:
- Five compact cards. Each shows the task → tool → output flow as a tiny diagram.

---

### SLIDE 36: The Explore → Plan → Code → Verify loop
**PURPOSE**: This is the rhythm. Make it stick.

**CONTENT**:
A diagram showing the four-step loop with concrete actions:
- **Explore**: agent reads relevant files, gathers context (you don't pre-load)
- **Plan**: agent drafts approach; you review and edit
- **Code**: agent executes the plan
- **Verify**: tests run, lint, human review of diff

End note: *"If you skip Plan, you've gone back to vibe coding."*

**ILLUSTRATION**:
- Circular loop diagram. Animated rotation on slide enter.

---

## ACT 7 — THE COMMAND CENTER (Slides 37-41)

This is the new conceptual layer most participants will not have internalized. Spend real time. Demo if possible.

### SLIDE 37: Agents are async workers, not chatbots
**PURPOSE**: The mental model shift.

**CONTENT**:
A contrast:
- **Old**: chat thread. Sync. One agent. Your context window is the workspace.
- **New**: kanban board. Async. Many agents. The codebase is the workspace.

Quote: *"Stop treating AI agents like chatbots you talk to. Start treating them like asynchronous workers you manage."* — Vibe Kanban write-up

**ILLUSTRATION**:
- Two side-by-side workspace illustrations. Left: a chat panel. Right: a kanban board with cards in motion.

---

### SLIDE 38: Anatomy of an agent kanban
**PURPOSE**: Show what the command center actually looks like.

**CONTENT**:
A detailed mockup of a real agent kanban:
- Columns: **Backlog → To Do → In Progress → Review → Done**
- Each card: task title, branch name (auto-generated worktree), agent name, status icon, line count, "review diff" button
- Some cards in "In Progress" show a live progress bar
- Some cards in "Review" show a diff preview snippet
- Dependency lines between cards (some cards are blocked until another lands)

**ILLUSTRATION**:
- Full kanban mockup. Hand-drawn SVG. Should look real enough to be a screenshot but stylized.
- This is one of the must-build illustrations.

---

### SLIDE 39: Git worktrees — the magic underneath
**PURPOSE**: Make the technical mechanism concrete.

**CONTENT**:
A diagram showing:
- Main repo on left
- Three worktrees branching out, each with an agent icon
- Agent A on `feat/auth`, Agent B on `feat/billing`, Agent C on `refactor/db`
- Zero conflicts because each agent only touches its own worktree
- Merge happens via PR, human-reviewed

Inline command snippet:
```bash
git worktree add ../my-project-auth feat/auth
git worktree add ../my-project-billing feat/billing
# Agent A runs in ../my-project-auth
# Agent B runs in ../my-project-billing
```

**ILLUSTRATION**:
- Branch tree visualization. Three parallel worktrees fanning out from main.

---

### SLIDE 40: Live demo — running 3 agents in parallel
**PURPOSE**: This is the experiential moment. Embed a simulation.

**CONTENT**:
A simulated kanban demo (since live demo may not be possible in all venues):
- 3 tasks pre-loaded: "Add login form", "Fix billing calculator bug", "Refactor user model"
- Click "Start agents" button
- Three agent rows show streaming output (simulated, pre-recorded)
- Tasks move through To Do → In Progress → Review
- Click any task to see its diff
- At the end: 3 PRs ready in ~simulated 2 minutes (real-time accelerated)

**ILLUSTRATION**:
- **Interactive widget** — must-build. The kanban from Slide 38, but functional. Pre-scripted agent outputs that stream realistically.
- Optional: a real-time / accelerated toggle.

---

### SLIDE 41: Manager surface vs editor view (Antigravity's framing)
**PURPOSE**: Show that even single-vendor tools are converging on this idea.

**CONTENT**:
- **Editor View**: hands-on, synchronous, you write code with AI help
- **Manager Surface**: spawn, orchestrate, observe multiple agents asynchronously
- Same paradigm in Cursor (Agents Window), Claude Code (agents view), Antigravity (Manager surface).

Quote: *"You can be hands-on, you get a state-of-the-art AI-powered IDE. Or you can offload end-to-end tasks that previously required constant context switching."* — Google Antigravity blog

**ILLUSTRATION**:
- Toggle UI showing both views. Click to switch.

---

## ACT 8 — MULTI-AGENT ORCHESTRATION, HONESTLY (Slides 42-45)

The hype is over. Be honest about when multi-agent works and when it's expensive theater.

### SLIDE 42: Multi-agent is not always the answer
**PURPOSE**: Reset expectations. The 2024 hype crashed.

**CONTENT**:
The headline: *"The 2024 hype that 'more agents = more intelligence' failed in production. Five major vendors (Anthropic, OpenAI, AutoGen, Cognition, LangChain) converged on orchestrator + isolated-subagents as the default."*

The numbers:
- Multi-agent systems use **15× more tokens** than chat interactions
- Token usage explains 80% of performance variance
- Single-agent systems consistently match or outperform multi-agent on multi-hop reasoning when reasoning tokens are held constant

**ILLUSTRATION**:
- A token-cost bar chart. Single agent: 1 unit. Multi-agent: 15 units. For the same task.

---

### SLIDE 43: The patterns that survived
**PURPOSE**: When multi-agent actually works.

**CONTENT**:
Three patterns:
1. **Agent-flow (assembly line)** — sequential pipeline. Plan → Code → Test → Review.
2. **Orchestration (hub-and-spoke)** — supervisor delegates to isolated workers.
3. **Bounded collaboration** — agents critique each other in a controlled mesh.

**ILLUSTRATION**:
- Three small diagrams side by side. Each shows the topology cleanly.

---

### SLIDE 44: The subagent contract (Anthropic's "P2 prompt")
**PURPOSE**: How to actually structure a multi-agent task.

**CONTENT**:
Three rules (validated across 2025-2026 production deployments):
1. **Dedicated system prompt** — never reuse orchestrator's prompt. Subagents need role-scoped context.
2. **First user message is the structured brief** — objective, format, tools, boundaries. Free-form delegation is a documented failure mode.
3. **Return a summary string, not a transcript** — transcript inlining pollutes context and burns tokens at 15× rate.

**ILLUSTRATION**:
- Three callout cards.

---

### SLIDE 45: Decision tree — single agent or multi?
**PURPOSE**: Make it actionable.

**CONTENT**:
A simple flowchart:
- "Can the task be decomposed into independent subtasks?" — No → single agent.
- "Do you have parallel, independent work?" — No → single agent.
- "Are the subtasks worth 15× the token cost?" — No → single agent.
- Yes to all → multi-agent, orchestrator + isolated subagents pattern.

End line: *"When in doubt, single agent. Multi-agent is a tool you reach for, not a default."*

**ILLUSTRATION**:
- Flowchart with binary branches.

---

## ACT 9 — MODELS & FUTURE GOSSIP (Slides 46-49)

### SLIDE 46: Pick the right model for the task
**PURPOSE**: Practical model selection.

**CONTENT**:
A matrix:
| Task | Recommended model | Why |
|------|---|---|
| Hardest reasoning / multi-file refactor | Opus 4.7 (xhigh), GPT-5.5 Pro, Gemini 3.1 Pro | best on benchmarks, worth the cost |
| Daily coding | Opus 4.7 (xhigh off), GPT-5.5, Composer 2, SWE-1.5 | balance |
| Autocomplete, simple tasks | Sonnet 4.6, GPT-5.5 mini/nano, Gemini 3.5 Flash, Haiku 4.5 | speed + cost |
| Privacy / offline | Llama 4, DeepSeek V4, Qwen | self-hosted |

**ILLUSTRATION**:
- A 2x2 matrix: cost vs intelligence. Plot each model.

---

### SLIDE 47: Specialized coding models
**PURPOSE**: The new wave — models trained for coding, not chat.

**CONTENT**:
Three examples:
- **Composer 2** (Cursor) — $0.50/$2.50 per 1M tokens, 86% cheaper than 1.5, 200+ tok/s
- **SWE-1.5** (Cognition/Windsurf) — 13x faster than Sonnet 4.5 on agentic coding tasks (Cognition's claim)
- **GPT-5.3-Codex** — OpenAI's first model "instrumental in creating itself"

Trend line: *"Every major IDE vendor is now training their own coding model. UX wrappers around someone else's frontier model is over."*

**ILLUSTRATION**:
- Speed comparison bar chart.

---

### SLIDE 48: What's coming — the gossip slide
**PURPOSE**: Audience loves future-gossip. Give them what's credibly expected.

**CONTENT**:
- **GPT-6** — Q2-Q3 2026 likely. (Polymarket had "by April 30" at 72%, fell after GPT-5.5 shipped as "Spud".)
- **Claude 5** — internally codenamed **"Fennec"**. Most anticipated in developer community.
- **Llama 4** — Meta's next agentic-focused open release.
- **Gemini 3.5 Pro** — announced at I/O 2026, not yet shipped (only 3.5 Flash is out).
- **The pattern**: continuous fine-tuning replacing version jumps. GPT-5.4 → 5.5 in six weeks.

Caveat slide: *"This is gossip. By the time you're watching this, half of these will have shipped or been renamed."*

**ILLUSTRATION**:
- A "rumor mill" style card layout. Each card with confidence indicator (e.g., "high signal", "speculation").

---

### SLIDE 49: The Mythos moment — the gated model
**PURPOSE**: This is dramatic. Earn the drama.

**CONTENT**:
A storytelling slide:
- **April 7, 2026**: Anthropic announces **Claude Mythos Preview**.
- General-purpose frontier model. Not designed for cybersecurity.
- During testing: found a 27-year-old bug in OpenBSD. Wrote a remote code execution exploit for FreeBSD's NFS server chaining six RPC requests. Achieved full control flow hijack on ten fully patched targets.
- Previous models: zero full control flow hijacks. Mythos: ten.
- AISI evaluation: 73% success on expert-level Capture-the-Flag, first model to complete a network takeover simulation.
- Anthropic's decision: **not released publicly.** Instead, **Project Glasswing** — coordinated disclosure with ~40 critical-infrastructure organizations.
- Critics: Some say it's clever marketing. Others say it's the inflection point.

End line: *"The same capability that defends can attack. This is the watershed moment."*

**ILLUSTRATION**:
- A single image: a model card with a "DO NOT RELEASE" stamp across it. Dark, somber tone. Don't sensationalize but make it land.

---

## ACT 10 — GOOD, BAD, DANGEROUS, HONEST (Slides 50-54)

### SLIDE 50: The good — what's actually working
**PURPOSE**: Validate the productivity claims with data.

**CONTENT**:
Four stat cards (count-up animation):
- **+35%** personal productivity boost (SonarSource State of Code 2026)
- **+66%** epics completed per developer (DORA / AI Engineering Report 2026)
- **27%** of production code now AI-authored (up from 22%)
- **50%** reduction in onboarding time (Q1 2024 → Q4 2025)

Quote: *"54% of developers say they're more satisfied with their job as a result of AI."*

**ILLUSTRATION**:
- Four big stat cards with subtle animation. Source citations beneath each.

---

### SLIDE 51: The bad — the verification bottleneck
**PURPOSE**: Equal time. The dark side, with data.

**CONTENT**:
- **96%** of developers don't fully trust AI-generated code
- **95%** spend at least some effort reviewing/correcting AI output
- **+10%** software delivery instability with AI adoption
- **40–62%** of AI-generated code contains security flaws
- **86%** fail XSS protection
- **35** new CVEs in March 2026 alone, directly caused by AI-generated code (up from 6 in January)
- Code duplication **4x** higher

Quote: *"93% of developers use AI, but organizational productivity gain is only ~10%."*

**ILLUSTRATION**:
- Four stat cards in a different color (red/orange accent). Visually echoes Slide 50 to show the trade-off.

---

### SLIDE 52: The dangerous — Moltbook and AI slop
**PURPOSE**: Concrete case study. The cautionary tale.

**CONTENT**:
The Moltbook story:
- Late 2025 / early 2026 startup. AI-built backend on Supabase. Deployed to prod.
- Supabase misconfiguration exposed the data.
- No rate limiting. No identity verification. (Agent built exactly what was asked — nothing more.)
- Within hours of launch, automated scanning detected the vulnerabilities.
- Attackers exploited. Public failure.

The lesson: *"AI agents, prompted to 'build a backend that handles user requests,' build exactly that. Without explicit prompting for rate limiting, these safeguards simply don't exist."*

End line: *"Speed without verification is the ultimate engineering failure of 2026."*

**ILLUSTRATION**:
- A timeline of the incident, hour by hour. Or a "before/after" of the deployment.

---

### SLIDE 53: The automation bias trap
**PURPOSE**: The subtle danger — psychological, not technical.

**CONTENT**:
The finding:
> "Developers using AI assistance not only wrote significantly less secure code than those who worked unaided, but they also believed their insecure code was safe."

Three concrete patterns:
- **Hallucinated packages** — AI suggests packages that don't exist. Attackers register them. Supply chain compromise.
- **Phantom dependencies** — AI references libraries it can't verify are still maintained.
- **False confidence** — AI explains its code so well that reviewers stop questioning it.

**ILLUSTRATION**:
- A "mirror" illustration: developer looking at AI output, seeing reflection of their own confidence amplified back at them.

---

### SLIDE 54: The honest framing
**PURPOSE**: The one sentence to remember from Act 10.

**CONTENT**:
Big quote on dark background:
> "AI is rapidly automating the **craft of coding** while the **discipline of software engineering** remains largely human."

Underneath:
- The craft: typing, syntax, lookup, boilerplate — commoditized.
- The discipline: architecture, judgment, taste, system design, security thinking — more valuable than ever.

**ILLUSTRATION**:
- Two visually distinct halves. Left side (craft): mechanical, repetitive icons. Right side (discipline): organic, considered icons.

---

## ACT 11 — FUTURE OF SWE & WRAP-UP (Slides 55-57)

### SLIDE 55: The jobs picture, honestly
**PURPOSE**: Address the elephant in the room.

**CONTENT**:
The data:
- Entry-level postings **down 28%** from 2022 peaks
- AI skills in **42%** of software job descriptions (up from 8% in 2022)
- Developers with AI tool proficiency hired **2.3x faster**

The reframe:
- Not replacement. **Role shift.**
- Senior engineers are MORE valuable — needed to clean up AI slop and direct agents.
- New roles emerging: context engineer, agent orchestrator, AI quality reviewer, prompt/spec author.

**ILLUSTRATION**:
- A "before/after" job posting comparison. 2022 vs 2026.

---

### SLIDE 56: Career advice — what to actually do
**PURPOSE**: Concrete take-home for participants.

**CONTENT**:
Five concrete recommendations:
1. **Learn to read diffs fast.** This is your new core skill.
2. **Lean into architecture.** Type-fast is commoditized; design isn't.
3. **Build agent fluency.** AGENTS.md, MCP, skills, orchestration tools.
4. **Stay close to verifiable outputs.** Code and math are where AI accelerates fastest — be the human in that loop.
5. **Pick a hard domain.** Taste and judgment win in markets where the answer isn't obvious.

End line: *"Don't try to compete with AI on speed of typing. Compete on what it can't do."*

**ILLUSTRATION**:
- Five numbered cards with hand-drawn icons.

---

### SLIDE 57: The Karpathy frame — closing the loop
**PURPOSE**: Bookend the session. Return to where we started.

**CONTENT**:
The closing quote:
> "You can outsource your thinking but you can't outsource your understanding. The agents can do the work — they write the code, draft the spec, build the knowledge base. But something still has to direct all of that. Something has to know what's worth building, why it matters, and whether the agent's output actually makes sense.
> 
> **Understanding is still the bottleneck.**"

— Andrej Karpathy, Sequoia AI Ascent 2026

Underneath:
*"Now go build something. Slowly, with specs, in worktrees, with AGENTS.md, and review every diff."*

End screen: contact info, slide deck QR code, "questions?"

**ILLUSTRATION**:
- Echo of Slide 1. Bring the audience back to the start. Same network/graph illustration but now fully resolved.

---

# 3. ILLUSTRATION & INTERACTIVE WIDGET INVENTORY

To help the implementing agent prioritize Phase 3 and Phase 4 work:

## Must-build interactive widgets (Phase 4 — one per session)
1. **Slide 2** — Karpathy 15-month timeline scrubber
2. **Slide 12** — Seven-tier capability spectrum slider
3. **Slide 27** — AGENTS.md before/after simulated agent demo
4. **Slide 40** — Parallel kanban agent simulator (the big one)
5. **Slide 22** — Tool-picker decision tree (interactive flowchart)

## Static SVG illustrations to author (Phase 3)
- Slide 3: capability staircase
- Slide 5: release timeline tape
- Slide 6: model frontier cards with mini bar charts
- Slide 8: M&A newspaper clippings
- Slide 11: spectrum axis with dots
- Slide 14: orchestra metaphor (two panels)
- Slide 15: spectrum with tool placements
- Slide 16: four-category 2x2 grid
- Slide 17: three IDE mockups
- Slide 18: terminal mockups row
- Slide 19: cloud agent sequence diagram
- Slide 20: kanban mockup (preview of Slide 38)
- Slide 24: bad vs good agent output panel
- Slide 28: progressive disclosure funnel
- Slide 29: USB-C / MCP analogy diagram
- Slide 30: spec workflow cycle
- Slide 33: AGENTS.md before/after content
- Slide 36: Explore-Plan-Code-Verify loop
- Slide 38: full kanban anatomy (the detailed one)
- Slide 39: git worktree branching diagram
- Slide 41: editor / manager view toggle UI
- Slide 43: three multi-agent topology diagrams
- Slide 49: Mythos "do not release" stamp
- Slide 54: craft vs discipline split
- Slide 57: closing graph resolution

## Chart.js charts to embed (Phase 3)
- Slide 7: model release cadence line chart
- Slide 10: four stat cards with count-up
- Slide 42: token-cost bar chart (1x vs 15x)
- Slide 46: cost vs intelligence 2x2 plot
- Slide 47: speed comparison bar chart
- Slide 50, 51: stat card sets

---

# 4. DESIGN SYSTEM SPECIFICATION (give this to the implementing agent)

## Typography
- Headings: **Fraunces** (serif, editorial — weight 400-700)
- Body: **Space Grotesk** (sans-serif — weight 400-500)
- Code: **JetBrains Mono** (weight 400)
- Load from Google Fonts CDN

## Type scale (slide content)
- Slide title: 56px / 1.1 / weight 600 / Fraunces
- Subtitle: 28px / 1.3 / weight 400 / Space Grotesk
- Body: 20px / 1.55 / weight 400 / Space Grotesk
- Caption / source: 14px / 1.4 / weight 400 / Space Grotesk italic
- Code: 16-18px / 1.5 / JetBrains Mono

## Color tokens (dark mode primary)
- `--bg-primary`: #0a0a0b (near-black, slightly warm)
- `--bg-elevated`: #16161a
- `--bg-card`: #1c1c22
- `--text-primary`: #f5f5f0 (warm white)
- `--text-secondary`: #b0b0a8
- `--text-tertiary`: #6e6e68
- `--accent`: #ff6b3d (coral-orange — used sparingly)
- `--accent-soft`: #ff6b3d22
- `--border`: #2a2a30
- `--success`: #6bd968
- `--danger`: #ff5252

Light mode toggle: invert background/text. Keep accent.

## Spacing
- Use a base-8 scale: 8, 16, 24, 32, 48, 64, 96, 128px
- Slide padding: 64px desktop, 32px mobile
- Slides take full viewport width and height

## Slide layout
- Centered content column, max-width 1100px on large screens
- Vertical centering, but allow scroll if content overflows
- Top-right: slide counter (e.g., "12 / 57")
- Bottom: progress bar (thin, accent color)
- Bottom-left: section name (e.g., "Act 4 — The Tool Stack")
- Bottom-right: keyboard hint ("← →" / "?")

## Navigation
- Arrow keys (← →) to move between slides
- Spacebar to advance
- "?" key for help overlay (keyboard shortcuts)
- "n" key to toggle speaker notes
- "g" key to open slide jump menu
- "f" for fullscreen
- "Esc" to close overlays

## Animations
- Slide transitions: 250ms ease-out
- Element fade-in on slide enter: stagger 80ms each, 400ms duration
- Avoid bounce, avoid spin. Keep restrained and editorial.

## Code blocks
- Use highlight.js theme: a custom dark theme matching the palette
- Border-left accent stripe (3px) in accent color
- Padding: 24px
- Background: var(--bg-elevated)
- Always include language label (top-right)

---

# 5. SPEAKER NOTES SYSTEM

For Ashan's use during delivery. Implement as a hidden panel that toggles with "n" key.

Each slide should have:
- **Time budget**: e.g., "~4 min"
- **Key beat**: the one thing the audience must take from this slide
- **Audience question** (optional): a prompt to ask the room
- **Transition**: how to bridge to the next slide

The implementing agent should leave `data-speaker-notes` attributes on each slide div with this content. Render in the overlay panel when "n" is pressed.

---

# 6. CHECKLIST FOR THE IMPLEMENTING AGENT

Before starting, confirm:
- [ ] You have read both `session_planning_notes.md` AND this document end-to-end
- [ ] You understand this is a 5-phase build, not a single generation
- [ ] You have flagged any slides where the source material in the planning doc is insufficient
- [ ] You have proposed a Phase 1 deliverable (scaffold + nav + design system + placeholder slides) and a timeline
- [ ] You have asked Ashan to confirm the slide ordering and any cuts

After Phase 1, confirm with Ashan before continuing:
- Design system feels right
- Navigation is smooth
- Slide count and act structure align with venue time

After each subsequent phase, output a changelog and decisions log. Don't continue without Ashan's sign-off on major design or content choices.

---

*End of structure brief. Pair this with `session_planning_notes.md` for the content research. Begin Phase 1.*
