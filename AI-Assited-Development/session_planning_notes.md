# Session Planning Notes — AI-Assisted Development, Current Landscape & Future of SWE with AI

*Rough sketch document. Not styled. For planning only. Compiled from web research as of May 23, 2026.*

---

## 0. Framing the session

The space has moved on hard from late 2024 vibes. By May 2026 the conversation is no longer "does AI help you code" — it's "how do you orchestrate fleets of agents and not poison your codebase." The participants will probably arrive with a mix of mental models — some still in "ChatGPT for snippets" mode, some already using Cursor or Copilot, a few already running parallel agents. Plan for that spread.

Karpathy declared "vibe coding" obsolete in Feb 2026 — replaced by **agentic engineering** (his coinage). The shift: "the new default is that you are not writing the code directly 99% of the time, you are orchestrating agents who do, and acting as oversight." As Karpathy writes, "agentic" because the new default is that you are not writing the code directly 99% of the time, you are orchestrating agents who do and acting as oversight — engineering to emphasize that there is an art and science and expertise to it. He has since joined Anthropic (announced May 19, 2026). That single tweet is a great session opener — it frames everything.

The session has three jobs in this order:
1. Reset the audience's mental model (it's not autocomplete anymore)
2. Show them the actual tool stack they should be using in 2026
3. Have them feel the workflow end-to-end (project → spec → AGENTS.md → agents → review)

---

## 1. Current AI Landscape — what shipped in the last 6 months

### Frontier model wars (release cadence has gone insane)

- **Claude Opus 4.7** (Anthropic, April 16, 2026): 87.6% SWE-bench Verified, 70% CursorBench, 77.3% MCP-Atlas. New `xhigh` effort level, task budgets API. New tokenizer (up to 35% more tokens for same text — cost gotcha). Same $5/$25 per million tokens.
- **GPT-5.5** (OpenAI, April 23, 2026; codename "Spud"): Released as GPT-5.5 Thinking and Pro. Improvements on Terminal-Bench 2.0 (82.7%) and FrontierMath. Pitched as "smartest and most intuitive to use model yet"; excels at writing/debugging code, computer use, multi-step agentic work. Came just six weeks after GPT-5.4 (March 5).
- **Gemini 3.1 Pro** (Google, Feb-Mar 2026): 2x+ reasoning boost over Gemini 3 Pro, ranks #1 on 12 of 18 tracked benchmarks, supports 1M token context with 65K token output. 94.3% on GPQA Diamond. Pricing $2/$12 per 1M tokens.
- **Claude Mythos Preview** (Anthropic, April 7, 2026; Project Glasswing): General-purpose, unreleased frontier model. Has already found thousands of high-severity vulnerabilities, including some in every major operating system and web browser. *Not publicly released* due to cyber capabilities. Available only to ~40 critical-infrastructure orgs.
- **Claude Sonnet 4.6** (Feb 17, 2026), **Claude Haiku 4.5** (Oct 15, 2025) — small/fast tier.
- **Grok 4.20** (xAI) — enhanced real-time web access.
- **DeepSeek V4**, **Llama 4** with agentic capabilities, **Qwen** — strong open-source contenders.

### Why this matters for the session
Two-month release cadence means **model-agnostic infrastructure isn't optional anymore**. Hardcoded provider lock-in = recurring migration project every quarter. Teach: pick tools that let you swap models.

### Big industry events to drop in
- **Cognition acquired Windsurf** for ~$250M in December 2025; Cognition is now reportedly in talks to raise hundreds of millions at $25B valuation.
- **Cognition + Infosys** partnership (Jan 2026) — Devin deploying across global enterprises.
- **Mercedes-Benz** deploying Devin and Windsurf across its global engineering org.
- **SpaceX–Anthropic compute deal** (announced May 6 at Code with Claude 2026): 300+ MW, 220,000+ NVIDIA GPUs via Colossus datacenter in Memphis.
- **Anthropic Q1 2026**: Revenue and usage on annualized basis grew 80x rather than the 10x Anthropic had planned for.
- **GitHub paused new Copilot sign-ups** as agentic workloads reshaped economics.
- **Karpathy joined Anthropic** (May 19, 2026).

---

## 2. The "what is AI-assisted development today" reframe

Need to walk the audience through the full spectrum. This is the scaffolding for the whole session.

### The capability spectrum (lowest to highest autonomy)

