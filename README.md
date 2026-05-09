# UI/UX Master — A Claude Skill for World-Class Redesign

Take any existing UI from average to world-class through a rigorous audit → redesign → test → iterate loop.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Skill version](https://img.shields.io/badge/skill-v1.0.0-111111.svg)](CHANGELOG.md)
[![For Claude Sonnet/Opus 4+](https://img.shields.io/badge/Claude-Sonnet%20%2F%20Opus%204%2B-d97706.svg)](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-2ea44f.svg)](CONTRIBUTING.md)

A Claude [skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) that turns Claude into a senior product designer for the duration of a redesign. It enforces a six-phase workflow — audit, domain study, direction, build, test, iterate — and refuses to stop at "good enough." Built for designers, engineers, and founders who want their interfaces to look like the top 10% of Awwwards, not a Bootstrap reskin.

## Table of contents

- [What this skill does](#what-this-skill-does)
- [Quick install](#quick-install)
- [The 6-phase workflow](#the-6-phase-workflow)
- [Domain coverage](#domain-coverage)
- [What's inside the skill](#whats-inside-the-skill)
- [Example before/after](#example-beforeafter)
- [Requirements](#requirements)
- [Build from source](#build-from-source)
- [Contributing](#contributing)
- [Roadmap](#roadmap)
- [License](#license)
- [Credits](#credits)

## What this skill does

- **Domain-aware design.** Cars get gauges, parallax car parts, and headlight glows; food gets steam, sizzle, and warm serif type; finance gets tickers and split-flap counters. The domain breathes through the design instead of being a generic "modern" template.
- **Modern technical patterns.** OKLCH color spaces, fluid `clamp()` typography, design tokens via CSS custom properties, container queries, scroll-driven animations, `view-transition` API, and a real dark mode that isn't just inverted colors.
- **Motion craft.** Tuned cubic-bezier curves, staggered choreography, micro-interactions on every state, plus a catalogue of domain-signature animations (steam, pulse, equalizer, line-draw, magnetic buttons).
- **Accessibility-first.** WCAG AA contrast as a floor, keyboard navigation tested, `prefers-reduced-motion` respected, focus-visible styled instead of removed.
- **Iterative refinement.** A built-in self-review pass identifies the two or three weakest moments after each iteration and rebuilds them. The skill won't stop on "thanks" — only on explicit shipping approval.
- **Rigorous testing.** A full QA checklist before the work is reported as done: responsive at 360–2560px, screen-reader pass, Lighthouse targets, cross-browser smoke test, designed empty/loading/error states.

Most AI redesigns produce a generic "modern" look that could be ported to any industry by changing the copy. This skill exists to close the gap between that and the level of intentionality, craft, and finish you'd expect from a senior design director at Apple, Linear, Stripe, or Vercel.

## Quick install

1. Download [`dist/ui-ux-master.skill`](dist/ui-ux-master.skill) — or grab it from the [latest release](https://github.com/MarwanAljijakli/UI-UX-master-skill-for-Claude/releases/latest).
2. Open Claude → Settings → Capabilities → Skills → Upload skill.
3. Drop in the `.skill` file. Done.

Then just say:

```
"Redesign my homepage to feel world-class — here's the current code: [paste]"
"Make this dashboard look like Linear or Vercel built it"
"Improve the UX of this car dealership site, add domain-relevant motion"
```

Claude will detect the redesign intent, load the skill, run the audit, and walk you through each phase.

## The 6-phase workflow

The skill enforces these phases in order. Each one earns its place — none are skippable.

1. **Audit** — Walk eleven design axes (typography, color, spacing, layout, motion, hierarchy, interactions, accessibility, responsiveness, performance signals, brand/domain fit) and produce a tight 5–10 line verdict before changing a single line of code.
2. **Domain study** — Load the matching playbook from 18+ domains (or derive a new one in three minutes) and pick two or three signature moves that the design will be built around.
3. **Direction** — Commit to one bold aesthetic identity (brutalist editorial, refined luxury, kinetic motion-first, glass and depth, etc.) and explain in one sentence why it fits the domain.
4. **Build** — Write production-grade code with modern craft standards: design tokens, fluid type, OKLCH palettes, choreographed motion, designed empty/loading/error states.
5. **Test** — Run the full QA checklist. Fix what fails. Report honestly — don't gloss over known issues.
6. **Iterate** — Brutally self-review. Pick the weakest two or three moments and rebuild them. Repeat until the work would stand up next to the top 10% of Awwwards or Dribbble.

The "don't stop too early" rule is explicit: a "thanks" or "looks good" without explicit shipping approval triggers another iteration offer. Fine is the enemy.

## Domain coverage

Eighteen built-in playbooks. Each lists the visual language, type and color discipline, motion principles, signature moves, and reference-quality examples for the domain.

| | | |
|---|---|---|
| Cars / Automotive | Food & Restaurants | Finance / Fintech |
| SaaS / B2B | E-commerce | Real Estate / Architecture |
| Healthcare / Wellness | Fitness / Sports | Music / Audio |
| Travel / Hospitality | Education / Learning | Gaming |
| News / Editorial | Fashion | Portfolio / Personal |
| Agency / Studio | Non-profit / Cause | Crypto / Web3 |

For domains not in the list, the skill derives a playbook on the fly using a seven-step framework (material audit, industry references, native motion, native iconography, tone calibration, signature moves, mood sentence).

New domain coverage is welcome — see the [contributing guide](CONTRIBUTING.md) for the playbook template.

## What's inside the skill

The skill ships as one progressive-disclosure entry point plus five reference modules that load on demand.

| File | Use it for |
|---|---|
| [`SKILL.md`](ui-ux-master/SKILL.md) | The orchestrator — workflow, mission, world-class bar, phase gates, stop conditions. |
| [`references/audit-framework.md`](ui-ux-master/references/audit-framework.md) | Phase 1 — eleven-axis audit checklist with red flags, examples, and the audit-summary output format. |
| [`references/domain-playbooks.md`](ui-ux-master/references/domain-playbooks.md) | Phase 2 — playbooks for 18+ domains plus a framework for deriving one from scratch. |
| [`references/design-systems.md`](ui-ux-master/references/design-systems.md) | Phase 4 — modern technical patterns: design tokens, fluid type, OKLCH color, layout, motion, dark mode, font pairings. |
| [`references/animation-library.md`](ui-ux-master/references/animation-library.md) | Phase 4 — copy-paste-ready animations with tuning notes: reveals, scroll-driven, marquee, magnetic buttons, page transitions, domain-signature motion. |
| [`references/testing-checklist.md`](ui-ux-master/references/testing-checklist.md) | Phase 5 — the full QA procedure with code snippets and reporting format. |

## Example before/after

Real-world redesign showcases live in [`examples/`](examples/README.md) and are coming soon. Want to contribute one? See [CONTRIBUTING.md](CONTRIBUTING.md) — submissions need the original site or code, the redesign output, screenshots or a recorded walkthrough, and a short writeup of the design choices made.

## Requirements

- **Claude model**: Sonnet 4 / Opus 4 or later. The skill is written for the current generation of Claude models and uses progressive disclosure across reference files.
- **Plan**: a paid plan (Pro, Max, Team, or Enterprise) — uploading custom skills is a paid-tier feature.
- **Surface**: works in the Claude web app, desktop apps (macOS/Windows), and mobile apps wherever the Skills feature is enabled. Also works in the Claude API and Claude Code via the [agent skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) system.

## Build from source

If you want to modify the skill or repackage from a clone:

```bash
git clone https://github.com/MarwanAljijakli/UI-UX-master-skill-for-Claude.git
cd UI-UX-master-skill-for-Claude
bash scripts/package.sh
```

That regenerates `dist/ui-ux-master.skill` with the current contents of `ui-ux-master/`.

## Contributing

Contributions are welcome. The three highest-leverage paths:

- **New domain playbooks** — propose a domain not yet covered (with reference-quality examples and signature moves).
- **New animation patterns** — framework-agnostic, CSS-first, with timing notes and a `prefers-reduced-motion` story.
- **Real before/after examples** — original code/URL, redesign output, design rationale, screenshots or video.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide and PR checklist.

## Roadmap

- Curated showcase of real-world before/after redesigns in `examples/`
- More domain playbooks contributed by the community (legal, B2B marketplaces, dev tooling, dating, kids/edtech)
- Video walkthrough of the six-phase workflow on a live redesign
- Automated eval suite that scores skill output on craft criteria
- Framework-specific companion presets (Tailwind config, shadcn/ui theme, Motion preset)

## License

[MIT](LICENSE).

## Credits

Authored by [Marwan Aljijakli](https://github.com/MarwanAljijakli). Built on the [Anthropic agent skills](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) framework.
