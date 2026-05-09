# Testing Checklist

Use this in Phase 5 of the workflow. A redesign that hasn't been tested isn't done. Walk every section. Don't skip. Honest reporting beats glossy reporting.

---

## 1. Responsive

Test at minimum these viewport widths:

| Width | Device | What to check |
|-------|--------|---------------|
| 360px | Small phone | Type readable, touch targets ≥ 44×44px, no horizontal scroll |
| 414px | iPhone Pro Max | Layout breathes, image crops sensible |
| 768px | Tablet portrait | Hybrid mobile/desktop layout doesn't get awkward |
| 1024px | Tablet landscape / small laptop | Most important breakpoint to land |
| 1280px | Standard laptop | Designed for, should be the sweet spot |
| 1440px | Larger laptop | Doesn't feel sparse |
| 1920px | Desktop | Composition holds, no awkward stretching |
| 2560px | Large display | Container max-widths, type doesn't keep growing past readable |

**Common bugs:**
- Horizontal scroll caused by `100vw` plus padding (use `100%` or `min(100vw, 100% - 32px)`)
- Touch targets shrunk for desktop and never re-enlarged on mobile
- Grid that collapses awkwardly between breakpoints
- Hero text that wraps poorly mid-word
- Images that don't have responsive sources, slow on mobile

**Manual test:** open dev tools, resize the viewport from 320px to 2560px continuously. Watch what breaks.

---

## 2. Keyboard Navigation

Tab through every interactive element on every page.