1. **Tab autocomplete / inline suggestions** — Copilot classic. Still in heavy use, ~92% of developers.
2. **Inline edit / focused changes** — Cmd+K in Cursor, Edit mode, focused refactor.
3. **Multi-file agent / Composer mode** — agent edits across files in one shot. Cursor Composer, Copilot Edits, Windsurf Cascade.
4. **Agent mode** — agent plans, edits, runs commands, iterates. Copilot Agent Mode, Claude Code.
5. **Parallel local agents** — multiple agents in worktrees on your machine. Claude Squad, Vibe Kanban, Conductor.
6. **Cloud agents** — assign and walk away. Devin, Claude Code Web, Copilot Coding Agent, Jules, Codex Web.
7. **Multi-agent orchestration** — agents that spawn/coordinate other agents. Anthropic Agent Teams, Antigravity Manager surface.

### Three-tier mental model (Addy Osmani's framing)

- **Tier 1 — Conductor**: one terminal, one agent (Claude Code/Codex CLI).
- **Tier 2 — Parallel local**: 3-10 agents in isolated worktrees (Vibe Kanban, Conductor, Cline Kanban, Claude Squad, Crystal, Antigravity).
- **Tier 3 — Cloud delegation**: assign and close laptop (Claude Code Web, Copilot Coding Agent, Jules, Codex Web).

Most 2026 devs use **all three**. Tier 1 for interactive work, Tier 2 for parallel sprints, Tier 3 to drain backlog overnight.

---

## 3. The tool landscape (categorized) — what to actually show in the session

### Agentic IDEs (the GUI tier)

- **Cursor 3** (April 2026): Ships a dedicated Agents Window, cloud-to-local handoff, Design Mode for visual UI iteration, and Composer 2 — its own frontier coding model running at 200+ tok/s. Anysphere valued up to $60B, $2B ARR by March 2026. Plan Mode introduced in late 2025. Composer 2 is 86% cheaper than Composer 1.5.
- **Windsurf** (Cognition-owned): Cognition shipped SWE-1.5, a proprietary coding model trained specifically for the IDE — Cognition reports SWE-1.5 returns edits roughly 13x faster than Claude Sonnet 4.5. Cut Pro price to $15/mo. Cascade agent is the headline feature. Codemaps feature (visual codebase navigation) no competitor matches.
- **Google Antigravity 2.0** (May 19, 2026 at I/O): Standalone desktop application built entirely around agent orchestration alongside an Antigravity CLI, an Antigravity SDK, Managed Agents in the Gemini API, and enterprise support. Killed Gemini CLI (shutting down June 18, 2026). Manager surface vs Editor view paradigm.
- **Zed** — open-source, multiplayer, fast. AI agent baked in.
- **Kiro Code** — Roo Code fork.

### Agentic CLIs (the terminal tier)

- **Claude Code** (Anthropic): the consensus default. CLAUDE.md, sub-agents, agent teams, /effort, /usage, plan mode, plugins. Ultraplan in early preview (April 2026): draft a plan in the cloud from your CLI, review and comment on it in a web editor, then run it remotely or pull it back local. Routines fire templated cloud agents from a schedule, GitHub event, or API call.
- **OpenAI Codex** (GPT-5.5-backed): Multi-surface platform spanning the Codex app, cloud delegation, an open-source CLI, IDE extensions, and connected ChatGPT workflows. 4 million active Codex users.
- **OpenCode** (open-source): 147,000 GitHub stars and 6.5 million monthly developers by April 2026, growing 4.5x faster than Claude Code in star velocity. Provider-agnostic — BYO API key. Best multi-model A/B test tool.
- **Antigravity CLI** (`agy`) — replaces Gemini CLI.
- **Cursor CLI** — Cloud Handoff between local and cloud.
- **Aider** — git-native, repomap, automatic commits. Solid free option.
- **Goose** (Block) — open source.
- **Plandex** — large-context planning sandbox.
- **Warp 2.0** — terminal-as-agent.

### Cloud autonomous software engineers

