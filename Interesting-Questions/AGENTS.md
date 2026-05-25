# AGENTS.md — Building and Extending the Interactive Algorithm Slides

This file tells a coding agent (Devin, Claude Code, Cursor, Copilot, or any equivalent) two things:

1. **How to implement** the slide deck described in `PLAN.md`.
2. **How to generate new problems** that fit the deck's pedagogical style, so the deck keeps growing.

Read both sections before starting work. They are equally load-bearing.

---

## Part 1 — How to implement the deck

### Project shape

- **One file:** `slides.html`. Self-contained. No build step. No npm install. Opens directly in a browser.
- **External dependencies allowed only via CDN:** Google Fonts (Fraunces, Space Grotesk, JetBrains Mono). No JS libraries unless absolutely necessary — and if added, justify the choice in a code comment.
- **No Tailwind, no React, no bundlers.** Plain HTML, plain CSS (with custom properties), plain JavaScript (ES2020+).
- **No DOCTYPE-less fragments.** The file is a complete, valid HTML5 document.

### File structure inside `slides.html`

Organize the file in this order, top to bottom:

1. `<!DOCTYPE html>`, `<html>`, `<head>` with metadata, font links, and a single `<style>` block.
2. `<body>` containing:
   - A header with the deck title and progress indicator.
   - The slide stage: a single `<main id="stage">` element that the navigation engine writes into.
   - The full set of `<template id="scene-N">` elements — one template per scene, each containing the slide HTML for that scene.
   - A navigation bar with prev/next buttons and a scene jumper.
   - An overview grid (`<dialog id="overview">`).
   - A speaker-notes panel (`<aside id="notes">`).
3. A single `<script>` block at the end with the navigation engine.

Why templates? It keeps each scene's HTML grouped and inert until activated. It also makes the "one place to add a scene" promise from `PLAN.md` enforceable — agents drop in a new `<template>` and the engine picks it up.

### The navigation engine (contract)

Implement these behaviors. Tests are conceptual — verify by hand.

| Trigger                  | Behavior                                                                    |
| ------------------------ | --------------------------------------------------------------------------- |
| Right arrow / Page Down  | Advance one slide; cross scene boundaries naturally.                        |
| Left arrow / Page Up     | Reverse one slide.                                                          |
| `Home` / `End`           | Jump to first / last slide of the deck.                                     |
| `Esc`                    | Toggle overview grid (modal `<dialog>`).                                    |
| `N`                      | Toggle speaker notes panel.                                                 |
| URL hash `#sN/mM`        | Load scene N, slide M on page load and after every navigation.              |
| Click scene tile in grid | Navigate to that scene's first slide, close grid.                           |
| Click prev/next button   | Same as arrow keys.                                                         |

Scenes are discovered by querying `document.querySelectorAll('template[id^="scene-"]')`. The engine must not contain a hard-coded list of scene IDs.

### Design system (must follow)

- **Colors** are CSS custom properties on `:root`. Define ramps for: purple, teal, coral, amber, gray. Stops: `50, 100, 400, 600, 800`. Example: `--purple-600: #534AB7;`.
- **Semantic color roles:** purple for "insight" callouts, teal for "data structure" highlights, coral for "naive/bad" framing, amber for "live state during animation," gray for structural and neutral content.
- **Fonts:**
  - `--font-display: 'Fraunces', serif;` for slide titles and large numbers.
  - `--font-body: 'Space Grotesk', sans-serif;` for body text.
  - `--font-mono: 'JetBrains Mono', monospace;` for code and complexity notation.
- **Type scale:**
  - Slide title: 44px, Fraunces, weight 500.
  - Section heading inside a slide: 24px, Space Grotesk, weight 500.
  - Body: 19px, Space Grotesk, weight 400, line-height 1.6.
  - Code/complexity: 16px, JetBrains Mono.
- **Sentence case everywhere.** No Title Case headings. No ALL CAPS.
- **Spacing:** content max-width 1100px, centered. Slide padding 64px top/bottom, 48px sides.
- **Radii:** `--radius-md: 10px`, `--radius-lg: 16px`. Use `lg` for cards and large visualizations.
- **Animations:** all CSS animations wrapped in `@media (prefers-reduced-motion: no-preference) { ... }`. Default state must be the *end* of the animation, so reduced-motion users see the final visualization, not a blank frame.

### Slide HTML conventions

Each scene template looks like this:

```html
<template id="scene-1">
  <article class="scene" data-scene-title="Bucket-count and print">
    <section class="slide slide-problem" data-notes="One-sentence speaker hint.">
      <h1>Slide title in sentence case</h1>
      <!-- content -->
    </section>
    <section class="slide slide-naive" data-notes="...">...</section>
    <section class="slide slide-insight" data-notes="...">...</section>
    <section class="slide slide-walkthrough" data-notes="...">...</section>
  </article>
</template>
```

Class naming:

- `.slide` is the base class — applies padding, layout, transitions.
- `.slide-problem`, `.slide-naive`, `.slide-insight`, `.slide-walkthrough`, `.slide-followup` are *role* classes used for subtle styling (e.g. accent border color matching the semantic palette).
- Inside slides, use `.callout`, `.code`, `.viz`, `.complexity` for the major content blocks.