**Check:**
- [ ] Every button, link, input is reachable via Tab
- [ ] Tab order matches visual order
- [ ] Focus is always visible (never `outline: none` without a replacement)
- [ ] Skip-link present at top of page for screen reader users
- [ ] Modals trap focus (you can't Tab out of an open modal)
- [ ] Modals return focus to the trigger when closed
- [ ] Esc closes modals/drawers
- [ ] Enter activates buttons; Space activates buttons; Enter follows links
- [ ] No keyboard traps (you can always Tab away)
- [ ] Custom widgets (carousels, dropdowns) have keyboard support

**Focus styles that work:**
```css
:focus-visible {
  outline: 2px solid var(--color-accent);
  outline-offset: 3px;
  border-radius: var(--radius-sm);
}
```

Or for a more refined treatment:
```css
:focus-visible {
  box-shadow: 0 0 0 3px var(--color-bg), 0 0 0 5px var(--color-accent);
  outline: none;
}
```

---

## 3. Screen Reader

Use VoiceOver (Mac: Cmd+F5), NVDA (Windows, free), or TalkBack (Android).

**Check:**
- [ ] Every page has a single H1
- [ ] Headings descend in order — H1 → H2 → H3, no skipping
- [ ] All landmarks present: `<main>`, `<nav>`, `<header>`, `<footer>`, `<aside>` if appropriate
- [ ] Images have meaningful alt text (or `alt=""` for decorative)
- [ ] Buttons have accessible names (text content or `aria-label`)
- [ ] Icon-only buttons have `aria-label`
- [ ] Form fields have `<label>` associated by `for=` attribute
- [ ] Error messages are programmatically associated with fields (`aria-describedby`)
- [ ] Loading states announce themselves (`aria-live="polite"`)
- [ ] Interactive elements that aren't `<button>` or `<a>` have appropriate `role`
- [ ] Carousels have controls and pause buttons
- [ ] Modals have `aria-modal="true"` and `aria-labelledby`

**Common screen-reader anti-patterns:**
- "Click here" link text
- `<div onclick=...>` without `role` and keyboard handler
- Toast notifications that don't announce
- Form errors that only show visually (red border)

---

## 4. Color Contrast

Use a contrast checker (WebAIM, Stark plugin, browser dev tools "Inspect" → "Accessibility" panel).

**Standards:**
- **WCAG AA** (minimum):
  - Normal text: 4.5:1
  - Large text (18pt+ or 14pt+ bold): 3:1
  - UI components and graphical objects: 3:1
- **WCAG AAA** (enhanced — aim here for body):
  - Normal text: 7:1
  - Large text: 4.5:1

**Check:**
- [ ] Body text on bg
- [ ] Muted/secondary text on bg
- [ ] Link text on bg (in default and visited states)
- [ ] Button text on button bg (default, hover, active, disabled)
- [ ] Icon colors against their backgrounds
- [ ] Form input text on input bg
- [ ] Placeholder text (often the violator)
- [ ] Error/success/warning text
- [ ] Text on top of images (use overlays if needed)
- [ ] Focus indicators against bg

**Don't ship `color: #ccc` placeholders or `#666` body on near-white. They look fine and fail.**

---

## 5. Motion

- [ ] `prefers-reduced-motion: reduce` actually reduces motion
- [ ] No motion that triggers vestibular issues (large parallax, fast spinning, flashing)
- [ ] Auto-playing animations have controls or pause on hover
- [ ] No content that flashes more than 3 times per second (seizure risk)
- [ ] Loading animations don't continue forever silently — fail states exist

Test with motion reduction enabled (Mac: System Settings → Accessibility → Display → Reduce motion).

---

## 6. Performance

Run Lighthouse (dev tools → Lighthouse panel) on Mobile and Desktop. Targets:

- **Performance**: 90+
- **Accessibility**: 95+
- **Best Practices**: 95+
- **SEO**: 95+

**Core Web Vitals:**
- **LCP** (Largest Contentful Paint): < 2.5s
- **CLS** (Cumulative Layout Shift): < 0.1
- **INP** (Interaction to Next Paint): < 200ms

**Common fixes:**
- Hero image too large → compress, serve modern formats (WebP/AVIF), responsive `srcset`
- CLS from images → set `width` and `height` attributes
- CLS from web fonts → use `font-display: swap` and set fallback metrics with `size-adjust`, `ascent-override`
- Render-blocking JS → defer non-critical scripts, inline critical CSS
- Long Tasks → break up heavy JS, use `requestIdleCallback` for non-essential work

**Image budget:** hero image < 200KB ideally, < 500KB max. If it's bigger, reduce dimensions or compress more.

**Font budget:** load only weights actually used. Subset to Latin if not multilingual. Use `unicode-range` for ranges you need.

---

## 7. Cross-Browser

Test on at minimum:

- **Chrome / Edge** (Chromium) — latest
- **Safari** — latest desktop AND mobile (iOS Safari is its own beast)
- **Firefox** — latest

**Common compat issues:**
- Safari and dialog/`backdrop-filter` — sometimes flickers; test
- Safari and `:has()` — supported but recent
- Safari date inputs render differently
- Firefox scrollbar styling needs `scrollbar-width` and `scrollbar-color`
- View Transitions API — Chromium and Safari 26+; provide fallback
- Container queries — supported everywhere stable, but be aware of initial render

---

## 8. Empty / Loading / Error States

For every place data is loaded or user input is required, design these states:

- **Empty** — first-time user, no data yet. Don't just show nothing — show a thoughtful illustration, a clear next action, and warm copy. ("No projects yet. Create your first one ↗")
- **Loading** — skeleton or refined progress indicator, NOT a default spinner
- **Error** — clear message, no jargon, recovery action. ("Something went wrong loading your dashboard. Retry ↗")
- **Success** — confirm what happened. Use sparingly — don't celebrate every save.
- **Partial** — when only some content loads. Show what you have, indicate what's pending.

These are often the first thing cut from designs and the most frequently encountered states in real use.

---

## 9. Forms

- [ ] All inputs have visible labels (not just placeholders)
- [ ] Required fields indicated visually AND in `required` attribute
- [ ] Validation messages helpful (not "Invalid input")
- [ ] Errors associated with fields via `aria-describedby`
- [ ] Inline validation runs on blur, not keystroke (less stressful)
- [ ] Submit button shows loading state during submit
- [ ] Successful submit gives clear feedback
- [ ] Form fields accept paste (don't disable autofill on email/password)
- [ ] Email inputs use `type="email"` and `inputmode`
- [ ] Telephone uses `type="tel"`
- [ ] Numbers use `inputmode="numeric"` (not `type="number"` for things like postal codes)
- [ ] Autocomplete attributes set (`autocomplete="given-name"`, etc.)

---

## 10. Dark Mode (if implemented)

If you built dark mode, every surface needs verification:

- [ ] Hero
- [ ] All section variants
- [ ] Buttons (default, hover, active, disabled)
- [ ] Inputs (default, focus, filled, error)
- [ ] Cards
- [ ] Modals & drawers
- [ ] Tables and data viz
- [ ] Charts (often forgotten — adjust colors)
- [ ] Logos with light-mode color → invert or swap
- [ ] Images that have white backgrounds → add bg-aware treatment
- [ ] Code blocks
- [ ] Embedded media (YouTube, Twitter — they have their own dark mode)
- [ ] Loading states
- [ ] Error/success states (red/green need adjustment for dark)

---

## 11. Touch / Gesture (mobile-specific)

- [ ] Touch targets ≥ 44×44px (Apple HIG) or 48×48dp (Material)
- [ ] No hover-only interactions — provide tap alternatives
- [ ] Swipe gestures (carousels, modals) work
- [ ] Pull-to-refresh doesn't fire accidentally
- [ ] iOS bounce scroll doesn't reveal awkward layout
- [ ] Mobile Safari address bar appears/disappears doesn't break full-height (use `100dvh` not `100vh`)
- [ ] Pinch-zoom not blocked (`user-scalable=yes` in viewport meta)
- [ ] Forms don't zoom on focus (set inputs to ≥ 16px font-size on mobile)

---

## 12. SEO Basics (if marketing site)

- [ ] `<title>` tag set per page, < 60 chars
- [ ] Meta description, < 160 chars, compelling
- [ ] Open Graph tags (`og:title`, `og:description`, `og:image`, `og:url`)
- [ ] Twitter Card tags (`twitter:card`, `twitter:image`)
- [ ] Canonical URL
- [ ] `<html lang="...">` set
- [ ] Semantic HTML used (don't `<div>` everything)
- [ ] Sitemap generated
- [ ] robots.txt sensible
- [ ] Structured data (JSON-LD) for relevant content (Article, Product, Recipe, etc.)
- [ ] Image `alt` text descriptive
- [ ] No content hidden from indexing accidentally

---

## 13. Print (if appropriate)

For long-form articles, recipes, documents — make print not look like a disaster:

```css
@media print {
  nav, footer, .ad, .sidebar { display: none; }
  body { font-size: 11pt; color: black; background: white; }
  a::after { content: " (" attr(href) ")"; font-size: 9pt; color: #555; }
  img { max-width: 100%; }
  h1, h2, h3 { page-break-after: avoid; }
  p { orphans: 3; widows: 3; }
}
```

---

## Reporting to the user

After testing, write a brief report:

```
**Testing report**

✅ Passing:
- Responsive across 360–2560px
- Keyboard nav clean, focus visible
- WCAG AA contrast on all body and UI text
- Lighthouse performance: 94 desktop, 89 mobile
- Dark mode verified across all surfaces

⚠️ Known issues:
- [issue 1, with what's needed to fix]
- [issue 2]

🐛 Fixed during testing:
- [things you caught and fixed in this round]
```

If you found issues you can fix, fix them before reporting (don't dump them on the user). Only call out things that need their input or that you've decided to defer.

If everything passes, say so plainly. Don't pad.
