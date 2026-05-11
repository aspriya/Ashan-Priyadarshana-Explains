# Build Prompt — Day 1 Interactive Lesson

**For:** Claude Code / Cursor / Devin / any coding agent
**Context to provide alongside this prompt:** `day1-research-report.md` and `day1-lesson-outline.md`

---

## Role and standing instructions

You are an implementing engineer building a single-file, self-contained, interactive HTML presentation for a 4-hour live lecture. The lecturer is Ashan — a senior engineer who teaches working developers in Sri Lanka. He will present from this file projected to a screen. The audience is paying for this session.

The deliverable must be a single `.html` file (with CSS and JS inlined) that opens cleanly in any modern browser, requires no build step, no internet connection during presentation, and no external dependencies beyond what can be inlined or pulled from a major CDN with sub-resource integrity. Fonts and icons may be loaded from a CDN if needed, but the file must degrade gracefully when offline.

You will work in **phases**, not all at once. Do not skip ahead. At the end of each phase, stop, summarize what you built, list the files you touched, and **wait for explicit user approval before starting the next phase.** If you are uncertain about a design or content decision, ask before assuming.

You have been given two reference documents — `day1-research-report.md` (the research and reasoning behind the session) and `day1-lesson-outline.md` (the beat-by-beat lesson plan with all 34 visuals enumerated). Treat the outline as the source of truth for content and ordering. Treat the report as the source of truth for facts, numbers, and reasoning.

---

## Hard constraints (apply across all phases)

1. **Single-file deliverable.** All CSS, JavaScript, and SVG inlined. Images, if any, base64-encoded. The file Ashan opens on the night is one `.html` file.
2. **Presentation-style.** This is *not* an interactive textbook. It is a slide deck with live animations. Each "slide" is a section the presenter advances through. Keyboard navigation (arrow keys, space) must work. Optional mouse/touch advancement is fine but secondary.
3. **Dark theme by default**, with a light-theme toggle. The dark theme should look good projected in a room with house lights at 50%. Use generous whitespace. Type at presentation scale — assume the audience is 20 feet from the screen.
4. **Text content is paraphrased, never reproduced verbatim from sources.** The research report cites specific blog posts, articles, and studies. You may use the facts and numbers. You may not copy phrasings. Especially: do not reproduce Karpathy's CLAUDE.md text verbatim — paraphrase the four principles per the outline. Same for any blog quotes the report references.
5. **No client analytics, no telemetry, no localStorage abuse.** Avoid storing state across sessions unless explicitly needed. The lecturer should be able to F5 the page and reset cleanly.
6. **Accessible by default.** Real headings (`<h1>`–`<h3>`), real lists, real semantic HTML. Decorative SVGs marked `aria-hidden`. Animations must respect `prefers-reduced-motion`.
7. **Per-slide structure.** Each slide is its own `<section>` with a stable ID. The slide title is always an `<h2>` so the presenter can quickly jump using a slide picker (Phase 5 feature).
8. **Code style:** vanilla JavaScript, no React, no build step. CSS uses CSS variables for theming. No Tailwind — write the CSS by hand and keep it tight (<2000 lines is the target).
9. **Animations:** SVG and CSS only. No external animation library. If you reach for GSAP or Lottie, stop and ask first.
10. **All numbers and facts must come from the research report.** If you find yourself writing a number that isn't in the report, stop and flag it as TODO rather than making one up.

---

## What "done" looks like across all phases

When all phases are complete, the final HTML file must:

- Have **34 slides** matching the visual inventory at the bottom of the lesson outline (V01–V34).
- Run on the lecturer's laptop with no internet connection.
- Take less than 3 seconds to load on a 5-year-old laptop.
- Survive an accidental F5 mid-presentation — start at slide 1, no error.
- Support arrow keys for navigation, "F" for fullscreen, "S" for slide picker, "T" for theme toggle, "?" for keyboard help.
- Include a presenter mode (press "P") that shows the lecturer's beat-level notes for the current slide in a side panel while the audience-facing view stays clean.
- Pass an `axe-core` accessibility audit at "no critical violations" level.

---

## Phase 1 — Scaffolding and navigation (no content yet)

**Goal:** build the skeleton everything else plugs into. End of this phase, the file is navigable with 34 empty slides as placeholders.

