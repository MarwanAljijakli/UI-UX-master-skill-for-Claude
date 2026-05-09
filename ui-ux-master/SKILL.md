---
name: ui-ux-master
description: Transform any existing UI into a world-class, modern, domain-aware design through a rigorous audit, redesign, test, and iterate loop. Use this skill whenever the user wants to redesign, modernize, improve, beautify, polish, level-up, refresh, or overhaul any frontend — websites, web apps, dashboards, landing pages, components, or mobile screens. Trigger on phrases like "redesign", "improve the UI", "make it modern", "make it the best", "needs more animations", "elevate this", "polish this", "give it a glow-up", or whenever the user shares existing code or screenshots and wants the design improved. Always studies the domain first (cars → driving animations, gauges, parallax car parts; food → steam, ingredient motion; finance → tickers, animated charts) and never stops at the first pass — iterates through multiple refinement rounds until the result is genuinely world-class.
---

# UI/UX Master

A skill for taking any existing UI and elevating it to a world-class, modern, domain-aware design — with a relentless iterate-until-excellent mindset, rigorous testing, and creative motion that fits the subject matter.

## Mission

Most "redesigns" stop too early. They make a UI *better*, not *world-class*. This skill exists to push past that. The output should be the kind of work that gets bookmarked on Awwwards, not a Bootstrap reskin.

The user has handed you something that exists — code, a screenshot, a live site, a Figma export, a description — and wants it transformed. Your job:

1. **Understand what it is** (audit + domain study)
2. **Pick a bold direction** (commit to an aesthetic identity, not a template)
3. **Rebuild with modern craft** (typography, color, motion, layout, micro-interactions)
4. **Add domain-aware life** (the *thing the site is about* should breathe through the design)
5. **Test everything** (responsive, accessible, performant, cross-browser)
6. **Iterate until it's actually great** (don't stop at "good enough")

Treat each phase as non-skippable. A redesign without an audit is a guess. A redesign without testing is a draft.

---

## Phase 1 — Audit the existing UI

Before changing anything, understand what's there. Read `references/audit-framework.md` for the full checklist. The short version: walk through these axes and write a one-line verdict on each:

- **Typography** — font choices, hierarchy, line-height, letter-spacing, contrast between display and body
- **Color & contrast** — palette intent, WCAG contrast ratios, dark mode story, accent discipline
- **Spacing & rhythm** — is there a scale? do related things group? does it breathe?
- **Layout & composition** — grid, alignment, asymmetry usage, focal point, scan path
- **Motion** — what moves, how, why, and what's missing
- **Hierarchy** — can a user identify the most important element in 1 second?
- **Interactions** — hover states, focus states, active states, transitions
- **Accessibility** — keyboard nav, screen reader labels, contrast, motion-reduce, focus visible
- **Responsive behavior** — mobile, tablet, desktop, ultra-wide; what breaks
- **Performance signals** — image weight, unused CSS, blocking scripts, layout shift
- **Brand & domain fit** — does it look like *this kind of thing* or like a generic template?

Output a brief audit report to the user (5–10 bullet points) BEFORE touching code. This is not optional. The user needs to see you understood their starting point. Then ask: "Before I rebuild — anything you want me to keep, anything you want me to throw away?"

If they share code/screenshots, work with what's there. If they only describe the system, ask 1–2 sharp clarifying questions (purpose, audience, brand tone) and proceed.

---

## Phase 2 — Study the domain

This is where most AI redesigns fail. They produce a generic "modern" look that could be any product. World-class design speaks the language of the subject.

**The rule: the domain should be visible in the design even with the text removed.**

Open `references/domain-playbooks.md` and read the relevant section before designing. It covers playbooks for cars, food, finance, fashion, real estate, healthcare, education, gaming, fitness, travel, music, news, SaaS/B2B, e-commerce, portfolios, agencies, and more. If the domain isn't in the playbook, derive a playbook on the fly using these questions:

- What does this thing *physically look like*? (cars are sleek, metallic, fast → suggests gradients, motion blur, kinetic type)
- What sounds and rhythms is it associated with? (music = waveforms, beats, pulse)
- What metaphors does the industry use? (finance = up/down arrows, candles, tickers)
- What materials, textures, and lighting fit it? (luxury = warm shadows, serif type; tech = sharp edges, neon)
- What motion is native to it? (cars drive, food steams, charts grow, water ripples)

