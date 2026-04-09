# Project Brief: Week 4 Interactive Lesson — The Language of Vectors

## What We're Building

A single-file self-contained interactive HTML lesson for Week 4 of an online lecture series on Core AI Principles & Agentic App Development, run in partnership with eLearning.lk.

This is a full-screen slide-by-slide interactive web page — not a PowerPoint. It looks and navigates like a presentation but is built with HTML/CSS/JS and uses live animations, interactive diagrams, and explorable widgets so both educator and students can engage deeply with the material.

The file must be:

- A single `.html` file, fully self-contained (no external dependencies except Google Fonts and cdnjs-hosted Chart.js)
- Responsive — works on desktop for the educator and on mobile for students
- Navigable by keyboard arrow keys AND Prev/Next buttons
- Visually polished with a dark tech aesthetic matching the Week 3 style

---

## The 8-Week Course Structure

| Week | Title | Status |
|------|-------|--------|
| 1 | The Genesis of Intelligence | ✅ |
| 2 | The Digital Neuron | ✅ |
| 3 | The Deep Learning Balance | ✅ |
| **4** | **The Language of Vectors** | **← build this now** |
| 5 | The Final Choice | |
| 6 | The Rise of the Agents | |
| 7 | The Modular Architect | |
| 8 | The Orchestration Symphony | |

---

## Week 4 Topic & Key Takeaway

**Title:** "The Language of Vectors"

**Key Takeaway:** How Embeddings and the Attention Mechanism translate human language into a mathematical space where context and meaning are preserved — and why this is the complete foundation of every LLM.

---

## Design System (identical to Week 3)

**Aesthetic:** Dark navy tech. Sharp teal accent. Monospace data feel mixed with serif display type.

### Fonts (Google Fonts)

- **Display/titles:** Fraunces (serif, italic for emphasis)
- **Body/UI:** Space Grotesk
- **Code/data:** JetBrains Mono

### Colors

```css
--navy: #0D1B2A
--navy2: #1A2B3C
--navy3: #243447
--teal: #00D4AA
--teal2: #00A882
--blue: #4C9BE8
--purple: #8B5CF6
--amber: #F59E0B
--red: #EF4444
--orange: #F97316
--green: #10B981
--white: #F0F4F8
--muted: #64748B
--card: rgba(255,255,255,0.04)
--border: rgba(255,255,255,0.08)
```

### Libraries (cdnjs only)

- **Chart.js 4.4.0:** `https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.0/chart.umd.min.js`

---

## Slide System

- Each slide: `position:absolute; inset:0` — full viewport
- Transitions: opacity + translateX, 0.5s cubic-bezier
- Fixed bottom nav bar (64px): dots + slide label + Prev/Next buttons
- Fixed top progress bar (3px gradient teal→blue)
- Keyboard: ArrowLeft/Right
- `onSlideEnter(idx)` hook — lazy-init interactives

### Layout per slide

```
┌──────────────────────────────┐
│ section tag · slide title    │
│ subtitle (muted)             │
├──────────────────────────────┤
│                              │
│   INTERACTIVE CONTENT AREA   │
│                              │
└──────────────────────────────┘
[progress bar top · nav bar bottom]
```

**Responsive:** At ≤768px, stack layouts vertically, 44px touch targets, hide decorative elements.

---

## Full Slide Plan — 17 Slides

### Slide 0 — Title

Dark navy. Animated canvas: floating vector dots connected by faint lines (simulate a high-dimensional space projected to 2D). Title: "The Language of Vectors". Week 04 badge. Topic pills: Tokenization · Embeddings · Attention · Transformers · KV Cache · Context Window.

---

### Slide 1 — Why Language is Hard for Machines

**Interactive:** The encoding problem — three approaches with live comparison

Three toggle buttons: **One-Hot** | **Integer** | **Embeddings**