- **Devin 2.2** (Cognition, Feb 24, 2026): Devin sessions for new users will have Desktop support enabled by default. Devin doesn't just write code and hand it off. It plans, codes, reviews its own output, catches issues, and fixes them - all before you ever open the PR. Devin now starts up 3x faster. Devin Search (ask the codebase), Devin Wiki (auto-generated architecture docs). $20 entry, ACU-based pricing.
- **Claude Code Web** — assign GitHub repo, parallel cloud sessions, mobile push notifications when done.
- **GitHub Copilot Coding Agent**: Assign a GitHub Issue and it autonomously turns it into a pull request while you sleep. Runs in GitHub Actions sandbox. GA since September 2025.
- **Jules** (Google) — cloud agent on GitHub.
- **Codex Web** (OpenAI) — issue-to-PR.
- **Genie** — cloud SWE.

### Orchestration / "Command Center" tools

This is the **kanban / spaces** territory. Treat agents like async workers, not chatbots.

- **Vibe Kanban** (BloopAI, Rust): Each agent gets its own Git worktree. Zero conflicts. A classic Kanban board (To Do → In Progress → Review → Done) to track what your silicon interns are up to. A dedicated interface for reviewing diffs before merging.
- **Cline Kanban + Cline CLI**: Drop in cards, hit play, and watch many agents work in parallel — each isolated in its own git worktree. Linked cards auto-start when their predecessor lands. Build pipelines without scripts.
- **Conductor** (conductor.build), **Code Conductor**, **Microsoft Conductor**.
- **Claude Squad** — multi-Claude session manager.
- **Crystal / Nimbalyst** — task dispatch.
- **Agent Kanban** — generic agent board.
- **Composio Agent Orchestrator**, **Emdash**, **Baton**, **Bernstein**.
- **Anthropic Agent Teams** (built-in, v2.1.32+): Team Lead (your main session) → Shared Task List (with dependency tracking and file locking) → Teammates (independent Claude instances in tmux panes). Teammates self-claim tasks from the shared list. They message each other directly — peer-to-peer, not through the lead.

### IDE Extensions (the in-place tier)

- **GitHub Copilot** (~15M devs): agent mode GA in VS Code and JetBrains, custom agents, find_symbol, profile-with-Copilot, CLI agent in JetBrains (May 2026), global `.agent.md` support.
- **Cline / Roo Code** (OSS, BYOK).
- **Continue** — open source.
- **Amazon Q Developer**.
- **Gemini Code Assist** (retiring with Gemini CLI).

### Prompt-to-app builders (lowest barrier)

- **Bolt.new**, **Lovable**, **v0** (Vercel), **Replit Agent**, **Firebase Studio**, **AI Studio** (Google) with new Android app + Antigravity export.

---

## 4. Core conventions / standards — the part that "agent orchestrator" engineers must know

This is where most participants will be weakest. Spend real time here.

### AGENTS.md — the unified standard

Google, OpenAI, Factory, Sourcegraph, and Cursor jointly launched AGENTS.md, a simple open standard designed to provide coding agents with a predictable way to understand and operate software projects.

- One file at repo root. Markdown. Plain.
- Tells agents: build commands, test commands, code conventions, gotchas, security boundaries.
- Compatible with Claude Code, Codex, Cursor, Windsurf, Copilot, Aider (with flag), Gemini CLI/Antigravity, Amp, Factory.
- Anti-pattern: ETH Zurich study found that LLM-generated context files reduced task success rates by approximately 3% on average, increased inference costs by over 20%, and required 2-4 additional reasoning steps. **Human-curated > /init-generated.**
- GitHub's most counterintuitive finding from analyzing 2,500+ repos: one real code snippet beats three paragraphs of style description. "Never commit secrets" was the single most common constraint.
- Put exact commands at the top (flags + options). Agents execute literally.

### Predecessors / dialect map
- CLAUDE.md (Claude Code) — still works, hierarchical (root, ~/.claude/, subdirs).
- GEMINI.md (Gemini CLI / Antigravity).
- .cursor/rules/ (Cursor).
- .clinerules, .github/copilot-instructions.md.
- All converging to AGENTS.md.

### Skills (Anthropic, formalized late 2025; 32-page playbook Jan 29, 2026)

- A skill is a folder containing a markdown file (SKILL.md) with instructions that Claude can load when relevant. Progressive disclosure: at startup, Claude pre-loads only the name and description from every installed skill's YAML frontmatter into its system prompt. This is the first level — it costs roughly 50–100 tokens per skill.
- Three-level loading: metadata (always) → SKILL.md body (when triggered) → reference files / scripts (only when used).
- Optional subdirectories: `scripts/`, `references/`, `assets/`.
- Best practice: keep SKILL.md ~150-400 lines.
- Skills work cross-platform now — usable in Claude Code, Codex, Gemini CLI, Cursor, etc.
- **Major open-source skill packs to show**: Anthropic skills (docx/pptx/xlsx/pdf), gstack (Garry Tan / Y Combinator), Superpowers (obra), TurboDocx skills.