Then translate that into design decisions: typography, colors, illustration style, signature animations, hero treatment, decorative elements, cursor, sound design (if appropriate).

**Domain-aware motion examples:**

- **Cars** — hero with a car driving across the viewport, parallax car parts on scroll, animated speedometer/RPM gauges as data viz, headlight glow on hover, tire-tread patterns as decorative borders, gear-shift transitions between sections
- **Food** — animated steam rising from hero image, ingredients flying in on load, recipe step transitions like flipping pages, sizzle/bubble micro-animations on CTAs
- **Finance** — live ticker tape header, animated candle charts that build on scroll, number counters that flip like a stock board, gradient meshes that pulse with market data
- **Real estate** — parallax architectural sections, floor-plan reveals, room walkthroughs as scroll-triggered carousels, blueprint-line illustrations
- **Fitness** — heart-rate pulse on the logo, rep counters, motion-trail effects on imagery, muscle-group highlights on hover
- **Music** — waveform dividers, beat-synced animations, vinyl-spin loaders, equalizer bars as data viz

Don't pick *all* of these — pick 2–3 signature moves and execute them with precision.

---

## Phase 3 — Commit to a bold aesthetic direction

Generic = forgettable. Pick an extreme and lean in. Sample directions:

- **Brutalist editorial** — oversized serifs, harsh grids, raw HTML aesthetic, monochrome with one acid accent
- **Soft maximalist** — pastel gradients, organic blobs, layered transparencies, playful type
- **Retro-futuristic** — VHS scanlines, chromatic aberration, 80s neon, monospace
- **Refined luxury** — generous whitespace, fine serifs, deep blacks, gold accents, slow elegant motion
- **Industrial / utilitarian** — monospace UI, gridded data, terminal aesthetic, restrained color
- **Organic / natural** — earthy palette, hand-drawn elements, soft shadows, gentle motion
- **Kinetic / motion-first** — type that moves, scroll-driven everything, generative graphics
- **Glass / depth** — frosted glass layers, soft 3D, light refraction, subtle parallax

Tell the user the direction in one sentence ("I'm going with refined luxury — deep ink-black, ivory, gold accents, slow editorial-paced motion") and **why it fits the domain**. Get a thumbs up before going deep, unless they've already given you a clear brief.

---

## Phase 4 — Rebuild with modern craft

Now write the code. Open `references/design-systems.md` for the modern technical patterns (tokens, fluid type, container queries, color spaces, motion principles, dark mode strategy).

**Non-negotiable craft standards:**

- **Typography** — distinctive font pairing (one display + one body, NOT Inter + Inter). Fluid type with `clamp()`. Optical-size variations where supported. Tight tracking on display, looser on small body.
- **Color** — design tokens via CSS custom properties. Use OKLCH or LCH for perceptually uniform palettes when possible. Define a full scale (50–950) for each role. Dark mode is not an afterthought — design it from day one.
- **Spacing** — a scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 …), no arbitrary numbers. Use it religiously.
- **Layout** — CSS Grid for page-level structure, Flexbox for component-level. Container queries where the component is reused at different widths. Asymmetry where it serves the eye.
- **Motion** — every interaction has a state. Hover, focus, active, loading, success, error. Use spring physics or carefully tuned cubic-bezier (`cubic-bezier(0.16, 1, 0.3, 1)` is a great default for "ease-out-expo"). Respect `prefers-reduced-motion`.
- **Micro-interactions** — buttons that press, inputs that focus with personality, links that have something to say. None of this is decoration — it's feedback.
- **Imagery** — never stock-photo defaults. Use illustration, photography, or generative graphics that fit the aesthetic.
- **Decorative depth** — backgrounds aren't flat. Gradient meshes, grain, subtle noise, dot grids, corner ornaments — chosen to match the direction, never piled on.

Read `references/animation-library.md` for a catalog of high-quality animations (page-load reveals, scroll-triggered staggers, hover micro-interactions, loading states, transitions) you can adapt. Always tune timings — defaults are slop.

**Output format:**
- Default to working HTML/CSS/JS with Tailwind or vanilla CSS, depending on the user's stack.
- If they're using React/Vue/Svelte, match their framework. Use Motion (Framer Motion) for React when complex motion is needed; vanilla CSS for simple cases.
- Make the code production-grade — no placeholder text, no `// TODO`, no half-finished states.
- Comments explain *why*, not *what*.

---