- **One-Hot:** Render a vocabulary grid (~12 words). Clicking a word lights up its one-hot vector as a row of cells (mostly grey zeros, one teal 1). Show the similarity score between "cat" and "kitten" = 0.00. Show between "cat" and "airplane" = 0.00. Point: zero similarity information.
- **Integer Encoding:** Show words mapped to integers. "cat=2, kitten=3, airplane=847". Show the problem — integer distance implies false proximity. "cat" and "kitten" (2 and 3) look closer than "cat" and "feline" (2 and 156) even though feline is semantically closer.
- **Embeddings:** Show the same words as short dense vectors with real values. Show cosine similarity: "cat" vs "kitten" = 0.89, "cat" vs "airplane" = 0.12. The encoding captures meaning.

**Sidebar:** live cosine similarity display that updates as you switch encoding methods and click word pairs.

---

### Slide 2 — Tokenization: What the Model Actually Sees

**Interactive:** Live tokenizer

**Key insight:** The model never sees words. It sees tokens. Tokens are subword units — not characters, not full words.

**Interactive text box:** student types any text (or uses presets). Display:

- The text split into colored token chips (each token a different color)
- Token count and character count
- Token IDs shown below each chip

**Preset examples** to demonstrate key surprises:

- `"Hello world"` → 2 tokens (as expected)
- `"unbelievable"` → 3 tokens: `un` · `believ` · `able`
- `"GPT-4"` → 4 tokens: `G` · `PT` · `-` · `4`
- `"👍"` → 3 tokens (emoji are expensive!)
- `"aaaaaaaaaa"` → fewer tokens than characters
- `"The quick brown fox"` → show how common phrases tokenize cleanly

Show a **token budget bar:** "This sentence uses X / 4096 tokens of your context window."

Explain BPE (Byte Pair Encoding) in one card: "Tokenization is learned from a corpus. Frequent sequences get merged into single tokens. Rare words get split into known subword pieces."

---

### Slide 3 — What is an Embedding?

**Interactive:** 2D embedding space explorer

A Chart.js scatter plot showing ~25 words projected into 2D space, colored by semantic category:

- 🟢 **Animals:** cat, dog, fish, bird, wolf
- 🔵 **Royalty:** king, queen, prince, princess, crown
- 🟣 **Tech:** computer, laptop, software, data, network
- 🟡 **Food:** pizza, sushi, bread, rice, soup

**Two modes** (toggle button):

- **Random (untrained):** Points scattered randomly across the space
- **Trained:** Points cluster by category, similar words are near each other

**Clicking any word:**

- Highlights it with a ring
- Shows its nearest 3 neighbors with cosine similarity scores in a sidebar
- Shows its 2D coordinates as a vector

**Bottom card:** "An embedding is a learned, dense, real-valued vector. Position in this space = meaning. Distance in this space = semantic similarity."

---

### Slide 4 — Vector Arithmetic & King–Queen

**Interactive:** Vector arithmetic visualizer

Canvas showing labeled 2D arrows. The classic: **king − man + woman ≈ queen**

Animate this as three arrow additions:

1. Start at origin, draw arrow to **king**
2. Subtract **man** vector (draw arrow in opposite direction)
3. Add **woman** vector (draw arrow forward)
4. Land near **queen** — show the actual queen vector nearby, highlight the approximation

**Four preset analogies** student can click through — each animates the same way:

- `king − man + woman = queen`
- `Paris − France + Italy = Rome`
- `walked − walk + run = ran`
- `bigger − big + small = smaller`

Show the formula panel updating for each. Show the residual distance ("approximate match: 94%").

---

### Slide 5 — The Context Problem: Why Word-by-Word Fails

**Interactive:** Ambiguity resolver

Show the word **"bank"** in two sentences. Student clicks each sentence to see the word embedding it would get:

- *"I deposited money at the bank"* → finance vector (near: money, deposit, loan)
- *"The fish swam near the river bank"* → geography vector (near: river, shore, water)

**Without context:** both get identical embeddings. **With attention:** they diverge.