### Visualization conventions

- **Use inline SVG** as the default for diagrams. Set `viewBox` and `width="100%"` so the SVG scales with its container.
- **For step-through algorithm animations**, prefer SVG with JS-driven state updates over CSS keyframes. The learner controls progress; CSS keyframes are for ambient motion only.
- **Color shapes via the CSS custom properties**, not hardcoded hex. This means `fill="var(--teal-100)"`. SVG accepts CSS variables in attribute values in all modern browsers.
- **Label everything.** Every visualization has a 1-line caption underneath in `.viz-caption` (14px gray-600). The caption restates the visual's purpose in plain English — what the viewer should take away.
- **No emoji as visual elements.** Use SVG, CSS shapes, or no decoration at all. (Emoji are okay in speaker notes for the instructor's eyes only.)

### Complexity annotations (mandatory)

Every algorithmic claim must show its complexity in `JetBrains Mono` near the relevant code or visualization:

```
Time: O(n + k)    Space: O(k)
```

Where:
- `n` is the input size.
- `k` is the bounded range (or other relevant secondary parameter — define it inline if not obvious).
- Both time and space must be present. If space is `O(1)`, say so explicitly; don't omit it.

If the problem has a trade-off (e.g. "O(n) extra space for O(1) query"), show both bounds and a one-sentence note explaining the trade.

### What to avoid

- **No frameworks.** No React, Vue, Svelte, Alpine. The whole point is portability and zero-install.
- **No mid-slide auto-advancement.** The user controls the pace.
- **No infinite spinners or loading states.** Everything is local; if something appears to load, you've added a dependency that shouldn't be there.
- **No external state.** No localStorage, no cookies, no analytics. URL hash only.
- **No alerts, no `confirm()` dialogs.** Use the speaker notes panel or inline callouts instead.

---

## Part 2 — How to generate new problems for the deck

This section is for the request: *"Add three more scenes to the deck."* The agent's job is to invent new problems that fit the established style, then implement them as scenes.

### The "easy once you get it" criteria

A problem qualifies for this deck only if it meets **all four** criteria:

1. **The naive solution is obvious and clearly suboptimal.** A learner can come up with the naive approach in under a minute. Its complexity is visibly wasteful (O(n²) where O(n) is possible, O(n) space where O(1) is possible, etc.).
2. **The optimal solution hinges on one specific insight.** Not a clever trick stacked on another clever trick. One leap. The insight should be nameable in a single sentence.
3. **The insight teaches a transferable concept.** A specific data structure (hash map, counting array, two pointers, prefix sums, bit manipulation, monotonic stack/queue, set, sliding window) or a programming pattern (canonicalization, two passes, math-instead-of-iteration, insertion-vs-query trade-off, in-place modification, divide-and-conquer).
4. **The problem is language-agnostic.** It can be expressed and solved in Java, Python, C++, JavaScript, Go, Rust without leaning on language-specific features. Mention language tradeoffs in speaker notes only.

If a candidate problem fails any of these, reject it. Suggest a replacement rather than weakening the deck.

### Concept coverage matrix

When adding new problems, aim for diversity across concepts. Track what's already covered and prefer adding problems that introduce *new* concepts to the deck.

| Concept                          | Example problem already in deck    | Covered? |
| -------------------------------- | ---------------------------------- | -------- |
| Counting array / bucketing       | Bucket-count and print             | ✅       |
| Two passes (count then scan)     | First non-repeating character      | ✅       |
| Math beats iteration             | Find the missing number            | ✅       |
| Insertion-time vs query-time     | Most frequent in a stream          | ✅       |
| Canonicalization / hashing       | Group anagrams                     | ✅       |
| Two pointers (slow/fast)         | Floyd's cycle detection            | ✅       |
| Prefix sums                      | —                                  | Open     |
| Sliding window                   | —                                  | Open     |
| Monotonic stack / queue          | —                                  | Open     |
| Bit manipulation (XOR)           | —                                  | Open     |
| Binary search on answer space    | —                                  | Open     |
| Hash set for O(1) lookup         | —                                  | Open     |
| Greedy with sorting              | —                                  | Open     |
| In-place modification            | —                                  | Open     |

When generating new problems, **pick from the "Open" rows first**.

### Example "Open" problems to draw from

These are example problems that fit the deck's criteria. They are seeds — invent variations or replacements as needed.

1. **Maximum sum of a contiguous subarray of size k** (sliding window). Naive: nested loop, `O(n*k)`. Insight: slide the window, add the new element, drop the old. `O(n)` time, `O(1)` space.
2. **Two-sum** (hash set). Naive: check every pair, `O(n²)`. Insight: for each element, ask "have I seen target − this?" via a hash set. `O(n)` time, `O(n)` space.
3. **Find the only number that appears once when all others appear twice** (XOR). Naive: hash map of counts, `O(n)` space. Insight: XOR all elements; pairs cancel, the lone number remains. `O(n)` time, `O(1)` space.
4. **Largest rectangle in a histogram** (monotonic stack). Naive: try every left-right pair, `O(n²)`. Insight: a stack of increasing heights gives each bar's left/right boundary in amortized `O(n)`.
5. **Range sum queries on a static array** (prefix sums). Naive: sum the range on every query, `O(n)` per query. Insight: precompute prefix sums once; every query becomes `prefix[r+1] - prefix[l]`. `O(1)` per query after `O(n)` preprocessing.
6. **Find the smallest divisor such that the sum of ceilings is below a threshold** (binary search on answer space). Naive: try every divisor, `O(max_val × n)`. Insight: the predicate "is divisor d good enough?" is monotonic in d, so binary-search d. `O(n log max_val)`.
7. **Move all zeros to the end of an array** (in-place two pointers). Naive: filter then refill, `O(n)` extra space. Insight: a "write pointer" and a "read pointer" — copy non-zeros forward, then zero-fill the tail. `O(1)` extra space.

When asked for new problems, propose **5 candidates with a one-sentence pitch and the insight, the data structure, and the complexity**, and let the user pick which to flesh out into full scenes. Don't implement five scenes unprompted.

### How to produce a scene from a problem

When fleshing out a problem into a scene, follow this checklist:

1. **Write the problem statement** as a short paragraph with a small concrete example. The example must be tiny enough that a human can mentally walk through it in 30 seconds.
2. **Draft the naive solution in pseudocode.** Show its complexity. Explain *why* it's wasteful in one sentence.
3. **State the insight in one sentence.** This is the single most important sentence in the scene.
4. **Sketch the optimal solution in pseudocode.** Show its complexity. The complexity reduction must be clearly visible (e.g., "O(n²) → O(n)").
5. **Design the insight visualization.** This is the SVG that goes on slide 3. It should literally *show* the data structure being used, with state. For counting array: show the buckets. For hash set: show the set's contents growing. For two pointers: show both pointers on the same input.
6. **Design the walkthrough animation.** Slide 4 should let the user step through the algorithm running on the example input. State updates visibly on each step.
7. **Write speaker notes** for each slide — one to two sentences each, written for the instructor's eyes only. The notes should give the *exact phrase* the instructor should reach for if blanking.
8. **Verify the four criteria** are met before committing.

### Style of language for slides

- **Sentences are short.** Aim for 14 words or fewer in body text.
- **Code is annotated with intent, not narration.** A comment like `// counts[v]++ does both lookup and increment in one op` is good. `// increment counts at index v` is noise.
- **Complexity is stated, not buried.** Every claim of "this is faster" carries the big-O immediately.
- **The naive approach is treated with respect.** It's the natural first thought; don't mock it. The point of the scene is the *journey* from naive to optimal, not "look how dumb the obvious answer is."

### Workflow for the agent

When asked to generate and add new problems, follow this loop:

1. **Propose.** List 5 candidate problems (using the Open concepts matrix above as the priority list). For each, give: problem name, one-sentence pitch, naive complexity, optimal complexity, insight in one sentence, data structure or concept demonstrated.
2. **Confirm.** Wait for the user to pick which candidates to implement. Do not implement unprompted.
3. **Flesh out.** For each chosen problem, complete the scene-production checklist above. Show the draft scene HTML to the user before committing it to `slides.html`.
4. **Integrate.** Add the new `<template id="scene-N">` to `slides.html`. Verify the navigation engine picks it up. Update the concept coverage matrix in this file (`AGENTS.md`).
5. **Manual test.** Open `slides.html` in a browser. Navigate to the new scene via keyboard, mouse, and URL hash. Confirm all four (or five) slides render correctly, the visualization works, and speaker notes show under `N`.

### What "done" looks like for a new scene

A new scene is complete when:

- It has 3–5 slides following the problem / naive / insight / walkthrough structure.
- Every slide's complexity claim is annotated in big-O notation in monospace.
- The insight slide has a custom SVG visualization (not a generic placeholder).
- The walkthrough slide is interactive — a button steps through the algorithm and updates state.
- Speaker notes exist on every slide.
- The scene's concept is added to the coverage matrix in this file.
- Opening `slides.html` and navigating to the new scene via the hash URL works on the first try.

---

## Quick reference card

A condensed checklist for the agent to keep handy.

```
ON IMPLEMENTING:
  - One file: slides.html. No build, no npm.
  - Discover scenes via DOM, not hardcoded lists.
  - Fonts: Fraunces (display), Space Grotesk (body), JetBrains Mono (code).
  - Every algorithm claim shows time AND space complexity.
  - Animations honor prefers-reduced-motion.
  - URL hash routing: #sN/mM.

ON GENERATING PROBLEMS:
  - Must meet all 4 criteria: obvious naive, single insight, transferable concept, language-agnostic.
  - Propose 5 candidates; wait for the user to pick.
  - Prefer Open rows in the coverage matrix.
  - Update the matrix after adding.

ON STYLE:
  - Sentence case everywhere.
  - Sentences ≤ 14 words in body.
  - Treat the naive solution with respect.
  - Code comments state intent, not narration.
```
