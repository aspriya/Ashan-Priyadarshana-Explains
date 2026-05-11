# Day 1 Research & Reasoning Report

**Course:** AI Engineer 2.0 — Enterprise AI Development sub-track
**Session:** Day 1 (4 hours, 7 PM – 11 PM)
**Audience:** Working developers and engineering leads in Sri Lankan tech orgs, paying 13,000 LKR/session
**Author of this report:** research/reasoning pass before lesson material is built

---

## How to read this report

I'm giving you the research, plus the *reasoning* on top of it, plus the *decisions I'd recommend you make before we build the interactive lesson*. Some of this pushes back on the ordering you originally proposed — flagging that explicitly so you can decide.

The report is organized as:
1. The big calls (framing, hook, ordering) — read these first
2. The five content blocks with everything I'd put in each
3. Open questions for you before we move to building

---

# Part 1 — The big calls

## 1.1 The narrative spine

Three candidate spines were on the table. The one I'm recommending: **"AI tools as a new spectrum of teammates."**

Not "tools" as in inert software. Tools as a *team you assemble*. An IDE assistant is a pair-programmer at your shoulder. A terminal agent is a senior who works in a tmux pane. A cloud agent like Devin is a colleague in another building who works overnight and DMs you a PR in the morning. A code reviewer agent is the principal engineer who scrubs every PR. An MCP server is the company directory and key card system that lets these teammates reach things.

Why this spine wins:
- It's a metaphor, not a definition. You said you want experiential framings — this one is experiential through and through.
- It lets you talk about *autonomy levels* without using the word "autonomy" until you need to.
- It primes Day 2 without spoiling it. Day 2's "unlimited junior devs" reveal works *because* on Day 1 we set up "different kinds of teammates" — Day 2 then says: one of those teammates is so cheap and parallelizable that you should mentally treat it like an unlimited supply.

What this spine quietly does that the others don't: it shifts the audience from "which tool should I buy" (a procurement question) to "how do I work with this kind of teammate" (an engineering management question). That's the actual skill jump these sessions exist to teach.

## 1.2 The hook (first 10 minutes)

Recommended hook — open with **a paradox the audience can immediately feel**:

> In July 2025, a nonprofit called METR ran the gold-standard study on AI coding productivity. Sixteen experienced open-source developers, 246 real tasks in their own repos, random assignment, Cursor Pro with Claude Sonnet. Before the study, the developers predicted AI would make them 24% faster. After, they reported feeling about 20% faster.
> 
> The actual measured result: **AI made them 19% slower.** And they didn't notice.
>
> [pause]
>
> Now hold that. Because in the same year, Cognizant's CEO said 30% of their code is already AI-generated and they're targeting 50%. Infosys deployed Devin across financial services and reported doubling developer productivity. So which is it?
>
> The answer to that paradox is what these four hours are about. The tools work — but only when you understand *what kind of teammate you're working with*, *where each one belongs in your day*, and *how to actually talk to them*.

