# Contributing

Thanks for considering a contribution. This skill gets sharper every time someone adds a domain, tunes an animation, or shares a real before/after. The goal of this guide is to make those contributions easy to land.

The skill itself (`ui-ux-master/SKILL.md` and the `references/*.md` files) is the product. Everything else in the repo exists to ship and document it. When contributing, default to small, focused PRs rather than sprawling refactors.

## Three contribution paths

### 1. Add a new domain playbook

Domain playbooks live in [`ui-ux-master/references/domain-playbooks.md`](ui-ux-master/references/domain-playbooks.md). They follow a consistent structure so that the skill can load them quickly and the user can scan them. Use this template:

```markdown
## <Domain name>

**Visual language**: <one or two sentences capturing the material qualities — sleek/metallic, warm/sensual, data-dense/precise, etc.>

**Type**: <type pairing recommendation — display + body — with named typefaces, not "use a serif".>

**Color**: <palette discipline — backgrounds, neutrals, the one or two earned accents. Call out anti-patterns to avoid.>

**Signature moves:**
- <2–5 specific signature interactions or visual treatments unique to this domain>
- <prefer concrete moves over generic "add animations">

**Motion principles**: <one or two sentences on the motion language — fast/decisive, slow/breathing, kinetic/snap-cut.>

**Reference quality**: <3–5 best-in-class examples in this domain so contributors and users have a calibration target.>
```

Look at the `Cars / Automotive`, `Finance / Fintech`, and `Music / Audio` entries in the existing playbook for examples that meet the bar.

A good playbook:

- Names specific typefaces (not "a clean sans"), specific motion timings or curves, and specific reference sites.
- Pulls from the material reality of the domain — what does this thing physically look like, sound like, move like.
- Lists 2–5 signature moves, not 15. The user should pick from these, not be overwhelmed by them.
- Calls out anti-patterns — the things that show up in bad designs in this domain (purple-to-blue gradients on white in fintech, royal-blue-and-white in non-profit, default red pins on real-estate maps).

If you're unsure whether a domain is distinct enough to deserve its own playbook, open a [new-domain issue](https://github.com/MarwanAljijakli/UI-UX-master-skill-for-Claude/issues/new?template=new_domain_playbook.md) first to discuss.

### 2. Add an animation pattern

Animation patterns live in [`ui-ux-master/references/animation-library.md`](ui-ux-master/references/animation-library.md). Patterns must be:

- **Framework-agnostic by default.** CSS-first, with optional JS for interactions that genuinely need it (`IntersectionObserver`, magnetic buttons, custom cursors). React/Motion examples are fine as a secondary block when the pattern demands it.
- **Tuned, not slop.** Document the easing function, duration, stagger amounts, and what to change for different aesthetics (longer/slower for luxury, snappier for tech). Defaults like `transition: all 0.3s ease` are not patterns — they're the absence of one.
- **Accessibility-aware.** Every pattern must respect `prefers-reduced-motion: reduce` and provide a tasteful static state, not just disabled motion.
- **Performance-aware.** Animate `transform` and `opacity` only. Pause off-screen. Throttle scroll handlers or prefer scroll-driven CSS animations where possible.

A good pattern entry includes a short rationale ("use this when…"), the code, and any tuning notes.

### 3. Submit a real before/after example

Before/after showcases live in [`examples/`](examples/README.md). Submissions need:

- **The original** — a public URL or a code snippet of the starting point. If neither exists, screenshots and a description are acceptable.
- **The redesign** — the output Claude produced when given the original through this skill. Include the prompts you used and any iteration rounds.
- **A writeup** — 200–500 words on the audit findings, the direction chosen and why, the signature moves picked, and what changed during iteration.
- **Screenshots or a recorded walkthrough** — at minimum hero, key sections, and one interaction in motion. Video is even better.

Don't ship identifying screenshots from clients without permission. Public marketing pages and your own work are fair game.

## Local setup

```bash
git clone https://github.com/MarwanAljijakli/UI-UX-master-skill-for-Claude.git
cd UI-UX-master-skill-for-Claude
bash scripts/package.sh
```

This regenerates `dist/ui-ux-master.skill`. To test your changes, upload that file to Claude (Settings → Capabilities → Skills) and run a redesign prompt that exercises whatever you changed.

The packaging workflow runs automatically on every PR — your changes will be validated and packaged into a downloadable artifact you can grab from the workflow run page.

## PR checklist

Before opening a PR:

- [ ] Title follows [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `docs:`, `chore:`, `ci:`).
- [ ] PR description explains the motivation — what gap this fills and how you decided on the approach.
- [ ] No breaking changes to the six-phase workflow in `SKILL.md` without prior discussion in an issue.
- [ ] Any new code patterns respect accessibility (`prefers-reduced-motion`, focus visible, contrast).
- [ ] Ran `bash scripts/package.sh` locally and verified the resulting `.skill` opens cleanly in Claude.
- [ ] If touching a reference file, ran the testing checklist mentally against your changes — would they pass it?

## Commit style

Conventional Commits, scoped to the area touched:

- `feat: add gaming domain playbook`
- `fix: correct stagger timing in word-by-word reveal`
- `docs: clarify install steps for desktop app`
- `chore: bump GitHub Actions to v5`
- `ci: add yaml validation step`

## Code of Conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md) version 2.1. By participating, you agree to uphold it.