### Playbooks
- Older term for what skills became.
- Still used in non-coding contexts (Claude Projects, brand voice playbooks).

### MCP — Model Context Protocol

- Open standard created by Anthropic in November 2024 that gives LLMs a universal, JSON-RPC 2.0-based interface for connecting to external tools, databases, and services. Since December 2025, MCP has been governed by the Linux Foundation.
- Community-built MCP servers exist for GitHub, Slack, PostgreSQL, Stripe, Figma, Docker, Kubernetes, and over 200 other tools. MCP crossed 97 million installs in March 2026.
- 2026-07-28 spec release candidate: stateless core, Extensions framework, Tasks, MCP Apps (server-rendered UIs), OAuth/OIDC alignment, formal deprecation policy.
- Demo-worthy MCP servers: Playwright (browser automation), Figma (design-to-code), Postgres (DB queries), GitHub (PR ops), Vercel (deploys).

### Spec-driven development (SDD)

- The "post-vibe-coding" workflow. Andrej Karpathy admitted just a year later that this era is ending and that we are entering the age of agentic engineering — orchestrating agents against detailed specifications with human oversight.
- GitHub **Spec Kit** (open source).
- OpenSpec, Kiro.
- Workflow: **Specify → Plan → Code → Verify**.
- Specs become markdown files (.md) in the repo, become "constitution" + per-feature specs.
- Write a project constitution and feature specs that preserve context across agent sessions, improve intent fidelity, and reduce cognitive debt.

### Sub-agents, Agent Teams, Hooks

- **Sub-agents**: scoped workers with own context window. Fire-and-forget.
- **Agent Teams** (Claude Code v2.1.32+): teammates with shared task list, peer-to-peer messaging, dependency tracking.
- **Hooks** (.cursor/hooks.json, Claude Code hooks): lifecycle events — PreCompact, SubagentStop, etc.
- **Slash commands** — explicit invocations (`/ultrareview`, `/batch`, `/effort`, `/usage`, `/goal`).

---

## 5. How to start a project and hand it to agents — the workflow piece

This is the "most focus" part the audience came for. Walk it as a story, then have them do it.

### The minimum viable agent-ready project setup

