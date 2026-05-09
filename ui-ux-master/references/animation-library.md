# Animation Library

Use this in Phase 4 (build) when you need motion. These are tested patterns. **Always tune the timings and easings to fit the aesthetic** — defaults are slop.

The discipline: every animation answers a question. Why does this move? What is it telling the user? If you can't answer, cut it.

---

## Page Load Reveals

The first 800ms decide whether the user feels they've arrived somewhere designed.

### Staggered hero reveal

```css
.hero > * {
  opacity: 0;
  transform: translateY(24px);
  animation: rise 1s var(--ease-out-expo) forwards;
}
.hero > :nth-child(1) { animation-delay: 0.1s; }
.hero > :nth-child(2) { animation-delay: 0.2s; }
.hero > :nth-child(3) { animation-delay: 0.3s; }
.hero > :nth-child(4) { animation-delay: 0.4s; }

@keyframes rise {
  to { opacity: 1; transform: none; }
}
```

**Tuning:** ease-out-expo (`cubic-bezier(0.16, 1, 0.3, 1)`) is the most-used "cinematic" feel. Slower (`1.2s`) for refined/luxury, faster (`0.6s`) for tech/SaaS. Stagger delays should grow by 80–120ms each.

### Word-by-word headline reveal

```html
<h1 class="headline">
  <span class="word">Build</span>
  <span class="word">extraordinary</span>
  <span class="word">interfaces</span>
</h1>
```

```css
.word {
  display: inline-block;
  opacity: 0;
  transform: translateY(100%);
  animation: word-rise 0.8s var(--ease-out-expo) forwards;
  overflow: hidden;
}
.word:nth-child(1) { animation-delay: 0.1s; }
.word:nth-child(2) { animation-delay: 0.2s; }
.word:nth-child(3) { animation-delay: 0.3s; }

@keyframes word-rise {
  to { opacity: 1; transform: none; }
}
```

For a more dramatic effect, wrap each word in a `<span class="mask">` and clip overflow.

### Letter-by-letter (use sparingly, mostly for splash)

```js
document.querySelectorAll('[data-split]').forEach(el => {
  const text = el.textContent;
  el.innerHTML = [...text].map((c, i) =>
    `<span style="--i:${i}; display:inline-block;">${c === ' ' ? '&nbsp;' : c}</span>`
  ).join('');
});
```

```css
[data-split] span {
  opacity: 0;
  transform: translateY(0.5em);
  animation: letter-rise 0.5s var(--ease-out-expo) forwards;
  animation-delay: calc(var(--i) * 30ms);
}
@keyframes letter-rise { to { opacity: 1; transform: none; } }
```

---

## Scroll-Triggered Reveals

### Native CSS scroll-driven (modern browsers)

```css
@keyframes fade-up {
  from { opacity: 0; transform: translateY(48px); }
  to   { opacity: 1; transform: none; }
}

.scroll-reveal {
  animation: fade-up linear both;
  animation-timeline: view();
  animation-range: entry 10% cover 30%;
}
```

`animation-range`:
- `entry 0%` — when element starts entering viewport
- `entry 100%` / `cover 0%` — when fully entered
- `cover 50%` — center of viewport
- `exit 100%` — fully exited

### IntersectionObserver fallback

```js
const observer = new IntersectionObserver(
  (entries, obs) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('revealed');
        obs.unobserve(e.target);
      }
    });
  },
  { threshold: 0.15, rootMargin: '0px 0px -10% 0px' }
);

document.querySelectorAll('[data-reveal]').forEach(el => observer.observe(el));
```

```css
[data-reveal] {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.9s var(--ease-out-expo), transform 0.9s var(--ease-out-expo);
}
[data-reveal].revealed { opacity: 1; transform: none; }

[data-reveal][data-delay="1"] { transition-delay: 0.1s; }
[data-reveal][data-delay="2"] { transition-delay: 0.2s; }
[data-reveal][data-delay="3"] { transition-delay: 0.3s; }
```

---

## Parallax (used sparingly)

```js
const layers = document.querySelectorAll('[data-parallax]');

window.addEventListener('scroll', () => {
  const y = window.scrollY;
  layers.forEach(layer => {
    const speed = parseFloat(layer.dataset.parallax) || 0.3;
    layer.style.transform = `translate3d(0, ${y * speed}px, 0)`;
  });
}, { passive: true });
```

For better performance, use `IntersectionObserver` to only animate when in view, and use `requestAnimationFrame` to batch updates.

For modern parallax, prefer CSS scroll-driven animations over JS scroll handlers.

---

## Number Counters

```js
function countUp(el, target, duration = 1500) {
  const start = performance.now();
  const initial = 0;

  function frame(now) {
    const t = Math.min((now - start) / duration, 1);
    // ease-out-expo
    const eased = 1 - Math.pow(2, -10 * t);
    el.textContent = Math.round(initial + (target - initial) * eased).toLocaleString();
    if (t < 1) requestAnimationFrame(frame);
  }
  requestAnimationFrame(frame);
}

// Trigger via IntersectionObserver
const numObs = new IntersectionObserver((entries, obs) => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      const t = +e.target.dataset.target;
      countUp(e.target, t);
      obs.unobserve(e.target);
    }
  });
});
document.querySelectorAll('[data-target]').forEach(el => numObs.observe(el));
```