### Tasks
1. Create the single HTML file. Set up the document head with viewport meta, theme color, title ("AI Engineer 2.0 — Day 1").
2. Build the global CSS layer: CSS variables for color tokens (background, surface, text-primary, text-secondary, accent-primary, accent-warning, accent-danger, grid-line). Two theme variants — `data-theme="dark"` (default) and `data-theme="light"`.
3. Build the slide engine: one `<section class="slide" id="slide-N">` per slide, 34 total. Each section has placeholder `<h2>` with the visual ID and beat reference from the outline (e.g., "V05 — SDLC loop, Block 2 Beat 2.2").
4. Build the navigation controller in vanilla JS:
   - Arrow Right / Space / Page Down → next slide
   - Arrow Left / Page Up → previous slide
   - Home → first, End → last
   - "F" → toggle fullscreen
   - "T" → toggle theme
   - "?" → toggle keyboard help overlay
   - Track current slide in `window.location.hash` so F5 resumes at the right slide
5. Build the chrome:
   - Slide counter bottom-right (e.g., "5 / 34")
   - Progress bar across the top, animated on slide change
   - Minimal, unobtrusive
6. Build the keyboard help overlay (triggered by "?"). Lists all shortcuts.
7. Build a simple "fade + slide" transition between slides. Respect `prefers-reduced-motion`.
8. Add typography: a clean sans-serif system stack (no external font in this phase — Phase 6 can add a font if needed). Sizes scale by viewport: `h1: 4rem`, `h2: 3rem`, `body: 1.5rem` on a 1080p projector.

### Acceptance criteria for Phase 1
- All 34 placeholder slides exist and are navigable.
- Theme toggle works.
- Fullscreen works.
- Hash-based resume works.
- Reduced-motion honored.
- File is < 800 lines of HTML+CSS+JS (it will grow in later phases).

### Stop point
Stop after Phase 1. Report what was built. **Do not begin Phase 2 until the user approves.**

---

## Phase 2 — Static content slides (Blocks 1, 6, and the simpler slides of 3 and 4)

**Goal:** fill in all the slides that are pure typography and layout — no custom diagrams or animations yet.

### Slides to populate in Phase 2

From the lesson outline, populate the *content* of these slides. Use the beat-by-beat narrative from the outline as the authoritative source for what each slide says.

- **V01** Title slide
- **V02** METR paradox (static layout; animated number reveal comes in Phase 4)
- **V03** What changed — three-pillar slide
- **V04** Session roadmap — six numbered blocks
- **V07** Block 2 stats reinforcement
- **V08** Seniority spectrum (static layout; the axis visual comes in Phase 4)
- **V09–V13** Tool category matrices (Categories 1–5) — these can be done as styled HTML tables in this phase
- **V14, V20, V28** Live demo placeholder slides — clean "Live Demo #N" framing with what's about to be shown
- **V16** LSP analogy — static text/diagram in this phase
- **V18** MCP ecosystem state stats
- **V19** Eight MCP servers visual shelf
- **V21** Security incident timeline
- **V22** Practical defenses checklist
- **V23** Karpathy story (static text; the stars-chart visual comes in Phase 4)
- **V25** Nine-section content checklist
- **V26** Importance-score table (color-coded)
- **V27** File-loading timing diagram (static this phase; animated in Phase 4 if time allows)
- **V29** Karpathy's four principles
- **V30** Six principles (six slides, one per principle)
- **V31** Governance three-pillar diagram
- **V32** Adult-honest caveats slide
- **V33** Recommended stack — three columns
- **V34** Final cliffhanger

### Content rules for Phase 2
- Pull narrative from the outline's beat descriptions. Paraphrase where the outline uses phrasing close to the report.
- Each slide should have **at most ~30 words of body text**, rendered large. If something needs more, it belongs in presenter notes, not on the slide.
- Use icons sparingly. Lucide-style line icons inlined as SVG are fine.
- The recommended-stack slide (V33) is opinionated by design — keep it that way.
- The caveats slide (V32) must be visually sober. Black/very-dark background regardless of theme. No decorative flourishes. The numbers do the work.

### Acceptance criteria for Phase 2
- Every slide listed above has its real content.
- Numbers are pulled from the research report only — no invented stats.
- No verbatim quotes from any blog post or article cited in the report.
- File is still < 2500 lines total.

### Stop point
Stop after Phase 2. Report what was built. **Wait for user approval.**

---

## Phase 3 — The signature visuals (the five that carry the lesson)

