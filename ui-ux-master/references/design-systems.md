# Modern Design Systems & Technical Patterns

Use this in Phase 4 (build) when you need the technical foundation. This isn't a textbook — it's the patterns to apply now.

---

## Design Tokens (CSS Custom Properties)

Define everything as tokens at the root. Never use raw values inside component styles.

```css
:root {
  /* Color — use OKLCH for perceptually uniform palettes where browser support allows */
  --color-bg: oklch(0.98 0.01 80);
  --color-fg: oklch(0.18 0.02 260);
  --color-accent: oklch(0.65 0.22 25);
  --color-muted: oklch(0.55 0.02 260);
  --color-surface: oklch(0.96 0.01 80);
  --color-border: oklch(0.88 0.01 80);

  /* Type scale — fluid with clamp() */
  --text-xs:   clamp(0.75rem, 0.7rem + 0.2vw, 0.8125rem);
  --text-sm:   clamp(0.875rem, 0.83rem + 0.2vw, 0.9375rem);
  --text-base: clamp(1rem, 0.95rem + 0.25vw, 1.0625rem);
  --text-lg:   clamp(1.125rem, 1.05rem + 0.4vw, 1.25rem);
  --text-xl:   clamp(1.375rem, 1.25rem + 0.6vw, 1.625rem);
  --text-2xl:  clamp(1.75rem, 1.5rem + 1.2vw, 2.25rem);
  --text-3xl:  clamp(2.25rem, 1.8rem + 2vw, 3.25rem);
  --text-4xl:  clamp(3rem, 2.2rem + 3.5vw, 5rem);
  --text-display: clamp(4rem, 2.8rem + 6vw, 8rem);

  /* Spacing scale — never deviate */
  --space-1: 0.25rem;
  --space-2: 0.5rem;
  --space-3: 0.75rem;
  --space-4: 1rem;
  --space-6: 1.5rem;
  --space-8: 2rem;
  --space-12: 3rem;
  --space-16: 4rem;
  --space-24: 6rem;
  --space-32: 8rem;

  /* Radii */
  --radius-sm: 0.375rem;
  --radius-md: 0.625rem;
  --radius-lg: 1rem;
  --radius-full: 9999px;

  /* Shadows — layered, color-tinted, never default black */
  --shadow-sm: 0 1px 2px oklch(0.18 0.02 260 / 0.05);
  --shadow-md: 0 4px 12px oklch(0.18 0.02 260 / 0.08), 0 1px 3px oklch(0.18 0.02 260 / 0.05);
  --shadow-lg: 0 24px 48px oklch(0.18 0.02 260 / 0.12), 0 4px 12px oklch(0.18 0.02 260 / 0.06);

  /* Motion */
  --ease-out-expo: cubic-bezier(0.16, 1, 0.3, 1);
  --ease-in-out-quart: cubic-bezier(0.76, 0, 0.24, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
  --duration-fast: 150ms;
  --duration-base: 250ms;
  --duration-slow: 500ms;
  --duration-slower: 800ms;

  /* Layout */
  --container-sm: 40rem;
  --container-md: 64rem;
  --container-lg: 80rem;
  --container-xl: 96rem;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: oklch(0.16 0.01 260);
    --color-fg: oklch(0.96 0.01 80);
    --color-surface: oklch(0.22 0.01 260);
    --color-border: oklch(0.28 0.01 260);
    --color-muted: oklch(0.65 0.02 260);
    /* Dark mode is not just inverted — adjust accent saturation */
    --color-accent: oklch(0.7 0.18 25);
  }
}
```

For OKLCH support, the spec is well supported in modern browsers (Chrome 111+, Safari 15.4+, Firefox 113+). If supporting older browsers, provide HSL fallbacks via `@supports`.

---

## Fluid Typography

Use `clamp()` instead of breakpoint-driven font sizes. Modern formula:

```
clamp(MIN_SIZE, BASE + SCALE * 1vw, MAX_SIZE)
```

Don't use raw clamp magic numbers — use a calculator (utopia.fyi) or follow this rule: between viewports 320px and 1440px (common range), every `1vw` ≈ `0.16rem` of difference.

Display sizes need negative tracking:
```css
.display {
  font-size: var(--text-display);
  letter-spacing: -0.04em;
  line-height: 0.95;
  font-weight: 600;
}
```

Body needs comfortable measure:
```css
.prose {
  max-width: 65ch;
  font-size: var(--text-base);
  line-height: 1.65;
  letter-spacing: -0.005em;
}
```

---

## Color Strategy

**Three-tier color use:**

1. **Foundational** — bg, fg, surface, border. The 80% you don't notice.
2. **Semantic** — success, warning, error, info. Used for state.
3. **Brand / accent** — the 1–2 colors that signal *this product*. Used scarcely so they retain meaning.

**Don't ship purple-to-blue gradients on white.** That's the AI-slop signature. If you want a gradient, make it specific to the domain.

