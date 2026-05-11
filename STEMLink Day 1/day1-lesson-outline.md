# Day 1 Lesson Outline — Beat-by-Beat

**Duration:** 4 hours (240 min), 7:00 PM – 11:00 PM
**Format:** Interactive single-file HTML, presentation-style, with live animations and three live demos
**Break:** One 15-min break around the 2-hour mark

---

## Time budget at a glance

| # | Block | Duration | Cumulative |
|---|---|---|---|
| 1 | Hook + framing | 15 min | 0:15 |
| 2 | The SDLC map | 35 min | 0:50 |
| 3 | The tools landscape (incl. Live Demo #1) | 60 min | 1:50 |
| — | **Break** | 15 min | 2:05 |
| 4 | MCP — connective tissue (incl. Live Demo #2) | 45 min | 2:50 |
| 5 | Markdown files (incl. Live Demo #3) | 45 min | 3:35 |
| 6 | Best practices | 25 min | 4:00 |
| 7 | Recommended stack slide + cliffhanger | 5 min (folded into block 6) | 4:00 |

Note: Block 7 ("Recommended stack" slide and Day 2 teaser) is intentionally short and folded into the tail of Block 6 to land cleanly at 11:00 PM. If running long, the recommended-stack slide compresses to 90 seconds.

---

## Block 1 — Hook + framing (15 min, 7:00–7:15)

### Beat 1.1 (3 min) — Walk-in + the METR paradox
- Slide: title slide of session.
- Tell the METR study story end-to-end. The numbers: 16 devs, 246 tasks, randomized, Cursor + Claude 3.5/3.7 Sonnet. Predicted: 24% speedup. Felt: 20% speedup. Actual: **19% slowdown.**
- Pause. Let it land.
- Then pivot: Cognizant CEO says 30% of code is AI-generated, targeting 50%. Infosys deploys Devin across financial services. Visma: 2x productivity, 50% cost reduction.
- "So which is it?"

### Beat 1.2 (4 min) — The frame: AI tools as teammates
- Introduce the spine: these aren't tools, they're a *spectrum of teammates*.
- Build the seniority axis verbally: intern at your shoulder → peer pair-programmer → colleague who works alone → swarm of colleagues.
- Don't show the visual yet — it pays off in Block 3. Just plant the idea.

### Beat 1.3 (4 min) — What changed in the last 18 months
- Three things that flipped the field:
  1. Models got good enough that the bottleneck moved from "can it write code" to "can you direct it well"
  2. Agentic loops let tools run for *minutes to hours* unsupervised (this is the 2026-defining feature)
  3. MCP became the standard connective tissue, so tools can reach beyond the chat window
- Pose the question: "If your colleague suddenly upgraded from 'can answer a question' to 'can take a ticket and ship a PR' — does your team's workflow need to change? Spoiler: yes. That's what we're here to learn."

### Beat 1.4 (4 min) — What this session covers + sets up Day 2
- Roadmap slide: the six blocks the audience is about to walk through.
- One sentence on Day 2: "Next week is about a single mental shift — and we'll earn the right to make it tonight."

**Visuals needed for Block 1:**
- Title slide
- METR paradox slide — large numbers, no clutter (animate the numbers in: 24% → 20% → -19%)
- "What changed" slide — three pillars
- Session roadmap — six numbered blocks

---

## Block 2 — The SDLC map (35 min, 7:15–7:50)

### Beat 2.1 (5 min) — Why SDLC first, not last
- Hand-wave the classic SDLC briefly (plan → design → code → test → ship → operate). Audience knows this.
- Reframe as a *loop*, not a line. Critical: draw the feedback arrow from "operate → plan."
- The point about the loop: "Until 2025, humans closed this loop. In 2026, agents are starting to close it themselves."

### Beat 2.2 (10 min) — Build the seven stations
- Animate the loop onto the slide, station by station:
  1. Discover / Plan
  2. Design
  3. Implement
  4. Review
  5. Test
  6. Ship
  7. Operate
- For each station, ask: "What does this station look like in *your* week? Hands up if you spend most of your week here." Quick audience pulse-check.

### Beat 2.3 (15 min) — The money slide
- Reveal the grid: stations on x-axis, tool categories on y-axis. Empty at first.
- Animate fills in this order:
  - **IDE-bound tools** → fill Implement, partial Design, partial Review. Pause. "These are most of the tools you've heard of. They upgrade one station."
  - **Terminal agents** → fill Implement, Review, Test, partial Ship.
  - **Dedicated reviewers** → one tall column under Review.
  - **Cloud autonomous engineers** → animate a *horizontal bar across all seven stations*. **This is the visual punchline.**
- Pause. Let the audience see the difference.
- Script: "Most tools are dots in one column. Devin-class agents draw a line across the whole loop. This isn't a 'better IDE.' This is a fundamentally different kind of teammate. We'll come back to this row in detail."

### Beat 2.4 (5 min) — Stat reinforcement
- Throw three numbers on screen:
  - Cognizant: 30% of code AI-generated, targeting 50%
  - Visma + Devin: 2x developer productivity, 50% project cost reduction
  - Qodo report: AI code review usage lifted quality from 55% to 81%
- "The bottom row is why those numbers exist."

**Visuals needed for Block 2:**
- The seven-station SDLC loop (animated assembly)
- The big grid (stations × tool categories) with animated fills — this is *the* signature visual of the session
- Stats reinforcement slide

---

## Block 3 — The tools landscape (60 min, 7:50–8:50)

### Beat 3.1 (3 min) — The seniority spectrum
- Pay off the metaphor from Block 1. Draw a horizontal axis.
- Far left: "intern at your shoulder" → autocomplete (Copilot)
- Middle: "peer pair-programmer" → Cursor agent, Windsurf Cascade
- Right: "colleague who works alone" → Devin, Jules, Codex Cloud
- Far right: "swarm of colleagues" → Cursor 8 parallel agents, Claude Code Agent Teams, Antigravity multi-agent
- Reframe the axis: "this is really about how much trust you give per unit of supervision."

### Beat 3.2 (12 min) — Category 1: IDE-native AI assistants
- Walk through each, ~90 seconds each:
  - **Cursor** — dominant, Composer model, 8 parallel agents, $2B+ ARR, ~14M MAUs
  - **Windsurf** — Cognition-owned, Cascade, $15/mo value play
  - **GitHub Copilot** — 28M MAUs, 37% share, cheapest at $10/mo, deepest GitHub integration
  - **Zed** — Rust-native, fastest editor, BYO-agent model
  - **JetBrains AI Assistant + Junie** — for the IDE-loyal crowd
  - **Antigravity** — Google's agent-first IDE, multi-agent from day one, free preview
  - **Kiro** — AWS-native, spec-driven, EARS syntax
- One slide showing the comparison matrix at the end.

### Beat 3.3 (10 min) — Category 2: Terminal / CLI agents
- **Claude Code** — best quality on hard problems, deepest harness (Skills/Hooks/Subagents/MCP), ~4% of all public GitHub commits
- **Codex CLI** — open source, Rust, Terminal-Bench leader, bundled with ChatGPT Plus
- **Gemini CLI** — most generous free tier, 1M context, best for huge monorepos
- **Aider, OpenCode, Hermes, Cline** — honorable mentions
- The line to say out loud: **"Most pros run two — one IDE-native, one terminal. 'Codex for keystrokes, Claude Code for commits.'"**

### Beat 3.4 (12 min) — Category 3: Cloud autonomous software engineers
- This is the row that will reshape their thinking. Spend more time here.
- **Devin** — category-defining. Plans, executes, opens the PR. Pricing pivot from $500/mo to $20/mo + $2.25/ACU. Customers: Goldman Sachs, Santander, Nubank, Dell, Cisco, Infosys, Cognizant. $25B valuation talks.
- Cognition's own framing: *"if you can do it in three hours, Devin can probably do it."*
- **GitHub Copilot Coding Agent** — lives on GitHub, assigned to issues
- **Codex (cloud)** — OpenAI's cloud agent
- **Google Jules** — proactive, 15 free tasks/day
- **Cursor Cloud Agents** — IDE companion
- **Replit Agent** — vertically integrated for prototyping
- Plant the seed: "We'll come back to this row at the end of the night, and again next week."

### Beat 3.5 (8 min) — **Live Demo #1: Cursor parallel agents**
- Open Cursor in front of the audience.
- Show 3 agents running in parallel on a real (small) task. Worktrees visible.
- ~90 seconds of actual demo, ~3 min of narration around it.
- The point isn't the task — the point is that the audience *sees* multiple agents working concurrently.

### Beat 3.6 (8 min) — Category 4: AI code review
- The bottleneck has moved to review. CodeRabbit's data: 91% more time on AI-generated PRs, 3x more readability problems.
- **CodeRabbit** — best signal-to-noise, all four Git platforms, $24/dev/mo
- **Greptile** — highest bug catch rate (82% vs CodeRabbit 44%), GitHub/GitLab only
- **Qodo** — multi-agent, air-gapped option, open-source PR-Agent base
- **Bugbot** — Cursor-acquired via Graphite, 2M+ PRs/month, sandbox VM auto-fix
- **Macroscope** — most autonomous, can auto-approve low-risk PRs
- **Anthropic's multi-agent code review** — March 2026 launch

### Beat 3.7 (5 min) — Category 5: Specialized / adjacent
- Quick shelf — name and one-liner each:
  - **Test generators** — Qodo's test feature
  - **Doc generators** — Mintlify, Devin Wiki
  - **Browser testing agents** — Browserbase + Stagehand, Playwright MCP
  - **Spec-driven dev** — GitHub Spec Kit (93K+ stars), Kiro, OpenSpec
  - **Context engineering platforms** — Augment, Intent
- The reason to mention: "The category is fragmenting into specialists. Expect new names monthly. Don't panic — they all sit somewhere on the grid you already learned."

### Beat 3.8 (2 min) — Reality check stat slide
- 70% of pros run 2-3 tools concurrently. 80% of devs use AI tools somewhere.
- "If you walk out with nothing else tonight, walk out with: pick one IDE-native, pick one terminal agent, get fluent in both."

**Visuals needed for Block 3:**
- Seniority spectrum (horizontal axis with tool placements)
- Category 1 matrix (IDE tools)
- Category 2 matrix (terminal agents)
- Category 3 matrix (cloud autonomous engineers) — visually distinct, emphasize this row
- Category 4 matrix (code reviewers)
- Category 5 — quick visual shelf
- Live demo screen placeholder

---

## **Break (15 min, 8:50–9:05)**

---

## Block 4 — MCP, the connective tissue (45 min, 9:05–9:50)

### Beat 4.1 (4 min) — The N×M problem
- Visual: a "before MCP" diagram. N tools (Cursor, Claude Code, Devin, Copilot…) on the left. M systems (GitHub, Postgres, Slack, Sentry, Linear…) on the right. Tangled spaghetti of N×M connections between them.
- Animate the spaghetti collapsing into N + M when MCP sits in the middle.

### Beat 4.2 (4 min) — The LSP analogy
- "Remember LSP? Language Server Protocol? Ten years ago every editor had to write a TypeScript plugin, a Python plugin, a Rust plugin. After LSP, languages built one server and every editor benefited. **MCP is the LSP moment for AI tools.**"
- This analogy is gold for a developer audience.

### Beat 4.3 (6 min) — Architecture in three components
- **Host** — the AI app the human talks to
- **Client** — the part of the host that speaks MCP
- **Server** — exposes tools, resources, prompts
- Two transports: stdio (local process) and Streamable HTTP (remote service)
- Streamable HTTP is what unlocked production deployment

### Beat 4.4 (5 min) — State of the ecosystem
- 97M monthly SDK downloads
- 10,000+ live production MCP servers
- 28% of Fortune 500 deployed MCP in production by early 2026
- Adoption timeline: Anthropic Nov 2024 → OpenAI March 2025 → Google → spec Nov 2025 → 2026 roadmap

### Beat 4.5 (8 min) — The servers worth knowing
- Walk through 8 servers, ~60 seconds each:
  - **GitHub MCP** (issues, PRs)
  - **Sentry MCP** (errors, traces)
  - **Linear MCP** (tickets)
  - **Postgres / Supabase MCP** (databases)
  - **Playwright MCP** (browser automation)
  - **Filesystem MCP** (git-aware, .gitignore-respecting)
  - **Memory / Knowledge Graph MCP** (persistent context)
  - **Cloudflare MCP server portals** (enterprise pattern)

### Beat 4.6 (5 min) — **Live Demo #2: MCP in action**
- Claude Code with GitHub MCP server connected.
- Real tool call: "list my open issues" or "fetch the README of [repo]."
- Show the tool definition, the call, the response, the model's reasoning.
- 60 seconds of demo, ~4 min of narration.

### Beat 4.7 (10 min) — Security — adult honest
- Open with: "Now the part nobody wants to hear, but you need to know."
- **Prompt injection** — OWASP #1 on the LLM Top 10. NIST called it "generative AI's greatest security flaw."
- **The GitHub MCP incident, May 2025** — Invariant Labs disclosure. Attacker plants malicious issue in public repo. Developer asks agent "check the issues." Agent reads instruction, follows it, leaks data from *private* repos using same credentials. Cross-repo data leakage.
- **OX Security's RCE disclosure (early 2026)** — architectural issue in Anthropic's MCP SDKs (Python/TS/Java/Rust). Affected Cursor, VS Code, Windsurf, Claude Code, Gemini-CLI. CVE-2026-30615: Windsurf RCE with **zero user interaction**.
- **Tool poisoning** — malicious server modifies its own tool description.
- **Why traditional input validation doesn't help** — the LLM *is* the validation layer, and it's the thing being attacked.

### Beat 4.8 (3 min) — Practical defenses
- Run MCP servers least-privileged (not as root, scoped API keys, container-isolated)
- Treat MCP tool result content as *untrusted user input*, not trusted system context
- For enterprise: use a gateway (Kong AI Gateway, Cloudflare MCP portals, Lasso Security)
- Highest-risk pattern: an agent with simultaneous access to a public-content server AND a private-data server

**Visuals needed for Block 4:**
- N×M → N+M diagram (animated)
- LSP analogy diagram
- MCP three-component architecture
- Ecosystem state stats
- Eight MCP servers visual shelf
- Live demo screen placeholder
- Security incident timeline (GitHub MCP attack, OX RCE)
- Practical defenses checklist

---

## Block 5 — Special markdown files (45 min, 9:50–10:35)

### Beat 5.1 (5 min) — The Karpathy story
- Date: April 13, 2026.
- A plain markdown file uploaded by Andrej Karpathy hits 7,900 GitHub stars in a single day.
- Within three months: 110,000+ stars. 28 consecutive days at #1 on GitHub Trending.
- The repo contains one file. The file is 65 lines. Just text — no code, no framework, no install script.
- "How does a markdown file accumulate more stars than most successful libraries? Because every developer who'd been using Claude Code or Cursor for a month recognized the four pain points instantly. Karpathy didn't invent anything. He named what everyone was feeling."

### Beat 5.2 (8 min) — The three-layer stack
- Visual: a layered diagram, build it up bottom-to-top.
- **Layer 1 — Project context (everyone needs)**
  - **AGENTS.md** — emerging open standard, Linux Foundation governed, 20+ tools, ~60K+ repos
  - **CLAUDE.md** — Claude's native; Claude reads AGENTS.md too; symlink pattern `ln -s AGENTS.md CLAUDE.md`
  - **GEMINI.md**, **.github/copilot-instructions.md**, **.cursorrules / .cursor/rules/*.mdc**, **.windsurfrules**
- **Layer 2 — Capability extensions (newer)**
  - **SKILL.md** — open standard, directory-based, YAML frontmatter, progressive disclosure
  - **Slash commands** — `.claude/commands/`
  - **Hooks** — shell commands fire on agent events
  - **Subagent definitions** — isolated contexts, restricted tool access
- **Layer 3 — Project structure files agents read anyway**
  - README.md, ARCHITECTURE.md, CONTRIBUTING.md, package.json, tsconfig.json, linter configs
  - **"Don't repeat what these already say."**

### Beat 5.3 (5 min) — What goes inside (the content checklist)
- The nine sections from GitHub's analysis of 2,500+ files:
  1. Project overview
  2. Build / dev setup commands
  3. Test commands
  4. Code style (only what linter can't enforce)
  5. Architecture overview
  6. Conventions
  7. Don't-touch list
  8. Gotchas
  9. Release / deploy notes

### Beat 5.4 (10 min) — The importance score
- The table — go through it row by row, briefly explaining the score:
  - AGENTS.md/CLAUDE.md project overview: **5/5**
  - Build/test commands: **5/5**
  - Gotchas section: **5/5**
  - Don't-touch list: **4/5**
  - Architecture overview: **4/5**
  - SKILL.md for repeated workflows: **4/5**
  - Slash commands: **3/5**
  - Conventions/naming: **3/5**
  - Subagents: **3/5**
  - README/ARCHITECTURE.md (for agent use specifically): **3/5**
  - Hooks: **2/5**
  - Verbose role-playing instructions: **1/5**

### Beat 5.5 (5 min) — Timing — when each file loads
- Critical insight: not all files load all the time.
- **Always-loaded:** rules file in project root (CLAUDE.md / AGENTS.md) — every line is a token tax on every turn
- **Hierarchical override:** subdirectory rules override parent ("nearest file wins")
- **On-demand:** SKILL.md frontmatter in context, body loads on invocation (*progressive disclosure*)
- **Event-triggered:** hooks fire on specific lifecycle events
- **Subagent-isolated:** subagent definitions only load when delegated to
- Why this matters: it teaches *context budget thinking*.

### Beat 5.6 (5 min) — **Live Demo #3: Real CLAUDE.md walkthrough**
- Show a real CLAUDE.md from VedicAstro.me or Ivoreel (your DevTuskers projects).
- Walk through the sections. Point out what's there, what's deliberately not there.
- Show the project tree with `.claude/` directory if it exists.
- ~5 min total, no slides during demo.

### Beat 5.7 (7 min) — Karpathy's four principles
- The four behavioral rules from the viral file (paraphrased — we don't reproduce the original):
  1. **No assumptions.** If the agent doesn't know, ask. Don't guess.
  2. **Surgical edits only.** Don't touch unrelated files. Don't sneak in improvements.
  3. **Define success criteria.** State what "done" looks like before writing code.
  4. **No over-engineering.** No layers of abstraction or error handling that wasn't asked for.
- The takeaway: **four behavioral rules outperformed a hundred lines of instructions for most users. Brevity is leverage.**

**Visuals needed for Block 5:**
- Karpathy story slide (visual of the GitHub stars chart)
- Three-layer markdown files stack diagram — build animated layer by layer
- Content checklist (the nine sections)
- Importance-score table — make this visually rich, color-coded by score
- File-loading timing diagram (when does each file enter context)
- Live demo screen placeholder
- Karpathy's four principles slide

---

## Block 6 — Best practices + governance + recommended stack + cliffhanger (25 min, 10:35–11:00)

### Beat 6.1 (12 min) — Six principles
Walk through each, ~2 min each:

1. **Treat AI agents like capable junior developers, not search engines.** Story: METR 19% slowdown — autocomplete-on-steroids users got slower; delegators got faster. The shift is managerial, not technical. (Plants Day 2.)

2. **Context engineering has replaced prompt engineering.** Anthropic's 2026 Agentic Coding Trends Report calls it the most important skill shift of the year. You're not crafting the perfect sentence — you're building the *environment*: files the agent reads, rules it follows, tools it can reach, history it carries.

3. **Spec before code.** Vibe-coding works for prototypes, breaks on production. Spec-driven development (GitHub Spec Kit, Kiro, or even an informal `plan.md`) produces measurably better code, especially brownfield.

4. **Review is the new bottleneck.** As generation accelerates, the constraint moves to review. CodeRabbit data: reviewers spend 91% more time on AI-generated code. Invest in your review tooling. Measure PRs *merged without regression*, not PRs opened.

5. **Verify with evidence, not narrative.** Agents produce confident prose claiming code works — and it doesn't. Hallucinated package names, fake SHAs, invented API versions. The discipline: every claim by the agent needs corresponding evidence — test output, lint output, actual diff.

6. **The agent is not the source of truth. The spec is.** If your agent and your spec disagree, the spec wins. Treat spec docs as living artifacts under version control.

### Beat 6.2 (5 min) — Governance (deepened per your request)
- Why this matters more now: when a single Devin task can touch your codebase, your databases, your deployment infra, governance isn't a future problem — it's already happening.
- **The three governance pillars:**
  1. **Access control** — least-privilege MCP servers, scoped API keys, time-bound credentials, SSO-integrated auth
  2. **Audit trails** — every agent action logged, every MCP tool call recorded, every PR traceable to which agent on which prompt
  3. **Guardrails** — sandboxed execution environments, gateways like Kong AI Gateway / Cloudflare MCP portals / Lasso Security
- **Enterprise patterns surfacing in 2026:**
  - MCP server portals (centralized discovery + auth) — Cloudflare's pattern
  - Code Mode (progressive tool disclosure) — reduces token cost by 99.9% and improves auditability
  - Permission systems that distinguish read-only from write operations (Claude Code's permission model)
- **The hard truth:** 83% of companies deploying AI agents discovered their traditional security tools weren't built for this. The EU AI Act (high-risk obligations starting August 2026) treats specifications as evidence — fines up to €15M or 3% of global turnover.
- **What to do Monday morning:**
  - Inventory: which agents have access to what?
  - Scope: are API keys least-privileged?
  - Audit: is every agent action logged somewhere replayable?
  - Pilot: pick one team, deploy with full governance, expand from there

### Beat 6.3 (5 min) — Adult-honest caveats slide
- 40–62% of AI-generated code contains some kind of security vulnerability (Yan et al. 2025)
- 110,000+ surviving AI-introduced issues in production repos by Feb 2026
- Devin: ~85% failure rate on complex tasks; ~67% PR merge rate on *well-defined* tasks. Scoping is everything.
- METR: 19% slowdown, devs believed 20% speedup. Your gut is unreliable.
- Stack Overflow 2025: two-thirds of devs spend more time fixing AI code than they save.
- Trust in AI accuracy dropped from 40% to 29% YoY.
- **The point:** the productivity gains only show up when you've internalized the practices above. Otherwise you get the slowdown without knowing it.

### Beat 6.4 (3 min) — The recommended stack slide
- One opinionated slide. Three columns: Individual, Startup, Enterprise.
- **Individual developer:**
  - IDE: Cursor Pro ($20/mo) OR Copilot Pro ($10/mo) for budget
  - Terminal: Claude Code Pro ($20/mo) OR Gemini CLI (free)
  - Cloud agent: experiment with Devin ACUs as needed
  - Markdown: AGENTS.md (with CLAUDE.md symlink)
  - MCP: GitHub, Filesystem, Postgres if relevant
- **Startup (5–20 devs):**
  - Same IDE/terminal stack, team plans
  - Add: CodeRabbit or Qodo on every PR
  - Add: Devin for backlog grooming and well-defined tickets
  - Governance: scoped MCP servers, basic audit logging
- **Enterprise:**
  - Same plus: Cursor Business or Copilot Business with SSO/audit
  - MCP gateway (Kong / Cloudflare portals)
  - Dedicated AI governance owner
  - On-prem option where data sensitivity requires (Qodo, Tabnine, Codacy)
- The line to say: "Pick one row. Start there. Don't try to deploy all of this in a month."

### Beat 6.5 (— part of 6.3/6.4 time) — Day 2 cliffhanger
- Bring back the SDLC grid from Block 2 — specifically the bottom row.
- "Most tools occupy one station. The bottom row occupies all seven."
- "We've covered everything else. Next week is about that one row — and the mental shift it forces."
- Don't mention the $9/hour figure (saving that for Day 2 opener per your call).
- "Bring questions. See you Monday."

**Visuals needed for Block 6:**
- Six principles slide (one per beat)
- Governance three-pillar diagram (access / audit / guardrails)
- Adult-honest caveats slide — sober, numbers, no decoration
- Recommended stack slide — three columns
- Final cliffhanger slide — the SDLC grid one more time, with the bottom row highlighted

---

# Summary of all visuals to build

For the implementing agent's reference, here's the complete visual inventory:

| # | Visual | Block | Type | Priority |
|---|---|---|---|---|
| V01 | Title slide | 1 | Static | Required |
| V02 | METR paradox slide (animated numbers) | 1 | Animated | Required |
| V03 | "What changed" three-pillar slide | 1 | Static | Required |
| V04 | Session roadmap (six blocks) | 1 | Static | Required |
| V05 | SDLC loop with seven stations (animated assembly) | 2 | Animated | **Signature** |
| V06 | The big grid (stations × tool categories) with animated fills | 2 | Animated | **Signature** |
| V07 | Block 2 stats reinforcement | 2 | Static | Required |
| V08 | Seniority spectrum (horizontal axis) | 3 | Static | Required |
| V09 | Category 1 (IDE tools) comparison matrix | 3 | Static | Required |
| V10 | Category 2 (terminal agents) comparison matrix | 3 | Static | Required |
| V11 | Category 3 (cloud autonomous engineers) — visually distinct | 3 | Static | **Signature** |
| V12 | Category 4 (code reviewers) comparison matrix | 3 | Static | Required |
| V13 | Category 5 (specialized) quick shelf | 3 | Static | Required |
| V14 | Live demo placeholder #1 (Cursor parallel agents) | 3 | Placeholder | Required |
| V15 | N×M → N+M animated diagram | 4 | Animated | **Signature** |
| V16 | LSP analogy diagram | 4 | Static | Required |
| V17 | MCP three-component architecture | 4 | Static | Required |
| V18 | MCP ecosystem state stats | 4 | Static | Required |
| V19 | Eight MCP servers visual shelf | 4 | Static | Required |
| V20 | Live demo placeholder #2 (Claude Code + GitHub MCP) | 4 | Placeholder | Required |
| V21 | Security incident timeline | 4 | Static | Required |
| V22 | Practical defenses checklist | 4 | Static | Required |
| V23 | Karpathy story slide (stars chart) | 5 | Static | Required |
| V24 | Three-layer markdown files stack (animated build) | 5 | Animated | **Signature** |
| V25 | Nine-section content checklist | 5 | Static | Required |
| V26 | Importance-score table (color-coded) | 5 | Static | Required |
| V27 | File-loading timing diagram | 5 | Static | Required |
| V28 | Live demo placeholder #3 (real CLAUDE.md walkthrough) | 5 | Placeholder | Required |
| V29 | Karpathy's four principles slide | 5 | Static | Required |
| V30 | Six principles slides (one per principle) | 6 | Static (6 slides) | Required |
| V31 | Governance three-pillar diagram | 6 | Static | Required |
| V32 | Adult-honest caveats slide | 6 | Static | Required |
| V33 | Recommended stack (three columns) | 6 | Static | Required |
| V34 | Final cliffhanger (SDLC grid, bottom row highlighted) | 6 | Static | Required |

**"Signature" visuals (5):** these are the ones worth spending extra polish on — they carry the most pedagogical weight. V05, V06, V11, V15, V24.