Also show: *"The animal didn't cross the street because it was too tired"* — what does "it" refer to? A grid showing word-to-word attention scores lights up: "it" → "animal" gets a high score.

**Bottom callout:** "We need a mechanism that reads the entire sentence before deciding what each word means. That mechanism is Attention."

---

### Slide 6 — The Attention Mechanism — Intuition

**Interactive:** Attention weight heatmap

**Sentence:** "The animal didn't cross the street because it was too tired"

Two-panel layout:

- **Left:** clickable word list (the query words)
- **Right:** attention heatmap grid — rows = query words, columns = key words, cell color = attention weight

**Clicking any word on the left:**

- Highlights that row in the heatmap
- Shows which words it attends to strongly
- Updates an explanation panel: e.g., clicking "it" shows: "This token attends strongly to 'animal' (0.72) — this is how the model resolves the pronoun reference"

**Attention Temperature slider** (0.1 → 5.0):

- **Low temperature:** attention is sharp/peaked (one dominant word)
- **High temperature:** attention is diffuse/flat (uniform across all words)
- Watch the heatmap update live as student drags

This is the key intuition-builder: the model "looks at" different parts of the sentence differently for each word.

---

### Slide 7 — Attention: Q, K, V — The Math

**Interactive:** Step-by-step Q/K/V walkthrough

Use a 3-token example: `["cat", "sat", "mat"]` with small toy vectors (d=4).

**Formula:** `Attention(Q,K,V) = softmax(QK^T / √d_k) · V`

Four clickable steps — clicking each step animates a transition and updates the visual:

1. **Step 1 — Input embeddings → Q, K, V matrices**
   - Show: input embedding × W_Q = Q, × W_K = K, × W_V = V
   - Visual: three small matrices side by side, each value shown as a colored cell

2. **Step 2 — Dot products: QK^T**
   - Show: Q × K^T produces a 3×3 score matrix
   - Each cell = "how much does token i attend to token j?"
   - Values shown as colored cells (warm = high attention)

3. **Step 3 — Scale by √d_k, then Softmax**
   - Show the raw scores → divided by √4=2 → softmax turns them into probabilities
   - Show WHY we scale: "Without √d_k scaling, large d_k causes extreme dot products → softmax saturates → vanishing gradients"
   - Animate the transition from raw scores to probabilities

4. **Step 4 — Multiply by V**
   - Show: attention weights × V matrix = final output
   - Each output token is a weighted combination of Value vectors
   - Plain English: "The output for 'cat' is: 70% of V[cat] + 20% of V[sat] + 10% of V[mat]"

Progress indicator showing which step is active. "Next Step" button to advance.

---

### Slide 8 — Multi-Head Attention

**Interactive:** Parallel attention heads

Show the same sentence processed by 4 attention heads simultaneously.

4 head buttons. Clicking each reveals that head's attention heatmap (a smaller version of Slide 6's heatmap) with a label:

- **Head 1:** "Syntactic structure" — subject-verb-object relationships light up
- **Head 2:** "Coreference" — pronouns strongly attend to their antecedents
- **Head 3:** "Positional proximity" — words mostly attend to their immediate neighbors
- **Head 4:** "Semantic similarity" — words attend to semantically related words regardless of position

**Below:** show the architecture: 4 heads → concat → linear projection → output. Show that `d_model = num_heads × d_k` (the dimensions are split, not duplicated).

**Key insight card:** "Each head asks a different question. Together they capture a richer, multi-dimensional understanding than any single attention pattern could."

---

### Slide 9 — Layer Stacking & Why Depth Matters

**Interactive:** Layer-by-layer representation evolution

Show a vertical stack of N transformer layers (use N=6 for visualization). Each layer = one attention + FFN block.

Clicking a layer number reveals what kind of features that layer level typically learns (based on research findings from BERT probing studies):