For finance/automotive: split-flap board style — see `domain-playbooks.md`.

---

## Marquee / Ticker

```css
.marquee {
  display: flex;
  overflow: hidden;
  user-select: none;
  gap: 4rem;
  mask-image: linear-gradient(to right, transparent, black 5%, black 95%, transparent);
}
.marquee__inner {
  display: flex;
  gap: 4rem;
  flex-shrink: 0;
  animation: marquee 30s linear infinite;
}
.marquee:hover .marquee__inner { animation-play-state: paused; }

@keyframes marquee {
  to { transform: translateX(-100%); }
}
```

```html
<div class="marquee">
  <div class="marquee__inner">
    <span>Item 1</span><span>Item 2</span><span>Item 3</span>
    <!-- duplicate the items for seamless loop -->
  </div>
  <div class="marquee__inner" aria-hidden="true">
    <span>Item 1</span><span>Item 2</span><span>Item 3</span>
  </div>
</div>
```

For finance tickers: alternate up/down colors per item, monospace, tabular numerals.

---

## Hover Micro-Interactions

### Button press
```css
.btn {
  transition: transform 0.15s var(--ease-out-expo), background 0.2s, box-shadow 0.2s;
}
.btn:hover { transform: translateY(-1px); box-shadow: var(--shadow-md); }
.btn:active { transform: translateY(0); box-shadow: var(--shadow-sm); }
```

### Card lift with depth
```css
.card {
  transition: transform 0.4s var(--ease-out-expo), box-shadow 0.4s;
}
.card:hover { transform: translateY(-4px); box-shadow: var(--shadow-lg); }
```

### Image reveal (e-commerce, portfolio)
```css
.thumb { position: relative; overflow: hidden; }
.thumb img.alt {
  position: absolute; inset: 0;
  opacity: 0;
  transition: opacity 0.5s var(--ease-out-expo);
}
.thumb:hover img.alt { opacity: 1; }
```

### Magnetic button (premium feel)
```js
document.querySelectorAll('[data-magnetic]').forEach(el => {
  el.addEventListener('mousemove', (e) => {
    const rect = el.getBoundingClientRect();
    const x = (e.clientX - rect.left - rect.width / 2) * 0.3;
    const y = (e.clientY - rect.top - rect.height / 2) * 0.3;
    el.style.transform = `translate(${x}px, ${y}px)`;
  });
  el.addEventListener('mouseleave', () => {
    el.style.transform = '';
  });
});
```
Add CSS transition for smooth return: `transition: transform 0.3s var(--ease-out-expo)`.

### Cursor follower (portfolios, agencies)
```js
const cursor = document.querySelector('.cursor');
let mx = 0, my = 0, cx = 0, cy = 0;

document.addEventListener('mousemove', (e) => { mx = e.clientX; my = e.clientY; });

function loop() {
  cx += (mx - cx) * 0.18;
  cy += (my - cy) * 0.18;
  cursor.style.transform = `translate(${cx}px, ${cy}px)`;
  requestAnimationFrame(loop);
}
loop();
```

```css
.cursor {
  position: fixed; top: 0; left: 0;
  width: 32px; height: 32px;
  border: 1px solid var(--color-fg);
  border-radius: 50%;
  pointer-events: none;
  mix-blend-mode: difference;
  z-index: 9999;
  transition: width 0.3s, height 0.3s;
}
body.hover-link .cursor { width: 64px; height: 64px; }
```

---

## Loading States

### Skeleton loader (better than spinners)
```css
.skeleton {
  background: linear-gradient(
    90deg,
    var(--color-surface) 0%,
    color-mix(in oklch, var(--color-surface), var(--color-fg) 8%) 50%,
    var(--color-surface) 100%
  );
  background-size: 200% 100%;
  animation: shimmer 1.5s linear infinite;
  border-radius: var(--radius-md);
}

@keyframes shimmer {
  to { background-position: -200% 0; }
}
```

### Refined progress (luxury)
```css
.progress {
  height: 1px;
  background: var(--color-border);
  position: relative;
  overflow: hidden;
}
.progress::after {
  content: '';
  position: absolute; inset: 0;
  width: 30%;
  background: var(--color-accent);
  animation: progress 1.5s var(--ease-in-out-quart) infinite;
}
@keyframes progress {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(400%); }
}
```

### Domain-specific loaders
- **Cars** — animated speedometer needle sweep, RPM gauge
- **Music** — pulsing equalizer bars
- **Food** — steam wisps, bubbling pot
- **Fitness** — heartbeat pulse
- **Finance** — candlestick building

---

## Page Transitions

### View Transitions API (Chrome stable, Safari/Firefox progressive)

```js
function navigate(url) {
  if (!document.startViewTransition) {
    location.href = url;
    return;
  }
  document.startViewTransition(async () => {
    const res = await fetch(url);
    const html = await res.text();
    const parser = new DOMParser();
    const newDoc = parser.parseFromString(html, 'text/html');
    document.body.replaceChildren(...newDoc.body.children);
    history.pushState({}, '', url);
  });
}
```

