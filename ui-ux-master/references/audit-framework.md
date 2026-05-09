# Audit Framework

Use this when you're in Phase 1 of the UI/UX Master workflow. Walk every axis. Write a short verdict per axis. Don't skip any.

The point of the audit is not to be polite. It's to find the gap between what exists and what world-class would look like. Be specific. "Typography is bad" is useless. "Body text is Arial 14px on near-white background, hierarchy collapses below H2" is useful.

---

## 1. Typography

**Look at:**
- What fonts are loaded? Are they distinctive or default (Inter, Arial, Roboto, system)?
- Is there one display + one body, or one font everywhere?
- Hierarchy: how many type sizes? Do they form a scale? Do related sizes feel related?
- Line-height: tight on display (0.9–1.1), comfortable on body (1.5–1.7)?
- Letter-spacing: tighter on big sizes, looser on caps and small sizes?
- Optical adjustments: are huge headlines getting `letter-spacing: -0.04em`?
- Italics, weights — used purposefully or arbitrarily?
- Numerals: tabular for tables, proportional for prose?

**Red flags:**
- Inter or Roboto everywhere
- More than 4 font weights loaded that aren't being used distinctively
- Body text below 15px on mobile
- Display sizes that don't get tighter tracking
- Mixed type scales (16, 17, 19, 20, 22 — pick a system)

---

## 2. Color & Contrast

**Look at:**
- Is there a defined palette or are colors picked ad-hoc?
- How many *real* colors are doing work vs. how many shades of grey clutter the file?
- Contrast ratios: text vs. background. WCAG AA = 4.5:1 for body, 3:1 for large text.
- Accent discipline: one or two accents doing real signaling vs. five different "primary" colors?
- Dark mode: does it exist? Is it crafted, or just inverted?
- State colors: hover, focus, error, success — distinguishable?
- Brand color: present and felt, or buried?

**Red flags:**
- Purple-to-blue gradient on white (the AI-slop signature)
- Body text as `#666` on `#FFFFFF` (looks fine, fails contrast in some viewports)
- "Dark mode" that's just `background: #000` with no temperature, no depth
- 12 different greys that could be 3

---

## 3. Spacing & Rhythm

**Look at:**
- Is there a spacing scale (4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96)?
- Do related elements group tighter than unrelated ones?
- Vertical rhythm: do section spacings feel intentional?
- Padding inside components: consistent or random?
- Generous or cramped?

**Red flags:**
- Margins like 13px, 17px, 22px (no scale)
- Same gap between everything — no hierarchy of grouping
- Mobile screens with 8px edge padding (looks tight)
- Buttons with `padding: 10px 16px` everywhere regardless of weight

---

## 4. Layout & Composition

**Look at:**
- Grid: is there one? How many columns? Does content sit on it?
- Alignment: things lined up, or close-but-not-quite?
- Focal point: clear primary element?
- Scan path: where does the eye go? Is that the right place?
- Asymmetry: used to create energy, or accidental?
- White space: enough? Too much? Wrong distribution?

**Red flags:**
- Centered hero → 3-column features → testimonial → CTA (the template skeleton)
- Equal-weight elements competing for attention
- Misalignment by 1–4px (looks broken even if user can't articulate why)
- Mobile that's just desktop squished

---

## 5. Motion

**Look at:**
- What animates on page load?
- What responds to scroll?
- Hover, focus, active states on interactive elements?
- Transitions between routes / states / modals?
- Loading states — designed or default spinner?
- Timing and easing — feel crafted or default?

**Red flags:**
- Nothing moves
- Everything moves with `transition: all 0.3s ease`
- Fade-in on scroll for every element (overkill)
- No `prefers-reduced-motion` handling
- Loading = browser default spinner

---

## 6. Hierarchy

**Squint test:** blur your eyes. Can you still tell what's primary, secondary, tertiary? If it all reads at the same level, hierarchy has failed.

**5-second test:** in 5 seconds, can a stranger tell what this product does and what action they should take?

**Red flags:**
- Three CTAs of the same visual weight
- Body text larger than supporting headlines
- Decorative elements louder than content

---

## 7. Interactions

**Look at:**
- Buttons: hover, focus, active, disabled, loading — all designed?
- Inputs: empty, focused, filled, error, success?
- Links: distinguishable from body text? Underline strategy?
- Cards: hover effect that adds info or depth, or just shadow change?
- Drag, swipe, gesture — used where appropriate?
- Cursor: changed where appropriate? Custom where it would surprise?

**Red flags:**
- Buttons with no hover state
- Focus-visible removed (`outline: none` without replacement)
- Click targets below 44×44px on touch
- Links that look exactly like body text

---

## 8. Accessibility

**Look at:**
- Keyboard: can you complete every action with Tab, Enter, Space, Esc?
- Focus visible: at all times, on every interactive element?
- Tab order: matches visual order?
- Headings: H1, H2, H3 in hierarchy (not skipping levels)?
- Images: alt text present and meaningful (not "image of...")?
- Forms: labels associated with inputs (not just placeholder)?
- ARIA: used where native HTML can't carry the meaning, not as decoration?
- Color: is meaning ever conveyed by color alone?
- Motion: `prefers-reduced-motion` respected?
- Contrast: 4.5:1 minimum for body?

**Red flags:**
- `outline: none`
- Form fields with no `<label>`
- Images with `alt=""` for content images
- "Click here" link text
- Icons with no accessible name
- Carousel that auto-advances with no pause control

---

## 9. Responsive Behavior

**Test at minimum:**
- 360 × 640 (small phone)
- 768 × 1024 (tablet portrait)
- 1280 × 800 (laptop)
- 1920 × 1080 (desktop)
- 2560+ (large display — does it feel empty?)

**Look for:**
- Horizontal scroll (almost always a bug)
- Touch targets too small
- Type that reflows awkwardly
- Hover-only interactions on touch devices
- Images that don't have responsive sources
- Layout shifts when content loads

---

## 10. Performance Signals

Without running Lighthouse, you can spot:

- Hero image > 500KB (likely)
- Multiple font weights loaded, only some used
- Animations that retrigger layout (animating `top/left` instead of `transform`)
- 5+ render-blocking external scripts in `<head>`
- No image lazy-loading
- Web fonts with no `font-display: swap`
- Animations running off-screen

When in doubt, run Lighthouse and report the results.

---

## 11. Brand & Domain Fit

**The question:** if you remove all the text, can a designer tell what kind of product this is from the visual language alone?

**Audit:**
- Is the visual language specific to the domain or generic?
- Do illustrations, icons, photography all share a style?
- Does the motion language fit the subject? (slow elegant for luxury, kinetic for sports, organic for wellness)
- Is there a memorable signature moment?

**Red flags:**
- Could ship this to any industry by changing copy
- Stock illustrations that don't match the photography style
- Icons from three different libraries
- Animation language fights the brand tone

---

## Output format

After walking the axes, produce a brief audit summary for the user. Format:

```
**Audit summary**

What's working:
- [1–2 honest positives]

What needs work:
- Typography: [verdict]
- Color: [verdict]
- Motion: [verdict]
- Hierarchy: [verdict]
- Domain fit: [verdict]
- [other axes worth calling out]

Biggest opportunity:
[One sentence on the highest-leverage change.]

Before I rebuild — anything you want me to keep, anything you want me to throw away?
```

Keep it tight — 8–12 lines total. The user doesn't need a dissertation; they need to know you saw what they saw and that you have a plan.