## Phase 5 — Test everything

A redesign that hasn't been tested isn't done. Open `references/testing-checklist.md` for the full procedure. The minimum gate before showing the user:

- **Responsive** — actually resize and check 360px, 768px, 1280px, 1920px. Note what breaks. Fix it.
- **Keyboard nav** — Tab through every interactive element. Focus visible? Order logical? Trap-free?
- **Screen reader** — every image has alt, every button has a label, headings are hierarchical, landmarks exist.
- **Contrast** — every text/background pair hits WCAG AA at minimum (AAA for body where possible). Use a contrast checker.
- **Motion** — `prefers-reduced-motion: reduce` actually reduces motion (don't just disable — provide a tasteful static alternative).
- **Performance** — no images over what the layout needs, no fonts loaded that aren't used, no render-blocking surprises.
- **Cross-browser** — at least: latest Chrome, Safari, Firefox. Mobile Safari is its own animal — test it.
- **Empty / loading / error states** — designed, not afterthoughts.
- **Dark mode** — if you implemented it, verify the entire surface, not just the homepage.

Report results to the user. Don't gloss over failures — fix them or explicitly call them out as known limitations.

---

## Phase 6 — Iterate until it's actually great

This is the phase the skill exists to enforce. **The first pass is never the final pass.**

After Phase 5, do a brutal self-review using these questions:

1. If I posted this on Awwwards or Dribbble, would it stand up next to the top 10% — or look like AI output?
2. Is there a single signature moment that someone would screenshot and share? If not, build one.
3. Does the domain breathe through the design, or could this be any product?
4. Are the animations crafted (timing, easing, choreography) or just "added"?
5. Is the typography doing real work, or is it default?
6. Have I made any timid choices I should make bolder?
7. Is there any section that feels weaker than the rest? (There always is on pass 1 — find it.)

Pick the **2–3 weakest moments** and rebuild them. Then run Phase 5 again. Then re-review. Continue until your honest answer to question 1 is yes.

**Stop conditions:**
- The user says "this is great, ship it" (only stop if they're explicit)
- You've completed at least 2 full iterations AND every section passes the self-review

**Do not stop because:**
- The user says "thanks" or "looks good" without explicitly approving — keep refining and offer the next iteration
- It's "fine" — fine is the enemy
- You're tired of the task

After each iteration, summarize what changed and why in 3–5 lines. Then ask: "Want me to push another round, or are we shipping?"

---

## Workflow summary

```
1. AUDIT       → write 5–10 line audit, ask what to keep/throw
2. DOMAIN      → load relevant playbook, identify 2–3 signature moves
3. DIRECTION   → commit to one bold aesthetic, get thumbs up
4. BUILD       → write production code with modern craft standards
5. TEST        → run the checklist, fix what fails, report honestly
6. ITERATE     → self-review brutally, rebuild weakest sections, repeat
```

Do not skip phases. Do not collapse phases. Each one earns its place.

---

## Reference files

Load these as needed during the relevant phase:

- `references/audit-framework.md` — full audit checklist with examples (Phase 1)
- `references/domain-playbooks.md` — design playbooks for 18+ domains (Phase 2)
- `references/design-systems.md` — modern technical patterns: tokens, fluid type, motion, dark mode (Phase 4)
- `references/animation-library.md` — catalog of crafted animations and how to tune them (Phase 4)
- `references/testing-checklist.md` — full QA procedure with tools and code snippets (Phase 5)

---

## What "world-class" actually means

Concretely, the bar is: a senior design director at Apple, Linear, Stripe, Vercel, or Studio for the Whole Could would look at this and not flinch. That doesn't mean it must look *like* those — it means the level of intentionality, craft, and finish must be on par.

Signs you're hitting the bar:
- Type feels chosen, not defaulted
- Motion has personality and rhythm, not just presence
- Color does work — it directs the eye, sets the mood, signals brand
- The first viewport tells the user what this is and makes them want to scroll
- Empty states, error states, and edge cases were designed, not retrofitted
- Removing 20% of elements would make it worse, not better — every piece earns its place
- The domain is unmistakable

Signs you're not there yet:
- The design could be ported to a different industry by changing copy
- Animations are uniform 0.3s ease-out across the board
- The hero is a centered headline + subheadline + CTA
- Spacing feels close-but-not-quite
- Dark mode is "the same with inverted colors"

Don't ship until you're on the right side of that list.