**Dark mode requires real design work:**
- Backgrounds get a hint of color (not pure black) — `oklch(0.16 0.01 260)` reads richer than `#000`
- Reduce accent saturation slightly (high saturation glares on dark)
- Reduce text contrast slightly (true white on true black is harsh)
- Borders need different luminance, not just inverted color
- Shadows become glows or subtle inner light

---

## Layout

**CSS Grid for page structure, Flexbox for components.**

Modern layout patterns:

```css
/* The classic asymmetric editorial */
.layout {
  display: grid;
  grid-template-columns: 1fr min(65ch, 100%) 1fr;
}
.layout > * { grid-column: 2; }
.layout > .full-bleed { grid-column: 1 / -1; }
.layout > .wide { grid-column: 1 / 3; }

/* Container queries for component-driven design */
.card-container { container-type: inline-size; }
@container (min-width: 30rem) {
  .card { grid-template-columns: 1fr 2fr; }
}

/* Subgrid for aligned content across siblings */
.row { display: grid; grid-template-columns: subgrid; }
```

**Asymmetry:** never split everything 50/50 unless you have a reason. Try 5/7, 4/8, 3/9 columns. Off-center hero. Diagonal flow.

---

## Motion Principles

**Every interaction has a state.** Default → hover → active → loading → success → error. Design all of them.

**Easing matters more than duration.** Default `ease-out` is fine but boring. Use:
- `cubic-bezier(0.16, 1, 0.3, 1)` — ease-out-expo, dramatic decelerate, great for entries
- `cubic-bezier(0.76, 0, 0.24, 1)` — ease-in-out-quart, smooth two-sided
- `cubic-bezier(0.34, 1.56, 0.64, 1)` — gentle overshoot, useful for delight
- Spring physics via Motion / Framer Motion when you need physical-feeling motion

**Choreography:** stagger related elements. Don't fade in 12 things at once.

```css
.stagger-child {
  opacity: 0;
  transform: translateY(20px);
  animation: rise 0.8s var(--ease-out-expo) forwards;
}
.stagger-child:nth-child(1) { animation-delay: 0.0s; }
.stagger-child:nth-child(2) { animation-delay: 0.08s; }
.stagger-child:nth-child(3) { animation-delay: 0.16s; }
.stagger-child:nth-child(4) { animation-delay: 0.24s; }

@keyframes rise {
  to { opacity: 1; transform: none; }
}
```

**Always animate `transform` and `opacity`, not `top/left/width/height`.** GPU vs. CPU.

**Respect motion preferences:**
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
    scroll-behavior: auto !important;
  }
}
```

But don't just disable — provide tasteful static alternatives for key animated content.

---

## Scroll-Driven Animations

Modern CSS scroll-driven animations (Chrome stable, Safari 26+):

```css
@keyframes reveal {
  from { opacity: 0; transform: translateY(40px); }
  to   { opacity: 1; transform: none; }
}

.reveal-on-scroll {
  animation: reveal linear both;
  animation-timeline: view();
  animation-range: entry 0% cover 30%;
}
```

For broader browser support, use Intersection Observer:

```js
const io = new IntersectionObserver((entries) => {
  for (const e of entries) {
    if (e.isIntersecting) {
      e.target.classList.add('in-view');
      io.unobserve(e.target);
    }
  }
}, { threshold: 0.15, rootMargin: '0px 0px -10% 0px' });