**Goal:** build the five "signature" visuals identified in the outline. These are the ones that carry the most pedagogical weight and need to be polished.

### Visuals to build in Phase 3

**V05 — SDLC loop with seven stations (animated assembly)**
- SVG of a circular loop with seven labeled stations: Plan → Design → Implement → Review → Test → Ship → Operate → (back to Plan).
- On slide enter, stations appear one by one with a 200ms stagger. Connecting arcs draw progressively.
- The "Operate → Plan" feedback arrow is visually emphasized (dashed line, different color) to make the loop nature obvious.
- Each station has an icon. Keep icons consistent in style.

**V06 — The money grid (stations × tool categories) with animated fills**
- The X-axis is the seven SDLC stations from V05.
- The Y-axis is five tool category rows: "IDE-bound", "Terminal agents", "Dedicated reviewers", "Cloud autonomous engineers", "Specialized".
- Grid cells start empty.
- On slide enter, fills animate in this exact order with pauses between (controlled by arrow-key advancement or auto-step on entry):
  1. IDE-bound row fills cells under "Implement" (full), "Design" (partial), "Review" (partial). Pause.
  2. Terminal agents row fills cells under "Implement", "Review", "Test", and "Ship" (partial). Pause.
  3. Dedicated reviewers row fills one tall column under "Review". Pause.
  4. **Cloud autonomous engineers row fills a horizontal bar across all seven stations.** This is the punchline — make it visually emphatic (brighter color, slight glow, a 600ms reveal).
  5. Specialized row remains empty or shows a few sparse cells.
- Use sub-step navigation: pressing space inside this slide advances the animation step-by-step (not the whole slide at once).

**V11 — Cloud autonomous engineers row, visually distinct**
- This is the standalone follow-up slide that shows the bottom row alone, larger, with tool logos/names placed on it: Devin, Jules, Codex Cloud, GitHub Coding Agent, Cursor Cloud Agents, Replit Agent.
- The horizontal bar from V06 is the visual motif — keep continuity.

**V15 — N×M → N+M animated diagram**
- Left side: 6 tool nodes (Cursor, Claude Code, Devin, Copilot, Windsurf, Gemini CLI).
- Right side: 6 system nodes (GitHub, Postgres, Slack, Sentry, Linear, Filesystem).
- Animation step 1: draw all-to-all connections (36 lines). Visually chaotic — that's the point.
- Animation step 2: lines fade out, a central "MCP" node appears.
- Animation step 3: tools connect to MCP (6 lines), systems connect to MCP (6 lines). 12 total. Calm.
- Caption: "N × M → N + M".

**V24 — Three-layer markdown files stack (animated build)**
- A stacked-layer diagram. Layer 3 (bottom) appears first: project structure files (README, ARCHITECTURE, package.json, tsconfig). Layer 2 in middle: capability extensions (SKILL.md, slash commands, hooks, subagents). Layer 1 on top: project context (AGENTS.md, CLAUDE.md, GEMINI.md, .cursorrules).
- Build animation: layers appear bottom-to-top with labels fading in.
- Hover or sub-step navigation reveals which AI tool reads which file.

### Acceptance criteria for Phase 3
- All five signature visuals work end-to-end.
- Sub-step navigation within multi-step slides (V05, V06, V15, V24) works without breaking global slide navigation.
- Animations respect `prefers-reduced-motion`.
- SVGs are inlined, not external.
- All five look polished at 1920×1080 projector resolution.

### Stop point
Stop after Phase 3. Report what was built. **Wait for user approval.**

---

## Phase 4 — The remaining animations and polish visuals

**Goal:** finish the slides that need light animation but aren't "signature" — the supporting visuals.

### Visuals to complete in Phase 4

- **V02** METR paradox — animate the three numbers (24% predicted, 20% felt, -19% actual) in sequence with a beat-pause between each. The -19% should land with visual emphasis (color shift to a warning red).
- **V08** Seniority spectrum — animate the horizontal axis filling left-to-right with tool placements popping in at their positions.
- **V17** MCP three-component architecture — clean SVG of Host + Client + Server with transport arrows (stdio, Streamable HTTP) labeled.
- **V23** Karpathy story — a simple line chart showing GitHub stars over three months (7.9K on day 1 → 110K by month three). Animated growth.
- **V27** File-loading timing diagram — a horizontal timeline showing which files enter context when (project rules always-on, SKILL.md on-demand, hooks event-triggered, subagent-isolated).