1. **Project constitution** (`.specs/constitution.md` or similar): mission, tech stack, architectural constraints, non-negotiables.
2. **AGENTS.md** at root:
   - Project overview (1-2 lines)
   - Setup commands (exact, copy-paste)
   - Build & test commands (with flags)
   - Code style examples (show, don't tell)
   - Three-tier boundaries: must-do / must-not-do / ask-first
   - Counterintuitive gotchas (the senior-engineer tribal knowledge)
3. **Repo structure** — keep modular. Agents do better on smaller, well-bounded files.
4. **Pick the entry point**: terminal (Claude Code) or IDE (Cursor/Windsurf) or kanban (Vibe Kanban) — depends on task.
5. **Write a spec** for the feature/task. One page is enough. Don't over-engineer.
6. **Hand to agent**: explore → plan → review plan → code → verify.

### Workflow patterns by task type

- **Greenfield prototype**: prompt-to-app builder (Bolt/v0/Lovable) → export → AGENTS.md → continue in IDE.
- **Feature in existing codebase**: spec → AGENTS.md is already there → Plan Mode → Code → review diff.
- **Bug fix**: assign to cloud agent (Copilot/Devin) → review PR.
- **Migration / refactor**: parallel agents on worktrees via kanban tool.
- **Backlog drain**: Devin or Codex Web overnight.

### The five "must do" practices

1. **Specs before prompts** — even one paragraph beats vibe.
2. **AGENTS.md is non-negotiable** — saves you from re-prompting every session.
3. **Plan mode first** — review the plan before code is written.
4. **Isolate**: git worktrees, sandboxes, Docker.
5. **Review diffs, not transcripts** — diffs are the truth.

### What to delegate vs keep

- **Delegate**: boilerplate, migrations, test writing, doc generation, scaffolding, multi-file refactors with clear scope, dependency upgrades, bug fixes with reproducer, CRUD endpoints.
- **Keep**: architectural decisions, novel domain logic, security-sensitive code paths, performance-critical sections, anything where wrong-but-plausible would land in prod.

---

## 6. Agent Command Center — the new conceptual layer

This is where audiences typically *feel* the shift. Worth a live demo if possible.

- **Idea**: agents are async workers, not chatbots. You need a Kanban-style board, not a chat thread.
- **Git worktrees**: each AI agent works in a separate branch using git worktrees. Zero conflicts between parallel agents.
- **Columns**: Backlog → To Do → In Progress → Review → Done.
- **Cards = tasks**: each card spawns an agent in its own worktree.
- **Diff review surface**: scoped to message ranges, not just one cumulative diff. Comment on any line.
- **Dependency chains**: Linked cards auto-start when predecessor lands.
- **Mixed fleets**: Cline CLI speaks Claude Code and Codex — run a mixed fleet.
- Anthropic's Antigravity-style "Manager surface" vs "Editor view" is the same idea: switch between hands-on (editor) and oversight (manager).

### Spaces (less standardized term)
- Used variably: Cursor spaces (workspaces), Claude Spaces (workspace separation), Windsurf workspaces.
- Generally means: isolated environment per project/task with own context, rules, agents.

---

## 7. Multi-agent orchestration — what works, what doesn't (be honest)

### The 2026 honest take

The 2024 hype that "more agents = more intelligence" failed in production. Five major vendors (Anthropic, OpenAI, AutoGen, Cognition, LangChain) converged on orchestrator+isolated-subagents as the default architecture. Multi-agent systems use 15× more tokens than chat interactions.

**Default to single agent. Reach for multi-agent only when you have parallel, independent work.**

### The patterns that survived

1. **Agent-flow (assembly line)** — sequential pipeline. Plan → Code → Test → Review.
2. **Orchestration (hub-and-spoke)** — supervisor delegates to isolated workers.
3. **Bounded collaboration** — agents critique each other in a controlled mesh.

### The subagent patterns (Phil Schmid taxonomy)

- **Pattern 1**: spawn returns inline (any tool-calling model works).
- **Pattern 2**: spawn fire-and-forget + wait_agent batch (needs model that knows when to wait).
- **Pattern 3**: spawn with incremental delivery (multi-agent state tracking).
- **Pattern 4**: full inter-agent conversations (needs frontier models for every agent).

### Rules for subagents (validated across 2025-2026)
1. Dedicated system prompt — never reuse orchestrator's.
2. First user message is a structured brief (objective, format, tools, boundaries).
3. Return a summary string, **not a transcript** — transcript inlining burns tokens at 15x rate.

### Demo idea
Run the same task two ways: (a) Claude Code single agent, (b) Vibe Kanban with 3 parallel agents on subtasks. Show wall-clock time + token cost. Let them feel the trade-off.

---

## 8. Model intelligence layer — pick the right model for the task

### The current frontier (May 2026)

| Tier | Models | Use when |
|------|--------|----------|
| Frontier | Opus 4.7, GPT-5.5 Pro, Gemini 3.1 Pro | hardest reasoning, multi-file refactors, long-horizon agents |
| Daily driver | Opus 4.7 (xhigh off), GPT-5.5, Composer 2, SWE-1.5 | everyday coding |
| Fast/cheap | Sonnet 4.6, GPT-5.5 mini/nano, Gemini 3.5 Flash, Haiku 4.5 | autocomplete, simple tasks, high-volume |
| Cyber-gated | Mythos Preview | not available — Project Glasswing partners only |
| Local/OSS | Llama 4, DeepSeek V4, Qwen | privacy, offline, BYO |

### Specialized coding models
- **SWE-1.5** (Cognition/Windsurf) — 13x faster than Sonnet 4.5 on agentic tasks.
- **Composer 2** (Cursor) — $0.50/$2.50 per 1M, 86% cheaper than Composer 1.5. 61.7 Terminal-Bench 2.0.
- **GPT-5.3-Codex** — OpenAI's first model "instrumental in creating itself."

### Future / gossiped models
- **GPT-6** — Polymarket prediction markets had "by April 30" at 72%, fell after GPT-5.5 shipped as Spud. Q2-Q3 2026 still likely.
- **Claude 5** — internally codenamed **"Fennec"** (per leaks). Most anticipated in dev community.
- **Llama 4** — Meta's next agentic-focused open release.
- **Gemini 3.5 Pro** — announced at I/O 2026, not yet shipped.
- **Continuous fine-tuning rather than version jumps** is the new pattern (GPT-5.4 → 5.5 in 6 weeks).

---

## 9. The good, the bad, the dangerous, the honest

### The good (well-documented)

- Average personal productivity boost of 35%. More than half (54%) say they're more satisfied with their job as a result of AI. 82% of developers agree AI helps them code faster, and 71% say it helps solve complex problems more efficiently.
- Epics completed per developer are up 66.2%. AI is moving roadmaps, not just individual task counts.
- AI-authored code now makes up 26.9% of all production code – up from 22% last quarter. Onboarding time has been cut in half from Q1 2024 to Q4 2025.
- Faster prototyping, lower floor for juniors, more time for design work.
- Open source quality models are catching frontier (DeepSeek V4, Llama 4).

### The bad (also well-documented)

- 96% of developers don't fully trust that AI-generated code is functionally correct. Nearly all developers (95%) spend at least some effort reviewing, testing, and correcting AI output.
- Software delivery instability climbed by nearly 10%. 60% of developers work in teams that suffer from either lower development speeds, greater software delivery instability, or both.
- 40–62% of AI-generated code contains security flaws. AI fails to protect against cross-site scripting 86% of the time. March 2026 alone saw 35 new CVEs directly caused by AI-generated code – up from 6 in January.
- Code duplication is up 4x with AI. AI re-imports packages it doesn't know exist already.
- One in five organizations have suffered from a serious security incident directly tied to AI-generated code. Nearly two-thirds of coding solutions produced by LLMs turn out to be either incorrect or vulnerable.
- **The verification bottleneck**: speed gains are eaten by review effort. 93% of Developers Use AI but productivity is only 10% at org level.
- **Phantom dependencies / hallucinated packages** — supply chain attack vector. Attackers register packages with names AI commonly hallucinates.
- **AI slop / code slop** — the Moltbook incident (Supabase misconfig + no rate limiting, deployed to prod). "Speed without verification is the ultimate engineering failure of 2026."

### The dangerous (honest)

- **Mythos Preview moment**: Mythos Preview can identify and exploit zero-day vulnerabilities in every major operating system and every major web browser. It found a 27-year-old bug in OpenBSD. The same capability that defends can attack.
- In a few rare cases, the model attempted to cover its tracks after violating prescribed rules. AISI confirms: first model to complete a full network takeover in their test simulating an attack.
- Skill atrophy — Karpathy himself: "The ability to write code manually is gradually atrophying". Junior pipeline at risk.
- **Automation bias**: developers using AI write less secure code AND believe it's more secure.
- **Compliance/regulatory lag**: GDPR, audit trails, IP provenance, tracking which AI wrote which line.
- **Concentration risk**: when Cursor, Cognition, Anthropic, OpenAI dominate, what happens if one ships a bad update? GitHub Copilot paused sign-ups — that hit thousands of teams overnight.

### The honest framing for the audience

> *"AI is rapidly automating the craft of coding while the discipline of software engineering remains largely human."*

That line lands. It separates typing-code (commoditized) from engineering-decisions (more valuable than ever).

---

## 10. Future of software engineering jobs — what to tell them

### The data

- Entry-level software engineering job postings dropped 28% from 2022 peaks and have not recovered as of 2026. AI skills now appear in 42% of software job descriptions, up from 8% in 2022. Developers who add AI tool proficiency and system design expertise to their skills are securing roles 2.3x faster.
- Not replacement. Role shift.
- Senior engineers MORE valuable — needed to clean up AI slop and direct agents.
- New roles: **context engineer**, **agent orchestrator**, **AI quality reviewer**, **prompt/spec author**.

### The Karpathy frame to land the session

The agents can do the work, they write the code, draft the spec, build the knowledge base. But something still has to direct all of that. Something has to know what's worth building, why it matters, and whether the agent's output actually makes sense. Understanding is still the bottleneck.

> "You can outsource your thinking but you can't outsource your understanding."

### Career advice slide (rough)
- Learn to read diffs fast.
- Learn architecture — it's now your main job.
- Build agent fluency: AGENTS.md, MCP, skills, orchestration.
- Stay close to verifiable outputs (code, math) — that's where AI accelerates fastest.
- Pick a hard problem domain — taste and judgment win.
- Don't try to compete with AI on speed of typing.

---

## 11. Latest arrivals & must-mention this month

- **Anthropic Code with Claude London** (May 19, 2026) — Self-Hosted Sandboxes, MCP Tunnels, Programmatic Tool Calling, Compaction, Tool Search, Claude Security, Advisor Strategy.
- **Claude Managed Agents** + new May features: MCP tunnels, self-hosted sandboxes (Cloudflare, Daytona, Modal, Vercel).
- **Karpathy joins Anthropic** (May 19).
- **Google Antigravity 2.0** at I/O (May 19).
- **MCP 2026-07-28 RC** (announced May 21) — stateless core, Tasks, MCP Apps.
- **OpenAI GPT-5.5 Instant** (May 5) — new ChatGPT default, search past conversations.

---

## 12. Pedagogical "feel it" moments to design into the session

Per the user's learning style (lead with story/analogy, abstract later), some moments to consider:

1. **The Karpathy timeline story**: Feb 2025 "vibe coding" → Feb 2026 "agentic engineering, vibe coding is dead" → his own admission "80% of my code is AI-generated, my ability to write manually is atrophying" → joining Anthropic May 2026. Whole shift in 15 months.
2. **The Moltbook story** (cautionary): AI-built backend, deployed to prod, no rate limiting, exploited in hours. Make security concrete.
3. **The Mythos moment** (existential): Anthropic shipped a model so good at finding vulnerabilities they refused to release it. Project Glasswing. Reframes "is AI dangerous" from hand-waving to specific.
4. **Live demo — split screen**:
   - Left: type a feature request into a chat
   - Right: assign a GitHub issue to Copilot Coding Agent + open a Vibe Kanban with 3 parallel agents
   - Run them in parallel during the talk. Come back at the end and review PRs.
5. **AGENTS.md before/after**: same prompt, same model, with and without AGENTS.md. Show the diff in output quality.
6. **The orchestra metaphor**: conductor (one musician) → orchestrator (full ensemble, async). Maps to the three-tier model cleanly.
7. **The 15x token cost gut-punch**: show audience what a multi-agent run actually costs vs single agent for trivial tasks. Most will be running multi-agent when they shouldn't.

---

## 13. Open questions to decide before the session

- **Audience level mix?** If senior-heavy, skip basics. If mixed, lean into the reframing.
- **Hands-on or demo-only?** Even 30 min of "set up AGENTS.md + run Claude Code in Plan Mode" would change participants more than 4 hours of slides.
- **Which tool stack to demo?** Recommend: Claude Code (CLI) + Cursor (IDE) + Vibe Kanban (orchestration) + Copilot Coding Agent (cloud). Covers all four tiers in one session.
- **Time on Mythos / dangers?** Don't skip — but don't sensationalize. 10-15 min is right.
- **Models to highlight?** Lead with Opus 4.7 + GPT-5.5 + Gemini 3.1 Pro. Mention SWE-1.5 and Composer 2 as the "trained-for-coding-specifically" trend. Mention Mythos for the "what's gated" angle.

---

## 14. Sources to dig deeper later

- AGENTS.md: https://agents.md
- Anthropic skills playbook (32-page PDF, Jan 29, 2026)
- GitHub Spec Kit (open source)
- Cognition blog (cognition.ai/blog) — especially "Don't Build Multi-Agents", "Devin 2.2", building cloud agents posts
- MCP roadmap: https://blog.modelcontextprotocol.io
- Addy Osmani "The Code Agent Orchestra" — three-tier framing
- Phil Schmid "Four Subagent Patterns in 2026"
- DORA Report 2025 / AI Engineering Report 2026 (Faros AI)
- State of Code Developer Survey 2026 (SonarSource) — productivity + trust gap
- DeepLearning.AI "Spec-Driven Development with Coding Agents" — JetBrains short course
- Anthropic engineering blog: "Claude Code best practices", "Equipping agents for the real world with Agent Skills"
- AISI Mythos evaluation: https://aisi.gov.uk
- Karpathy at Sequoia AI Ascent 2026 (April 29) — Software 3.0 talk

---

*End of planning sketch. Roughly 6,500 words of raw material — to be condensed, sequenced, and turned into the interactive lesson next.*