document.querySelectorAll('[data-reveal]').forEach(el => io.observe(el));
```

```css
[data-reveal] { opacity: 0; transform: translateY(30px); transition: opacity 0.8s var(--ease-out-expo), transform 0.8s var(--ease-out-expo); }
[data-reveal].in-view { opacity: 1; transform: none; }
```

---

## Micro-Interactions

**Buttons that press:**
```css
.btn {
  transition: transform 0.15s var(--ease-out-expo), background 0.2s;
}
.btn:hover { transform: translateY(-1px); }
.btn:active { transform: translateY(0); }
```

**Inputs with personality:**
```css
.input {
  border-bottom: 1px solid var(--color-border);
  background: transparent;
  padding: var(--space-3) 0;
  transition: border-color 0.3s;
}
.input:focus-visible {
  outline: none;
  border-bottom-color: var(--color-accent);
}
.input:focus-visible + .label { color: var(--color-accent); transform: translateY(-100%) scale(0.85); }
```

**Links that have something to say:**
```css
.link {
  position: relative;
  text-decoration: none;
  background-image: linear-gradient(var(--color-accent), var(--color-accent));
  background-size: 0% 1px;
  background-position: 0 100%;
  background-repeat: no-repeat;
  transition: background-size 0.4s var(--ease-out-expo);
}
.link:hover { background-size: 100% 1px; }
```

---

## Decorative Depth

Backgrounds aren't flat. Match the aesthetic direction:

**Grain overlay** (works in almost any aesthetic):
```css
.grain::after {
  content: '';
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' width='100' height='100'><filter id='n'><feTurbulence baseFrequency='0.9'/></filter><rect width='100%' height='100%' filter='url(%23n)' opacity='0.4'/></svg>");
  mix-blend-mode: overlay;
  opacity: 0.15;
  pointer-events: none;
}
```

**Gradient mesh** (soft maximalist, ambient):
```css
.mesh-bg {
  background:
    radial-gradient(at 27% 37%, oklch(0.85 0.15 25 / 0.3) 0px, transparent 50%),
    radial-gradient(at 97% 21%, oklch(0.85 0.15 200 / 0.3) 0px, transparent 50%),
    radial-gradient(at 52% 99%, oklch(0.85 0.15 80 / 0.3) 0px, transparent 50%),
    var(--color-bg);
}
```

**Dot grid** (technical, SaaS):
```css
.dot-grid {
  background-image: radial-gradient(var(--color-border) 1px, transparent 1px);
  background-size: 24px 24px;
}
```

**Subtle line grid** (editorial, structured):
```css
.line-grid {
  background-image:
    linear-gradient(to right, var(--color-border) 1px, transparent 1px),
    linear-gradient(to bottom, var(--color-border) 1px, transparent 1px);
  background-size: 80px 80px;
  opacity: 0.4;
}
```

---

## Dark Mode Strategy

Two patterns:

**1. System-driven** (default for marketing):
```css
@media (prefers-color-scheme: dark) { :root { ... } }
```

**2. User-toggled** (for product):
```css
[data-theme="dark"] { ... }
[data-theme="light"] { ... }
```

```js
const applyTheme = (theme) => {
  document.documentElement.dataset.theme = theme;
  localStorage.setItem('theme', theme);
};

const stored = localStorage.getItem('theme');
const system = matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
applyTheme(stored ?? system);
```

Always respect `prefers-color-scheme` as the default, and let users override.

---

## Typography Pairing Recipes

A few tested pairings (none are Inter):

- **Editorial luxury** — *Söhne* (body) + *GT Sectra* (display)
- **Modern tech** — *Söhne* (body) + *Söhne Mono* (accents)
- **Brutalist editorial** — *Neue Haas Grotesk* (body) + *Druk* (display)
- **Soft/playful** — *Inter* if you must (body) + *Beausite Classic* (display)
- **Open-source modern** — *Geist Sans* (body) + *Geist Mono* (accents) — Vercel's free family
- **Distinctive open-source** — *General Sans* + *Tanker* (Indian Type Foundry, free)
- **Refined free** — *Switzer* (body) + *Boska* (display) — both free from Indian Type Foundry

When using Google Fonts, prefer: Fraunces, Manrope, Sora, Bricolage Grotesque, Instrument Serif, Geist. Avoid: Roboto, Open Sans, Lato, Poppins (overused).

---

## Image Treatment

- Use `loading="lazy"` on below-fold images
- Provide `srcset` and `sizes` for responsive sources
- Use modern formats — WebP at minimum, AVIF where size matters
- For art-direction crops, use `<picture>` with `media` queries
- Set explicit `width` and `height` to prevent CLS
- For decorative images, `aria-hidden="true"` and `alt=""`

```html
<picture>
  <source media="(min-width: 64rem)" srcset="hero-wide.avif" type="image/avif">
  <source media="(min-width: 64rem)" srcset="hero-wide.webp" type="image/webp">
  <source srcset="hero-mobile.avif" type="image/avif">
  <img src="hero-mobile.jpg" alt="..." width="1280" height="720" loading="eager" fetchpriority="high">
</picture>
```

---

## Form Patterns

**Float-label inputs:**
```html
<div class="field">
  <input id="email" type="email" placeholder=" " required>
  <label for="email">Email</label>
</div>
```

```css
.field { position: relative; }
.field input { padding: 1.25rem 0 0.5rem; border: none; border-bottom: 1px solid var(--color-border); background: transparent; }
.field label {
  position: absolute; top: 1rem; left: 0;
  transition: transform 0.2s var(--ease-out-expo), color 0.2s;
  pointer-events: none;
}
.field input:focus + label,
.field input:not(:placeholder-shown) + label {
  transform: translateY(-110%) scale(0.85);
  transform-origin: 0 0;
}
.field input:focus { outline: none; border-bottom-color: var(--color-accent); }
```

---

## When to use a framework

- **HTML/CSS/JS** — works for marketing sites, landing pages, simple components
- **Tailwind** — when the user is already on it; fast component construction; great with design tokens defined in `tailwind.config`
- **React + Motion (Framer Motion)** — for complex motion choreography, gesture, layout animations (`<motion.div layout>`)
- **Svelte / Vue** — match the user's existing stack
- **shadcn/ui** — solid base components when you'll customize aggressively, never as-is

If the user doesn't specify, default to clean HTML/CSS/JS for landing pages and React + Tailwind + Motion for app interfaces. Always ask if unclear.