```css
::view-transition-old(root) {
  animation: 400ms var(--ease-out-expo) both fade-out;
}
::view-transition-new(root) {
  animation: 400ms var(--ease-out-expo) 100ms both fade-in;
}

@keyframes fade-out { to { opacity: 0; transform: translateY(-12px); } }
@keyframes fade-in { from { opacity: 0; transform: translateY(12px); } }
```

For shared element transitions (image carrying between pages), give matching `view-transition-name` on both old and new elements.

---

## Modal / Drawer

```css
dialog.modal {
  border: none;
  padding: 0;
  background: transparent;
  max-width: min(40rem, 90vw);
}
dialog.modal::backdrop {
  background: oklch(0.16 0.01 260 / 0);
  backdrop-filter: blur(0px);
  transition: background 0.4s, backdrop-filter 0.4s;
}
dialog.modal[open]::backdrop {
  background: oklch(0.16 0.01 260 / 0.4);
  backdrop-filter: blur(8px);
}
dialog.modal > .panel {
  background: var(--color-surface);
  padding: var(--space-8);
  border-radius: var(--radius-lg);
  transform: translateY(20px);
  opacity: 0;
  transition: transform 0.4s var(--ease-out-expo), opacity 0.3s;
}
dialog.modal[open] > .panel {
  transform: none;
  opacity: 1;
}
```

---

## Domain-Signature Animations (catalog)

These should be implemented when domain-relevant. See `domain-playbooks.md` for which to pick.

### Steam (food)
```html
<div class="steam">
  <span></span><span></span><span></span>
</div>
```
```css
.steam { position: relative; height: 120px; width: 60px; }
.steam span {
  position: absolute; bottom: 0;
  width: 12px; height: 12px;
  background: oklch(1 0 0 / 0.4);
  border-radius: 50%;
  filter: blur(8px);
  animation: steam 3s ease-out infinite;
}
.steam span:nth-child(2) { left: 20px; animation-delay: 0.6s; }
.steam span:nth-child(3) { left: 40px; animation-delay: 1.2s; }
@keyframes steam {
  0%   { transform: translateY(0) scale(1); opacity: 0; }
  20%  { opacity: 0.7; }
  100% { transform: translateY(-120px) scale(2.5); opacity: 0; }
}
```

### Pulse / heartbeat (fitness, healthcare)
```css
.pulse {
  animation: pulse 1.4s var(--ease-in-out-quart) infinite;
}
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  10%      { transform: scale(1.08); }
  20%      { transform: scale(1); }
  30%      { transform: scale(1.04); }
  40%      { transform: scale(1); }
}
```

### Headlight glow (cars)
```css
.car-card { position: relative; overflow: hidden; }
.car-card::before {
  content: '';
  position: absolute;
  width: 200px; height: 200px;
  background: radial-gradient(oklch(0.95 0.1 80 / 0.5), transparent 70%);
  top: 50%; left: 50%;
  transform: translate(-50%, -50%) scale(0);
  transition: transform 0.6s var(--ease-out-expo), opacity 0.6s;
  opacity: 0;
}
.car-card:hover::before { transform: translate(-50%, -50%) scale(1); opacity: 1; }
```

### Equalizer bars (music)
```html
<div class="eq">
  <span></span><span></span><span></span><span></span><span></span>
</div>
```
```css
.eq { display: flex; gap: 3px; align-items: end; height: 24px; }
.eq span {
  width: 3px; background: var(--color-accent); border-radius: 2px;
  animation: eq 1s ease-in-out infinite;
}
.eq span:nth-child(1) { animation-delay: 0.0s; height: 60%; }
.eq span:nth-child(2) { animation-delay: 0.2s; height: 80%; }
.eq span:nth-child(3) { animation-delay: 0.1s; height: 100%; }
.eq span:nth-child(4) { animation-delay: 0.3s; height: 70%; }
.eq span:nth-child(5) { animation-delay: 0.15s; height: 90%; }

@keyframes eq {
  0%, 100% { transform: scaleY(1); }
  50%      { transform: scaleY(0.4); }
}
```

### SVG line drawing (any technical domain — engineering, science, finance charts)
```css
.line-draw {
  stroke-dasharray: 1000;
  stroke-dashoffset: 1000;
  animation: draw 2s var(--ease-out-expo) forwards;
}
@keyframes draw { to { stroke-dashoffset: 0; } }
```

---

## Performance & Accessibility for Motion

**Always:**
- Animate `transform` and `opacity` only (hardware-accelerated)
- Use `will-change` sparingly and remove after animation
- Pause off-screen animations
- Honor `prefers-reduced-motion`

**Never:**
- Trigger long animations on every scroll event without throttling
- Animate `width`, `height`, `top`, `left` (use `transform` instead)
- Auto-play video/audio without user gesture
- Use `position: sticky` with heavy children inside scroll-driven animations (causes jank)

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    scroll-behavior: auto !important;
  }
}
```

But: provide a tasteful static state, not just no motion. A page with reduced motion should still look designed, just calmer.