This opener does three things at once: it earns trust (you're citing real numbers, including ones that undercut the hype), it creates curiosity, and it teaches the audience that this won't be a vendor sales pitch.

Alternative hooks I considered and rejected:
- *Karpathy CLAUDE.md / 100k stars story.* Tempting because it's recent and viral, but it lands flatter on a Sri Lankan audience that may not know Karpathy's voice deeply. Save it for the markdown-files section where it becomes a perfect anchor.
- *Live Devin demo.* Wastes the strongest cliffhanger you have — save Devin for the SDLC section and Day 2.
- *Cognition's "if you can do it in 3 hours, Devin can probably do it."* Same — pay this off in the SDLC section.

## 1.3 The session ordering (and why I'm pushing back on yours)

Your proposed order was:

1. Tools landscape
2. Best practices
3. Special markdown files
4. SDLC mapping
5. MCP

I want to flag a risk with this order and propose an alternative.

**The risk:** opening with a tools landscape means the audience hears 20+ product names — Cursor, Windsurf, Zed, Claude Code, Codex CLI, Gemini CLI, Antigravity, Devin, Jules, Cline, Aider, Augment, CodeRabbit, Qodo, Greptile, Bugbot, Continue, JetBrains AI, Copilot, Tabnine, Amazon Q, Kiro… — without a mental shelf to put them on. By minute 45 they'll have tool-fatigue and the rest of the session has to fight that.

**The alternative I'd recommend:**

1. **Hook + framing** (15 min) — METR paradox, "teammates" metaphor, what's actually changed in the last 18 months
2. **The SDLC map** (35 min) — *first*, as the scaffolding. Where in the work you already do is AI showing up?
3. **The tools landscape** (60 min) — *now* each tool name lands on a mental shelf already built in the audience's head
4. **Break** (15 min)
5. **MCP** (40 min) — the connective tissue. Why each of those tools can reach beyond its own walls.
6. **Special markdown files** (45 min) — how you actually feed and configure these tools. The Karpathy story belongs here.
7. **Best practices** (25 min) — the meta-layer that ties it all together. Best practices land best last, because the audience has seen the failure modes the practices exist to prevent.
8. **Cliffhanger to Day 2** (5 min)

Total: 240 min = 4 hours, with one 15-min break.

Why best practices go last: a "best practices" slide presented before the audience has felt the pain it prevents lands as abstract rules. Presented after, it lands as relief — "oh, *that's* how I avoid the thing I just saw go wrong."

Why MCP goes before markdown files: MCP is about *what the agent can reach* (external systems, tools, data). Markdown files are about *what the agent knows* (project context, conventions, rules). Reach before knowledge feels right pedagogically — you have to understand the agent has hands and eyes outside the codebase before you understand why telling it about the codebase matters.

You're welcome to keep your original order if you disagree — but I'd at least move SDLC up to position 2.

## 1.4 What's earned vs. covered at high speed

You said you can speed up sections based on audience. Here's where I'd flex:

- **Audience knows Cursor/Copilot already, never touched a cloud agent:** speed through the IDE row of the taxonomy, slow down dramatically on cloud agents and MCP. This is most likely.
- **Audience is mostly senior architects:** speed through the tools landscape entirely (one slide overview, name the categories), spend more time on SDLC implications and the enterprise governance angle.
- **Audience is mostly hands-on builders, low Devin awareness:** spend more on the cloud-agent end of the spectrum, less on IDE tool comparisons.

---

# Part 2 — Content blocks

## 2.1 Block: The SDLC map (35 min)

### The model

Use a modern loop, not waterfall. The classic six phases — plan, design, code, test, deploy, maintain — still work as labels, but draw them as a loop with a feedback arrow from "maintain → plan" rather than a straight line. This matters because the *interesting* AI capability is that agents now close that loop themselves: a Sentry alert (maintain) becomes a Linear ticket (plan) becomes a Devin task becomes a PR (code) — all without a human in between.

Concretely, I'd use seven stations on the loop:

1. **Discover / Plan** — turning fuzzy ideas into specs and tickets
2. **Design** — architecture, API contracts, data models
3. **Implement** — writing the code
4. **Review** — PR feedback, security checks, style
5. **Test** — unit, integration, E2E, regression
6. **Ship** — CI/CD, deploy, rollback
7. **Observe / Operate** — monitoring, incident response, debugging in prod

### The "money slide"

A grid: stations on the x-axis, tool categories on the y-axis. Each cell either filled or empty. The visual point you want to land:

- **IDE-bound tools** (Cursor, Copilot, Windsurf, Zed): mostly fill Implement, partial coverage of Design and Review.
- **Terminal agents** (Claude Code, Codex CLI, Gemini CLI): cover Implement, Review, Test, partial Ship.
- **Dedicated reviewers** (CodeRabbit, Qodo, Greptile, Bugbot): one tall column under Review.
- **Cloud autonomous engineers** (Devin, Jules, Codex Cloud, GitHub Coding Agent): a **horizontal bar across all seven stations**.

That last row is the visual reveal. While most tools are dots in one column, Devin-class agents draw a line across the whole loop. The audience should *see* the difference before you explain it.

### What to say at this slide (script-style)

> "Look at the tools you already use. Copilot, Cursor — they sit here, in Implement. Maybe a bit of Design when you ask for an API sketch. That's it. That's why they feel like an upgraded autocomplete: they upgrade one station.
>
> Now look at the bottom row. Devin doesn't sit in one station. Devin reads the Linear ticket — Plan. Devin reads your codebase and writes a plan — Design. Devin writes the code — Implement. Devin opens a PR and responds to review comments — Review. Devin runs the tests — Test. Devin can babysit the deploy — Ship. And it can read the Sentry trace from production — Observe.
>
> This isn't a 'better Copilot.' This is a fundamentally different kind of teammate. We'll come back to this row in detail."

That last sentence is your bridge to Block 2.

### Source data for stat points you might want

- Cognizant: 30% of code AI-generated, targeting 50% (CEO Ravi Kumar S., Jan 2026, partnership with Cognition).
- Visma case study with Devin: ~2x developer productivity, ~50% project cost reduction on modernization.
- Infosys deployed Devin across financial services (Jan 2026 partnership announcement).
- Qodo report: AI code review usage lifted quality improvements from 55% to 81%.
- Atlassian Rovo Dev: 38.7% of AI agent review comments lead to additional code fixes.

---

## 2.2 Block: The tools landscape (60 min)

### Taxonomy (the one I'd use)

Five categories, not seven. Three is too few, more than five overwhelms.

**Category 1 — IDE-native AI assistants and AI-first IDEs**
The thing you open to write code. The agent lives in the editor.

- **Cursor** — VS Code fork, dominant. Cursor 2.0 (Oct 2025) brought their own model (Composer, 4x faster), up to 8 parallel agents in worktrees, native browser tool for self-testing. Cursor 3.x (May 2026) added native PR review experience and parallel plan execution. $20/mo Pro, $40/mo Business. Roughly 14 million MAUs, 18% share. Cursor SDK lets teams ship custom agents from CI/CD.
- **Windsurf** — Now owned by Cognition (acquired from Codeium). Cascade agent. Tighter coupling with Devin coming. $15/mo, often called best price-to-capability ratio in the agentic-IDE row.
- **GitHub Copilot** — Still the volume leader. ~28 million MAUs, 37% share. $10/mo (cheapest serious tool). Added Agent Mode, Spaces, PR review. Strongest where teams are already deep in GitHub Enterprise.
- **Zed** — Rust-native, sub-50ms latency. AI features are functional but not the deepest. Best paired with Claude Code running in a side panel rather than as a primary agent IDE.
- **JetBrains AI Assistant + Junie** — JetBrains' answer. Junie is their agent. Strong for the IntelliJ/PyCharm/Rider crowd that won't leave their IDE.
- **Google Antigravity** — Launched November 2025 alongside Gemini 3. *Built agent-first*, not VS Code fork. Multi-agent orchestration with a built-in Chromium browser. Mission Control view. Free during preview. Worth showing on a slide as "what an agent-first IDE looks like."
- **Kiro (AWS)** — AWS-native, spec-driven, uses EARS syntax. Niche but technically interesting.

**Category 2 — Terminal / CLI agents**
You stay in the terminal. The agent is a CLI tool.

- **Claude Code** — Anthropic. Currently the highest-quality terminal coder for hard problems (SWE-bench Verified ~80.8%, ~67% blind-eval win rate). Agent Teams (Feb 2026) brought multi-agent. Skills, hooks, subagents, MCP — the deepest extensibility harness in the category. $20/mo Pro, $100 Max, $200 Max 20x. Note: ~4% of all public GitHub commits per day.
- **Codex CLI (OpenAI)** — Open source, Rust-built, fast. Terminal-Bench leader (~77.3%). Sandboxed by default. Bundled with ChatGPT Plus. Acquired ~1M devs in its first month after rebuild.
- **Gemini CLI (Google)** — Open source, Apache 2.0. The most generous free tier (1,000 reqs/day, 1M context). Plan Mode default. Best for huge monorepos. Less mature on complex multi-file refactors.
- **Aider** — Open source, BYOK. The one to mention for solo devs who want maximum model flexibility.
- **OpenCode, Cline (in VS Code as well), Hermes Agent** — honorable mentions.

The line worth saying out loud: **most professional developers in 2026 run at least two — one IDE-native tool and one terminal agent.** "Codex for keystrokes, Claude Code for commits" is a phrase floating around that captures the pattern.

**Category 3 — Cloud autonomous software engineers**
You assign a task; they go and do it in their own cloud sandbox. They have their own IDE, terminal, browser. You read the result.

- **Devin (Cognition)** — The category-defining tool. Plans, executes, opens the PR. Devin 2.2 (Feb 2026): 3x faster startup, unified UI across plan/code/review. Cognition's pricing pivot from $500/mo to $20/mo + $2.25 per ACU (one ACU ≈ 15 min of work) signals the shift toward mass adoption. Customers: Goldman Sachs, Santander, Nubank, Dell, Cisco, Infosys (across financial services), Cognizant partnership. Cognition's valuation reportedly $25B (April 2026). Cognition's own framing: *"if you can do it in three hours, Devin can probably do it."*
- **GitHub Copilot Coding Agent** — The autonomous agent that lives on GitHub itself. Assigned to issues, opens PRs.
- **Codex (cloud agents)** — OpenAI's cloud-side agent, integrated into ChatGPT app, Codex Chrome extension.
- **Google Jules** — Proactive cloud agent (finds improvements unprompted). 15 free tasks/day, 3 concurrent. Built on Gemini.
- **Cursor Cloud Agents (formerly Background Agents)** — Cursor's cloud-side companion to its IDE.
- **Replit Agent** — Vertically integrated: agent + IDE + hosting + DB in one product. Audience-relevant for prototyping and founders.
- **Factory.ai, Tembo, Sourcegraph Amp, Augment Code** — credible but lower-priority for this audience.

This is the row where the seniority-of-teammate metaphor lands hardest: a Devin task is closer to "I assigned this to a colleague" than "I'm using a tool."

**Category 4 — AI code review and quality**
Dedicated review-side agents.

- **CodeRabbit** — Most-used. Best signal-to-noise ratio (~46% accuracy, low false-positive rate). All four major Git platforms. $24/dev/mo Pro.
- **Greptile** — Highest raw bug catch rate (~82% in benchmarks vs CodeRabbit ~44%). Indexes full codebase. GitHub/GitLab only.
- **Qodo** — Multi-agent (Feb 2026 v2). Air-gapped/on-prem option. Open source PR-Agent underneath. Strong test generation.
- **Bugbot (Cursor)** — Now Cursor-acquired (via Graphite acquisition Dec 2025). Reviews 2M+ PRs/month. Auto-fix in sandbox VMs.
- **Macroscope** — Most autonomous: "Fix It For Me" spawns fix branch, "Approvability" can auto-approve low-risk PRs.
- **Anthropic's own multi-agent code review** (launched March 9, 2026) — worth mentioning as the platform's first-party play.

Key teaching point: as code generation accelerates, *the bottleneck moves to review.* CodeRabbit's own analysis: reviewers spend 91% more time on AI-generated code, with 3x more readability problems. This is why this category exists at all.

**Category 5 — Specialized / adjacent**
A short shelf at the end:

- **AI test generators** — Qodo's test feature, Codium-style.
- **AI doc generators** — Mintlify-style, Devin Wiki (auto-indexes repos and writes architecture docs).
- **Browser/UI testing agents** — Browserbase + Stagehand, Playwright MCP.
- **Spec-driven development tools** — GitHub Spec Kit (93K+ stars), Kiro, OpenSpec, BMAD-METHOD.
- **Context engineering platforms** — Augment Code's context engine, Intent's living-spec platform.

You won't have time to go deep here. The point of showing this row is to say "the category is fragmenting into specialists — don't be surprised when you see new names every month."

### Numbers that earn credibility

These are worth memorizing for the live session — they punch above their weight:

- Cursor: $2B+ ARR by Feb 2026
- Cognition (Devin): $25B valuation talks, April 2026
- GitHub Copilot: 28M MAUs, 37% market share
- ~70% of professional developers use 2-3 AI coding tools concurrently
- 80% of developers use AI tools in their workflow somewhere
- 40-62% of AI-generated code contains some kind of security vulnerability (Yan et al., 2025)
- 110,000+ surviving AI-introduced issues in production repos by Feb 2026 (arXiv 2026 study)
- Stack Overflow 2025 survey: 66% of developers say "AI solutions that are almost right, but not quite" is their top frustration

### One slide I'd build carefully: the seniority spectrum

Draw a horizontal axis. Far left: "junior intern at your shoulder" (autocomplete — Copilot's tab-suggestions). Middle: "pair-programming with a peer" (Cursor agent mode, Windsurf Cascade, Claude Code interactive). Right: "delegating to a colleague who works alone" (Devin, Jules, Codex Cloud). Far right: "swarms of colleagues" (Cursor 8 parallel agents, Claude Code Agent Teams, Antigravity's multi-agent orchestration).

The X-axis is essentially *how much trust per unit of supervision*. This is the same insight Day 2 will turn into the "unlimited junior developer" mindset.

---

## 2.3 Block: MCP — the connective tissue (40 min)

### How to teach it intuitively

The "USB-C for AI" analogy is well-worn by now — every blog uses it. I'd open with a different, more visceral framing:

> "Before MCP, every AI tool that wanted to read your GitHub issues had to build a GitHub integration. Every one that wanted to query your Postgres had to build a Postgres integration. Every one that wanted to post to Slack had to build a Slack integration. N tools × M systems = N×M integrations.
>
> MCP collapses that to N + M. Your tools speak MCP. Your systems expose MCP. Anything can talk to anything.
>
> The right mental model: **MCP is to AI tools what the LSP — Language Server Protocol — was to code editors a decade ago.** Before LSP, every editor had to write a TypeScript plugin, a Python plugin, a Rust plugin. After LSP, the languages built one server and every editor benefited. MCP is doing the same thing for tools."

The LSP analogy is gold for a developer audience because they've lived it.

### The minimum architecture they need to remember

Three components:
- **Host** — the AI app the human talks to (Claude Desktop, Cursor, ChatGPT, etc.)
- **Client** — the part of the host that speaks MCP
- **Server** — the thing on the other end exposing tools, resources, prompts

Two transports — stdio (local process) and Streamable HTTP (remote service). Streamable HTTP is what unlocked the production wave.

### The state of the ecosystem (mid-2026)

- Anthropic launched MCP November 2024.
- OpenAI officially adopted March 2025. Google followed.
- ~97M monthly SDK downloads, ~10,000+ live production MCP servers as of early 2026.
- ~28% of Fortune 500 had deployed MCP servers in production by early 2026.
- November 2025: MCP spec release; SEP-1865 (MCP Apps, formerly mcp-ui) standardizes interactive UIs from MCP servers.
- March 2026: MCP 2026 roadmap published — transport scalability, agent communication, governance maturation, enterprise readiness.
- April-May 2026: enterprise gateways (Kong AI Gateway, Cloudflare MCP server portals with Code Mode pattern) are how big shops are wrapping MCP servers in auth/audit.

### Servers worth naming

For developer audiences, name 6-8 max:
- **GitHub MCP** (issues, PRs, code) — also the canonical example of an MCP security incident, see below
- **Sentry MCP** (errors, traces)
- **Linear MCP** (tickets)
- **Postgres MCP, Supabase MCP** (databases)
- **Playwright MCP** (browser automation, UI testing)
- **Filesystem MCP** (enhanced — git-aware, .gitignore-respecting)
- **Memory / Knowledge Graph MCP** (persistent context across sessions)
- **Cloudflare Radar / Cloudflare MCP server portals** (enterprise pattern)

### The security section — don't skip it

This is where you earn the audience's adult-respect. MCP has had a rough 18 months on security and pretending otherwise damages your credibility.

Talking points:

- **Prompt injection via tool descriptions** — an attacker who can write text the LLM reads (an issue, a doc, an API response) can hijack the agent. OWASP ranks it #1 on the LLM Top 10. NIST called it "generative AI's greatest security flaw."
- **The GitHub MCP incident (May 2025)** — Invariant Labs disclosed: attacker creates a malicious issue in a public repo, developer asks their agent to "check the open issues," the agent reads the malicious instruction, follows it, and leaks data from *private* repos using the same credentials. Cross-repo data leakage.
- **OX Security's MCP SDK RCE disclosure (early 2026)** — architectural issue in Anthropic's MCP SDKs (Python, TypeScript, Java, Rust) enabled RCE in Cursor, VS Code, Windsurf, Claude Code, Gemini-CLI. CVE-2026-30615 was Windsurf with zero user interaction needed.
- **Tool poisoning** — malicious server modifies its own tool description to manipulate which tools the agent picks.
- **The architectural reality**: traditional input validation doesn't help, because the LLM *is* the validation layer and it's the thing being attacked.

The practical lessons you give the audience:
1. Run MCP servers least-privileged. Not as root, scoped API keys, container-isolated where possible.
2. Treat content from MCP tool results (issues, docs, API responses) as *untrusted user input*, not as trusted system context.
3. For enterprise: use a gateway (Kong, Cloudflare, Lasso) for centralized auth, audit, and scope control.
4. Be very careful with cross-server interactions — agents with access to both a public-content server and a private-data server are the highest-risk pattern.

### Should they build an MCP server today?

My take for this audience: **use, don't build.** A 4-hour Day 1 won't fit a build-a-server walkthrough without crowding everything else. Show them an MCP server config in Cursor or Claude Code, show them the tool list it exposes, show them a tool call happening. Note that building a server is a couple-hour task, and earmark it as a follow-up workshop topic.

---

## 2.4 Block: Special markdown files (45 min)

This block is where you want maximum stickiness — most of the audience has never heard the phrase "AGENTS.md" but it will reshape how they configure their projects within a year.

### The story to open with

Use Karpathy here.

> "April 13, 2026. A plain markdown file uploaded by Andrej Karpathy hits 7,900 GitHub stars in a single day. Within three months: 110,000+ stars. Twenty-eight consecutive days at #1 on GitHub Trending. Top 100 of all repositories ever.
>
> The repo contains one file. The file is 65 lines. It's just text — no code, no framework, no install script. Four behavioral rules for how an AI coding agent should act on your codebase.
>
> How does a markdown file accumulate more stars than most successful libraries? Because every developer who'd been using Claude Code or Cursor for a month recognized the four pain points instantly. Karpathy didn't invent anything — he named the frustrations everyone was feeling. And he gave them the recipe to fix them in a file the agent reads on every session.
>
> *This* is what we're going to learn how to write."

That story does the whole "why does this matter" job for you in 90 seconds.

### The current landscape of files

Walk through these in this order, building a stack:

**Layer 1 — Project context (the one everyone needs)**
- **AGENTS.md** — the emerging open standard. Backed by Sourcegraph, OpenAI, Google, Cursor, Factory; now governed under the Linux Foundation's Agentic AI Foundation. Supported by 20+ tools natively. As of April 2026: ~60,000+ open-source repos adopted.
- **CLAUDE.md** — Claude Code's native format. Claude Code reads AGENTS.md too but adds Claude-specific features (`@imports`, the `/init` workflow). Anthropic hasn't fully made CLAUDE.md a symlink to AGENTS.md — the workaround `ln -s AGENTS.md CLAUDE.md` is standard.
- **GEMINI.md** — Gemini CLI's format, hierarchical (global, project, subdirectory).
- **.github/copilot-instructions.md** — Copilot's format.
- **.cursorrules / .cursor/rules/*.mdc** — Cursor's older format and newer MDC format with YAML frontmatter and activation modes.
- **.windsurfrules**, **.aider.conf.yml**, **Cline's memory bank** — minor formats.

**The pragmatic recommendation to give the audience:** maintain AGENTS.md as your single source of truth. Keep CLAUDE.md as a thin file that either symlinks to AGENTS.md or references it plus adds the few Claude-specific things you need.

**Layer 2 — Capability extensions (newer, more powerful)**
- **SKILL.md** (Agent Skills open standard) — directory-based, YAML frontmatter, can include supporting scripts/references. Started as Anthropic's format for Claude Code, now adopted by Codex CLI, Gemini CLI, Copilot, Cursor, Cline, Windsurf, OpenCode. *Loaded on demand* via progressive disclosure — only the description (frontmatter) sits in context until invoked.
- Slash commands / **.claude/commands/** — repeatable workflows (e.g., `/pr`, `/fix-issue`, `/review`).
- **Hooks** — shell commands that fire on agent events (e.g., before a destructive command, on PR creation).
- **Subagent definitions** — `.claude/agents/*.md` files defining specialized subagents with restricted tool access.

**Layer 3 — Project structure files the agents read anyway**
Worth saying out loud: agents already read README.md, ARCHITECTURE.md, CONTRIBUTING.md, package.json, tsconfig.json, the linter config. *You do not need to repeat in CLAUDE.md what these files already say.* This is one of the top failure modes — bloated rules files restating things the agent could infer.

### What goes inside (a content checklist)

GitHub's analysis of 2,500+ agent files surfaced a pattern. Effective agent context files share these sections:

1. **Project overview** — what is this, who uses it, what business problem
2. **Build / dev setup** — exact commands (`pnpm install`, `pnpm dev`, ports, env files)
3. **Test commands** — how to run tests, what passing looks like
4. **Code style** — *only* things the linter can't enforce
5. **Architecture overview** — major modules, data flow, where layers live
6. **Conventions** — naming, error handling, logging patterns
7. **Don't-touch list** — files/directories the agent shouldn't modify
8. **Gotchas** — non-obvious things that have bitten you, with concrete examples
9. **Release / deploy notes** — branch model, commit conventions, where docs go

### The importance score you asked for

You asked me to score these. I've thought hard about the right axis. The cleanest is **"impact on agent quality per minute of effort to write."** High score = high leverage. Here's my ranking with reasoning:

| File / section | Importance | Why |
|---|---|---|
| AGENTS.md / CLAUDE.md (project overview) | **5/5** | Single highest-ROI artifact. Without it the agent guesses what your project even is. |
| Build / test commands inside the rules file | **5/5** | Massive. Agents waste cycles trying to figure out how to run tests. Tell them once. |
| Gotchas section | **5/5** | Anthropic engineers call this the highest-signal content in any skill or rules file. |
| Don't-touch list | **4/5** | Cheap to write, prevents catastrophic edits. |
| Architecture overview (high-level) | **4/5** | Agents will infer most of this — but high-level "what layer does what" is hard to infer and high-payoff to state. |
| Conventions / naming | **3/5** | Useful but partially redundant with linter. Worth writing only the parts linters can't enforce. |
| SKILL.md (custom skills for repeated workflows) | **4/5** | High leverage, but earns its score only if you have workflows worth automating (PR creation, deploys, etc.). |
| Subagents (.claude/agents/) | **3/5** | High ceiling, requires investment. Skip for teams just starting. |
| Hooks | **2/5** | Power-user feature. Worth knowing exists. Don't build day 1. |
| Slash commands (.claude/commands/) | **3/5** | Cheap wins for repeated workflows. |
| README.md / ARCHITECTURE.md | **3/5** | Important but agent-orthogonal — agents read them anyway. Maintain for humans first, agents benefit incidentally. |
| Verbose "personality" instructions ("be a senior engineer", etc.) | **1/5** | Mostly waste. The Karpathy file showed: behavioral rules matter way more than role-playing. |

### Timing — when each file gets loaded

This is the subtle thing you wanted me to dig into. Agents don't load all files always. The hierarchy:

- **Always-loaded (system prompt level):** the rules file in the project root (AGENTS.md or CLAUDE.md). Stays in context across all turns.
- **Hierarchical override:** subdirectory AGENTS.md files override parent ones. "Nearest file wins."
- **On-demand:** SKILL.md frontmatter is in context, but the body and supporting files only load when Claude (or the user) invokes the skill. This is the *progressive disclosure* pattern — context-budget-aware.
- **Event-triggered:** hooks fire on specific lifecycle events.
- **Subagent-isolated:** subagent definitions only load when the parent agent delegates to that subagent. Subagent gets its own context window.

This timing story matters because it teaches the audience to think about *context budget*. Every line in CLAUDE.md is a token tax on every turn. Every line in a SKILL.md only costs you when invoked. Once you internalize this, your decisions about where to put what change.

### Karpathy's four principles (the ones to actually share)

From the viral file, paraphrased so we're not reproducing the original:

1. **No assumptions.** If the agent doesn't know, ask. Don't guess and write code on the guess.
2. **Surgical edits only.** Don't touch files unrelated to the task. Don't sneak in improvements.
3. **Define success criteria.** State up front what "done" looks like before writing code.
4. **No over-engineering.** Don't add layers of abstraction, helper functions, or error handling that wasn't asked for.

The point isn't to copy-paste this file. The point is to recognize that *four behavioral rules outperformed a hundred lines of instructions* for most users. Brevity is leverage.

---

## 2.5 Block: Best practices (25 min)

This is the meta-layer. By now the audience has seen the tools and the failure modes — these practices land as relief.

### Six principles, each with a story or analogy

**1. Treat AI agents like capable junior developers, not search engines.**
Story to use: the 19% METR slowdown. Developers who used AI as autocomplete-on-steroids got slower. Developers who treated it as delegation got faster. The shift is *managerial*, not *technical*. (This sets up Day 2.)

**2. Context engineering has replaced prompt engineering.**
Anthropic's 2026 Agentic Coding Trends Report calls this the most important skill shift of the year. Story: you're not crafting the perfect sentence anymore. You're building the *environment* the agent thinks in — the files it can read, the rules it follows, the tools it can reach, the history it carries. The clever prompt era is gone. The information-architecture era is here.

**3. Spec before code.**
GitHub's framing: developers treat agents like search engines when they should treat them like literal-minded pair programmers. *Vibe-coding* (prompt-iterate-vibe) works for prototypes but breaks on production code. *Spec-driven development* — write the spec, get sign-off, then generate against it — produces measurably better code, especially in brownfield codebases. Tools to name: GitHub Spec Kit (93K+ stars), Kiro (AWS), and informal patterns like writing a `plan.md` before kicking off Claude Code.

**4. Review is the new bottleneck. Plan for it.**
As generation accelerates, the constraint moves to review. CodeRabbit's data: reviewers spend 91% more time on AI-generated code, 3x more readability problems. Practical implication: invest in your review tooling (CodeRabbit/Qodo/Greptile in CI), and don't measure productivity by PRs opened — measure by PRs *merged with no regressions*.

**5. Verify with evidence, not narrative.**
A recurring failure mode: agents produce confident, well-structured prose claiming the code works — and the code doesn't work. Story to use: hallucinated package names, fake commit SHAs, invented API versions (the documented Claude Code "post-compaction hallucination" problem). The discipline: every claim by the agent needs corresponding evidence — test output, lint output, actual diff. The TDD-style "RED → GREEN → REFACTOR" pattern enforced in obra's Superpowers skills library is one mature instantiation of this.

**6. The agent is not the source of truth. The spec is.**
This is the "spec-as-anchor" mindset. If your agent and your spec disagree, the spec wins. If the implementation drifts, you update the spec first, then re-generate or hand-fix. The most mature teams in 2026 treat spec docs as living artifacts under version control, not throwaway PRDs.

### A seventh, optional principle if time permits

**7. Use the right tool for the right station.**
Don't ask Cursor to do a multi-hour refactor with no supervision (that's Devin's job). Don't ask Devin to fix a typo in a comment (that's autocomplete's job). Mismatching tool to task burns time and money on both ends.

### The killer caveats slide (be honest)

End the section with a short, sober slide:

- AI-generated code is vulnerable. 40–62% of AI-generated code contains some kind of security vulnerability (Yan et al. 2025). 110K+ surviving AI-introduced issues in production repos by Feb 2026.
- Devin's documented failure rate on complex tasks: ~85%. PR merge rate on *well-defined* tasks: ~67%. Translation: scoping is everything.
- Developer self-perception is unreliable. METR study: devs were 19% slower but believed they were 20% faster. Your gut isn't measuring what you think it is.
- Two thirds of developers report spending more time fixing AI-generated code than they save (Stack Overflow 2025).
- Trust in AI accuracy dropped from 40% to 29% YoY (2024 → 2025).

The point of this slide isn't to scare. It's to make sure the audience leaves understanding that the productivity gains *only* show up when you've internalized the practices above. Otherwise they get the slowdown without knowing it.

---

## 2.6 The cliffhanger (5 min)

End the session by drawing the audience's attention back to the SDLC grid from earlier — specifically the **bottom row, the horizontal bar across all seven stations.**

> "We spent four hours mapping where each kind of AI tool sits in your work. Most tools occupy one station. The ones in the bottom row — Devin, Jules, Codex Cloud, GitHub's coding agent — sit on all seven.
>
> Here's the thing about that row that we haven't talked about yet. A Devin task costs about $2.25 per ACU. An ACU is fifteen minutes of work. That's roughly $9 an hour for an autonomous engineer that runs in the cloud, takes on a Linear ticket, and opens a PR while you sleep.
>
> $9 an hour. In parallel. Twenty-four of them at once if you want.
>
> Next week we're going to take that one fact and work out what it means for how enterprises, startups, and individual developers should think. We're going to talk about how to stop thinking of Devin as a 'tool you buy a license for' and start thinking of it as *an unlimited supply of junior developers* — and how that one mental shift changes how you scope work, how you organize your team, and how you think about your own time.
>
> Come back next week. Bring questions."

That's the bridge. Drop the mic.

---

# Part 3 — Open questions for you

Things I want you to decide before we build the interactive lesson:

1. **Are you sold on the ordering swap?** (SDLC before tools, best-practices last, my proposed order vs. yours.) If you'd rather keep your original order, we can — but I'd at least lobby for SDLC moving up to position 2.

2. **Do you want the cliffhanger to mention the $9/hour ACU figure explicitly,** or do you want to keep that as the *opener* of Day 2 so Day 1 ends on a softer "we'll talk about the bottom row next week"?

3. **Live demos — yes or no, and if yes, which?** My recommendations if you do demos:
   - During the *tools landscape* block: a 90-second Cursor parallel-agents demo (cheap, visual, makes the point about scale).
   - During the *MCP* block: show Claude Code with the GitHub MCP server connected, do one real tool call (e.g., "list my open issues"). 60 seconds.
   - During the *markdown files* block: show a real CLAUDE.md from one of your DevTuskers projects (VedicAstro.me or Ivoreel — both have agent-ready specs already, so it's natural to show).
   - **Skip a Devin demo on Day 1.** Save it for Day 2 — Devin's demo is the Day 2 hook.

4. **How much time on enterprise governance?** The Sri Lankan audience is going to have at least some learners thinking about this in their day jobs (Sysco/CoDev/Big4-Lanka type companies). MCP gateways, audit logs, data governance — I covered them lightly in the report. If you want me to deepen this for the lesson material, signal it.

5. **Workshop-mode interactivity?** Your "lesson" format is single-file HTML with live demos. Do you want me to design 2-3 interactive widgets specifically — e.g., a "drag the tool onto the SDLC stage" exercise, a "score this CLAUDE.md" exercise, a live MCP tool-call visualization — or keep it presentation-style throughout?

6. **One I'd particularly like your call on:** Do you want me to include a *concrete recommended stack* slide near the end — "if you walk out of this session and want to start, here's the minimum-viable setup for an individual / a startup / an enterprise"? It would be opinionated. It would also be the most actionable single slide of the night.

7. **Tone-check on the security section.** I've written it adult-honest — MCP has had a rough year on security. That's truthful but could be uncomfortable for an audience that wants to be told it's all unicorns. You're the better judge of your audience's tolerance for "yes, this stuff has problems too." Do you want it kept as-is, softened, or expanded?

---

# Part 4 — What I'd build next, once you've answered

Once you've responded to those seven questions, I'd recommend the next pass produces:

1. A **detailed lesson outline** — your seven blocks, broken into 5-10 minute beats, with exact talking points, slide cues, and demo prompts.
2. A **list of visuals to commission** — the SDLC grid, the seniority spectrum, the MCP architecture diagram, the markdown files stack diagram, the tools-landscape taxonomy chart.
3. Then we build the **interactive single-file HTML lesson** that turns all of this into the format you've been using for Weeks 1–3.

Ready when you are. Tell me which of the seven questions you want to answer and we'll move.