- **Layer 1–2:** Surface features — parts of speech, basic word boundaries
- **Layer 3–4:** Syntactic features — phrase structure, dependency parsing
- **Layer 5–6:** Semantic features — coreference, semantic roles, world knowledge
- **(For deeper models, add) Layer 7+:** Complex reasoning, long-range dependencies

**"Depth comparison" mini-table:**

| Model | Layers | Parameters |
|-------|--------|------------|
| GPT-2 Small | 12 | 117M |
| GPT-2 XL | 48 | 1.5B |
| GPT-3 | 96 | 175B |
| GPT-4 (est.) | ~120 | ~1T+ |

**Key insight:** "Depth = abstraction. Each layer builds on the representations of the layer below. Early layers see syntax. Deep layers see meaning."

Animate a token "flowing up" through the layers with its representation changing at each level.

---

### Slide 10 — Positional Encoding

**Interactive:** Position heatmap + before/after toggle

**Problem first:** Show "dog bites man" vs "man bites dog" — attention alone is permutation-invariant (it doesn't care about order). Demonstrate: the attention score matrix would be identical for both sentences.

**Solution:** Positional Encoding adds a unique signal to each position before the attention computation.

**Interactive heatmap:** a grid of positions (rows, 0–15) × embedding dimensions (columns, 0–31). Each cell colored by its PE value. Student can:

- Hover any cell to see: `PE(pos=3, dim=6) = sin(3 / 10000^(6/512)) = 0.29`
- See that each position has a unique "fingerprint" across all dimensions
- Toggle between sine dimensions (even) and cosine dimensions (odd)

**Before/After toggle:**

- **Without PE:** "The model treats 'dog bites man' and 'man bites dog' identically"
- **With PE:** "Position 0, 1, 2 each carry unique signals — order is now meaningful"

**Slider:** "Sequence position" — drag to see how the PE vector changes for different positions. Shows that nearby positions have similar (but not identical) encodings — the model can generalize to positions it hasn't seen.

---

### Slide 11 — The Transformer Architecture (Big Picture)

**Interactive:** Clickable architecture diagram

A clean Canvas or SVG diagram of the full Transformer encoder. Components shown as labeled blocks in a vertical stack:

```
[Input Text] → [Tokenizer]
     ↓
[Token Embeddings] + [Positional Encoding]
     ↓
┌─────────────────────┐ ×N
│  Multi-Head         │
│  Attention          │
│  Add & Norm ───────┐│
│  Feed-Forward      ││
│  Add & Norm ───────┘│
└─────────────────────┘
     ↓
[Output Representation]
```

Each component block is **clickable**. Clicking reveals a side panel with:

- What it does (1 sentence)
- Input → Output shape
- Why it exists (design rationale)

**Components covered:**

| Component | Description |
|-----------|-------------|
| Token Embedding | "Converts token IDs to dense vectors" |
| Positional Encoding | "Injects position information" |
| Multi-Head Attention | "Computes context-aware representations" |
| Add & Norm (Residual) | "Prevents vanishing gradients, enables very deep networks" |
| Feed-Forward Network | "Adds non-linearity and model capacity per token independently" |
| Layer Normalization | "Stabilizes training by normalizing activations" |

Also show the "×N" annotation with a toggle for N=1, 6, 12, 24 — show how the diagram grows.

---

### Slide 12 — KV Cache: Why Inference is Fast

**Interactive:** Step-through inference animation

> This is a **NEW** slide that earns its place immediately after the architecture slide.

**Setup the problem:** During inference (generating text), the model generates one token at a time. For each new token, does it recompute Keys and Values for all previous tokens from scratch?

- **Naive answer:** Yes — O(n²) computation per token. Generating a 1000-token response would be painfully slow.
- **KV Cache:** Store the K and V matrices for all previously processed tokens. Only compute Q, K, V for the NEW token. Reuse cached K and V for attention computation.

**Interactive step-through animation:**

- Show a growing sequence of tokens, one being added per step
- **"Without cache" mode:** all K and V re-highlighted (recomputed) on every step — show the waste
- **"With KV cache" mode:** previously computed K/V shown as "cached" (greyed out, marked ✓), only the new token's K/V computed fresh
- Show a "compute cost" counter updating — cache cuts it dramatically

**Key concept cards:**

- "Why K and V but not Q? Because Q only belongs to the current token — there's nothing to cache."
- "KV Cache is the reason ChatGPT can respond to long prompts in seconds, not minutes."
- "The KV cache grows with context length — this is directly why GPT-4 with 128K context needs massive GPU memory."

**Memory calculation widget:** `KV cache size = 2 × num_layers × num_heads × d_k × seq_len × bytes_per_param`. Student can adjust `seq_len` with a slider and watch memory usage update in MB.

---

### Slide 13 — Context Window: The Memory Limit

**Interactive:** Context buffer visualizer

Natural follow-on from KV Cache: the cache is finite because GPU memory is finite. This is why context windows exist.

Show a visual buffer of tokens as a scrolling strip:

- Fill it token by token with a sample conversation
- When it hits the limit (e.g., 4096 tokens), show what happens: oldest tokens fall off the left edge
- The model literally cannot "see" what it can't fit in the window

**Interactive controls:**

- **Dropdown:** select context window size (GPT-2: 1024 · GPT-3.5: 4096 · GPT-4: 128K · Claude 3: 200K)
- Watch the visual buffer resize accordingly
- Show real-world token counts: "A 200-page novel ≈ 100K tokens. You can fit 2 novels in Claude's context window."

**Key concept cards:**

- "Context window ≠ memory. When a token leaves the window, the model has no access to it at all."
- "Longer context windows require proportionally more KV cache memory — this is why they cost more."
- "Most production LLM calls use far less than the max context — but edge cases like code analysis and book summarization push these limits."

**Token budget bar:** show "remaining tokens" as a progress bar that depletes as a sample conversation grows.

---

### Slide 14 — From Transformer to LLM: The Training Objective

**Interactive:** Next-token prediction game

Show the student a partial sentence and ask them to guess the next word. Then reveal the model's actual probability distribution.

**Presets** (click through):

| Prompt | Prediction | Probability |
|--------|------------|-------------|
| "The capital of France is ___" | Paris | p=0.94 |
| "To be or not to ___" | be | p=0.89 |
| "The neural network learned to ___" | generalize / predict / classify | — |
| "In 2017, the paper 'Attention is All You ___'" | Need | p=0.97 |
| "The quick brown fox jumps over the lazy ___" | dog | p=0.91 |

For each, show a Chart.js horizontal bar chart of the top 5 predicted tokens with probabilities.

**Key concept:** "The model isn't outputting one word — it outputs a probability distribution over its entire vocabulary (~50,000 tokens). The decoding strategy decides which token to pick. That's Week 5."

Show the training loop in one card: `Input sequence → predict next token → cross-entropy loss → backpropagate → update weights → repeat on trillions of tokens.`

---

### Slide 15 — You Just Understood the Foundation of Every LLM

Dark motivational slide — same format as Week 3.

**Headline:** "You Just Understood the Foundation of Every LLM"

**Subtitle:** "These aren't abstract concepts. They are the literal engineering inside GPT-4, Claude, and Gemini."

**Six concept-to-product mapping rows** (same styled cards as Week 3 Slide 21):

| Concept | Color | Mapping |
|---------|-------|---------|
| Tokenization | teal | "Before Claude reads your message, it converts it to token IDs using BPE. 'unbelievable' is 3 tokens." |
| Embeddings | blue | "Every token becomes a 4096-dimensional dense vector. That vector encodes meaning, context, and relationships." |
| Attention | purple | "The reason GPT-4 resolves 'it' correctly in complex sentences — attention reads the whole context at once." |
| Multi-Head Attention | amber | "GPT-4 has 96 attention heads per layer. Each one looks at a different linguistic relationship simultaneously." |
| KV Cache | orange | "The reason Claude responds in seconds to a 50,000-token context — K and V are cached, not recomputed." |
| Positional Encoding | green | "The reason 'dog bites man' and 'man bites dog' produce different responses — positions are encoded in every token's representation." |

**Closing quote:** *"'Attention Is All You Need' — Vaswani et al., 2017. Eight researchers wrote a paper. You now understand why it changed everything."*

---

### Slide 16 — Week 4 Recap + Week 5 Preview

Standard recap format matching Weeks 1–3.

**Left column** (navy card, teal header): "Week 4 — Key Takeaways" with 10 checkmarks:

- [x] Machines can't process raw text — tokens and embeddings are needed
- [x] Tokenization uses BPE — words become subword token sequences
- [x] Embeddings are learned dense vectors — position = meaning
- [x] Vector arithmetic works — king − man + woman ≈ queen
- [x] Context determines meaning — attention solves the ambiguity problem
- [x] Attention uses Q, K, V — softmax(QK^T/√d_k)·V
- [x] Multi-head attention captures multiple relationship types simultaneously
- [x] Positional encoding makes attention order-aware
- [x] KV Cache makes inference fast by avoiding redundant computation
- [x] Context window = the finite buffer of tokens the model can "see" at once

**Right column** (cardBg, blue header): Week 5 preview — "The Final Choice"

- Decoding Strategies
- Temperature — controlling creativity
- Top-P (nucleus) sampling
- Beam Search
- Why the same model gives different outputs each time

---

## Interactivity Requirements

Every slide must have at least one fully working interactive element:

| Slide | Interactive Element |
|-------|-------------------|
| 1 | Toggle buttons + live cosine similarity display |
| 2 | Live tokenizer (type text → see tokens split) |
| 3 | Scatter plot with clickable words + nearest neighbors |
| 4 | Animated vector arithmetic canvas with preset buttons |
| 5 | Clickable sentence ambiguity demo |
| 6 | Attention heatmap with clickable words + temperature slider |
| 7 | 4-step Q/K/V walkthrough with Next Step button |
| 8 | 4 head selector buttons with attention heatmaps |
| 9 | Layer stack with clickable layers + depth comparison table |
| 10 | PE heatmap with hover tooltips + before/after toggle |
| 11 | Clickable architecture blocks with side-panel descriptions |
| 12 | Cache step-through animation + memory calculator slider |
| 13 | Context buffer visualizer + context window size dropdown |
| 14 | Next-token prediction game with Chart.js probability bars |
| 15 | Flip cards (same as Week 3 builder slide) |
| 16 | Static recap (no interaction needed) |

---

## Technical Constraints

- Single `.html` file — no external files
- No npm, no build step — pure HTML/CSS/JS
- External only: Google Fonts + Chart.js from cdnjs
- **Canvas for:** particle title, vector arithmetic, architecture diagram, PE heatmap, KV cache animation, context buffer
- **Chart.js for:** embedding scatter, probability bars
- Responsive at ≤768px: stack layouts vertically, 44px touch targets
- Target file size: under 250KB
- No vertical scroll within slides (except mobile)
- `onSlideEnter(idx)` lazy-init pattern — only initialize a slide's canvas/chart when first visited
- Destroy and reinit charts when revisiting slides to avoid canvas reuse errors

---

## Instructions for the AI

1. Read `/mnt/skills/public/frontend-design/SKILL.md` before writing any code
2. Build the complete single HTML file implementing all 17 slides
3. Save as `/home/claude/week4_interactive.html`
4. Verify no obvious JS syntax errors
5. Copy to `/mnt/user-data/outputs/week4_interactive_lesson.html`
6. Present the file using `present_files`

**Output filename:** `week4_interactive_lesson.html`

**Quality bar:** Every interactive element must actually work. No placeholder TODOs. No broken canvases. The Week 3 file was ~100KB with 12 fully working slides. Week 4 is larger in scope (17 slides) — target ~180-220KB. Match or exceed the Week 3 visual quality.