### Acceptance criteria for Phase 4
- All five animations work and feel intentional, not jittery.
- Total file size still reasonable (<400KB for the HTML file).
- No animation longer than 2 seconds — these are presentation aids, not feature films.

### Stop point
Stop after Phase 4. Report what was built. **Wait for user approval.**

---

## Phase 5 — Presenter features

**Goal:** add the tools Ashan needs to present smoothly on the night.

### Features to build

1. **Slide picker overlay** ("S" key): a grid view showing thumbnails (or just titles) of all 34 slides. Click or arrow-key + Enter to jump to any slide. Escape to dismiss.
2. **Presenter notes panel** ("P" key): a side panel showing the beat-level talking points for the current slide. Pull the notes from a JSON block embedded in the HTML — one entry per slide ID. The audience-facing view stays clean; only the lecturer's screen shows the notes (use the Presentation API or simply a toggle).
3. **Slide timer**: a small unobtrusive timer in the corner showing "time on current slide" and "total elapsed". Useful for staying on the 4-hour budget. Toggleable with "M".
4. **Block boundary markers**: visual indicator (a different progress bar color, or a small block-number indicator) showing which of the 6 blocks the current slide belongs to.
5. **"Demo mode"** for V14, V20, V28: when these slides are reached, the page shows a clean "Live Demo — [topic]" splash with a checklist of what's about to be shown. The lecturer alt-tabs to the actual demo (Cursor, Claude Code, etc.).
6. **Restart confirmation**: if the lecturer presses Home mid-presentation, a small confirmation toast appears ("Restart from slide 1? Y/N") so a fat-finger doesn't lose their place.

### Acceptance criteria for Phase 5
- Slide picker works with keyboard and mouse.
- Presenter notes load correctly for all 34 slides (even if notes are stubs in this phase).
- Timer is accurate.
- No feature gets in the way of the audience-facing view.

### Stop point
Stop after Phase 5. Report what was built. **Wait for user approval.**

---

## Phase 6 — Polish, accessibility audit, final pass

**Goal:** ship-ready quality.

### Tasks

1. Run `axe-core` (or equivalent) against the file. Fix all critical violations.
2. Test on Chrome, Firefox, Safari. Note any rendering differences.
3. Verify offline operation — open with Wi-Fi disabled.
4. Verify F5 mid-presentation resumes at the correct slide.
5. Verify `prefers-reduced-motion` is honored — every animation has a reduced-motion fallback (instant state change).
6. Test on a 1080p external display. Adjust any type or layout that doesn't read well at distance.
7. Optional: add a system font with good readability (Inter, Geist, or system stack — no need to bundle if not needed).
8. Add a print stylesheet — useful if the lecturer wants a hardcopy backup of the slides.
9. Inline a favicon (base64).
10. Final review of every slide against the lesson outline — any drift?
11. Final review of every fact and number against the research report — any drift?

### Acceptance criteria for Phase 6
- Zero critical axe-core violations.
- Works offline.
- Works on Chrome, Firefox, Safari.
- Print stylesheet produces something usable.
- Lecturer can present from this file alone, no other resources needed.

### Stop point
Done. Hand off the file with a 1-page README explaining keyboard shortcuts and the presenter mode.

---

## Things to ask the user about (not assume)

Stop and ask if you encounter:

- A fact in the report that seems contradicted by something you find. Flag, don't override.
- A visual that you think would land better as a different layout than what the outline specifies. Propose, don't substitute.
- A slide where the beat in the outline runs short or long for the time budget. Surface for the lecturer's decision.
- Any temptation to add features beyond this prompt. Don't. Ship the scope as written. The lecturer can iterate after the first run.

---

## What the lecturer is going to do with this file

To set expectations: Ashan will open this file in Chrome, full-screen, projected to a screen at the front of a room. He has a clicker. The audience is 30-50 working developers and engineering leads. He'll talk for 4 hours. He has done this before — he knows how to present.

What he needs from this file is: **a tight, polished, audience-respecting visual companion to a talk he's going to give from memory.** Not a textbook. Not a tutorial. A presentation.

When in doubt, make it cleaner, less busy, and trust the lecturer to do the talking.

---

## Begin

Acknowledge this prompt, ask any clarifying questions you have *before* starting, and once cleared, begin **Phase 1 only**. Stop at the end of Phase 1 and report.
