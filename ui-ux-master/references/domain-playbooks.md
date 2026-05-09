# Domain Playbooks

Use this in Phase 2 of the workflow. Find the domain that matches the user's project. Read its playbook. Pick 2–3 signature moves to execute. If the domain isn't here, derive a playbook using the framework at the bottom of this file.

The point: world-class design speaks the language of the subject. Generic "modern" looks the same across industries. We don't ship that.

---

## Cars / Automotive

**Visual language**: sleek, metallic, kinetic, precise. Chrome, glass, deep paint colors, machined surfaces.

**Type**: a tight modern grotesk (think Söhne, Neue Haas Grotesk, GT America) for body. A condensed display for hero — automotive press copy is often condensed. Italics rare; uppercase tracked-out for section labels.

**Color**: deep blacks (`#0A0A0A` not `#000000`), graphite greys, brushed-metal silvers, one signature accent (racing red, electric blue, or a brand-specific color).

**Signature moves:**
- Hero with a car driving across the viewport, or a slow rotational 3D model
- Parallax car parts on scroll — wheel turning, doors revealing
- Animated speedometer, tachometer, or RPM gauges as data viz
- Headlight glow on hover for cards
- Tire-tread patterns or carbon-fiber textures as decorative borders
- Gear-shift transitions between sections (a `.snap` mechanic with an animation that feels like a gearshift)
- Spec callouts that count up like a digital dashboard
- Aerodynamic line trails on cursor or scroll

**Motion principles**: fast, decisive, mechanical. `cubic-bezier(0.65, 0, 0.35, 1)` (in-out-cubic) or custom. Avoid bouncy springs — cars are precision machines.

**Reference quality**: Porsche, Tesla, Lucid Motors, Polestar configurator pages.

---

## Food & Restaurants

**Visual language**: warm, sensual, appetite-triggering. Light is everything — golden hour, soft shadows, depth of field.

**Type**: a high-contrast serif for display (Playfair, Canela, GT Sectra) signals craft. A clean sans for body. Script fonts only with extreme care — usually a trap.

**Color**: warm neutrals (cream, bone, terracotta, olive), one rich accent (deep burgundy, mustard, forest green). Avoid: pure white backgrounds, cold blues.

**Signature moves:**
- Animated steam rising from hero image (CSS or SVG `<animate>`)
- Ingredients flying in on load with stagger
- Recipe step transitions that feel like flipping a cookbook page
- Sizzle/bubble micro-animations on CTAs
- Hover that "plates" — image zooms slightly, garnish appears
- Menu sections that scroll horizontally like a tasting flight
- Hand-drawn illustrations for ingredients
- Slow ken-burns on hero photography

**Motion principles**: warm, slow, organic. Ease curves with longer outros. Things should feel like they're being plated, not served.

**Reference quality**: Eleven Madison Park, Noma, Atomix, Yelo (any high-end restaurant site).

---

## Finance / Fintech / Investing

**Visual language**: data-dense, precise, trustworthy, kinetic energy from the markets.

**Type**: monospace for numbers (JetBrains Mono, Söhne Mono, IBM Plex Mono). A serious sans for body (Söhne, Aktiv, Inter as a last resort but better). Tabular numerals everywhere.

**Color**: ink-blacks, paper-whites, one institutional accent (deep green, navy, or a rare earned color). Up/down red and green need to be tuned — default red/green is loud and triggering. Use muted, accessible variants.

**Signature moves:**
- Live ticker tape header
- Animated candle/line charts that build on scroll
- Number counters that flip like a stock board (split-flap animation)
- Gradient meshes that pulse with market data
- Data tables with restrained zebra striping and excellent typographic care
- Hover on charts that reveals tooltips with actual craft
- Section transitions that feel like trade execution

**Motion principles**: precise, fast, data-driven. Numbers updating should feel like trades, not like decoration.

**Reference quality**: Stripe, Mercury, Ramp, Brex, Bloomberg Terminal (for density inspiration).

---

## SaaS / B2B Software

**Visual language**: clear, confident, technically credible, slightly opinionated.

**Type**: a distinctive grotesk (avoid Inter — overused). Söhne, GT America, Neue Haas Grotesk, Söhne Buch, or something fresh from Pangram, Grilli Type, Klim.

**Color**: dark mode by default for product, light mode for marketing — or pick one and own it. One bold accent. Use color to signal product capability hierarchy.

**Signature moves:**
- Product UI shown in motion, not as a static screenshot
- Scroll-driven product story (feature → motion → outcome)
- Live-feeling demo embedded in the hero
- Customer logos that aren't a generic grey wall — animate them, group them, give them context
- Pricing table with a thoughtful highlight/comparison animation
- Doc-style code blocks with syntax highlighting that's actually pretty
- Subtle grid background or dot grid for technical credibility

**Motion principles**: quick, considered, productive. Nothing should waste the user's time.

**Reference quality**: Linear, Vercel, Stripe, Resend, Liveblocks, Cal.com, Arc.

---

## E-commerce

**Visual language**: product is hero. Photography quality determines the ceiling.

**Type**: depends on category. Luxury → high-contrast serif. Streetwear → bold sans / brutalist. Outdoor → utilitarian sans. Beauty → editorial mix.

**Color**: derived from the product photography. Let the products dictate the palette.

**Signature moves:**
- Product hero with hover-to-reveal alternate angle
- Quick-view modal that doesn't break flow
- Color/variant swatches with smooth transitions
- Add-to-cart with a small reward animation (the item flying to the cart icon)
- Sticky size/cart panel on PDP that doesn't feel intrusive
- Editorial-style storytelling sections, not just product grids
- Image zoom on hover with cursor-follow
- Lookbook sections with parallax

**Motion principles**: tactile. Picking, holding, examining the product. Not flashy — confident.

**Reference quality**: SSENSE, MR PORTER, Aimé Leon Dore, Glossier, Aēsop.

---

## Real Estate / Architecture

**Visual language**: spacious, architectural, photographic, calm.

**Type**: refined serif or a quietly confident sans. A lot of generous whitespace.

**Color**: very restrained. Photography drives color. Add: deep ink, paper, one warm earth accent.

**Signature moves:**
- Parallax architectural sections with slow vertical scrolling
- Floor-plan reveals with line-drawing animations (SVG `stroke-dashoffset`)
- Room walkthroughs as scroll-triggered carousels
- Blueprint-line illustrations as decorative elements
- Maps with custom-styled markers (not default Google red pins)
- Image galleries with full-bleed layouts
- Slow ken-burns on hero photography

**Motion principles**: slow, considered, architectural. Like walking through a building.

**Reference quality**: The Boundary, Frank Lloyd Wright Foundation, high-end architecture firm sites.

---

## Healthcare / Wellness / Medical

**Visual language**: calm, clean, trustworthy, human. NOT sterile-corporate.

**Type**: a humanist sans (FF Mark, Söhne, Maison Neue) — readable, warm. Avoid clinical or aggressive type.

**Color**: soft palette — sage, cream, warm white, deep navy or forest green as anchor. Avoid stark medical white-on-blue.

**Signature moves:**
- Pulse / heartbeat animations used very sparingly
- Soft organic shapes (blobs) as section dividers
- Scroll-triggered reveals that feel breath-paced
- Real human photography, not stock
- Educational diagrams with hover annotations
- Calm onboarding flows with progress that doesn't feel clinical
- Generous whitespace — this is a category that needs to feel like it's not rushing you

**Motion principles**: slow, breathing, gentle. Long ease-outs. Nothing snaps.

**Reference quality**: Headspace, Calm, Nurx, One Medical, Eight Sleep.

---

## Fitness / Sports

**Visual language**: kinetic, intense, athletic, performance-driven.

**Type**: bold condensed display (Anton, Druk, Tungsten). Strong sans for body. Italics earn their place here.

**Color**: high contrast — black, white, electric accent (volt green, neon orange, hot pink). Brand color hits hard.

**Signature moves:**
- Heart-rate pulse animations
- Rep counters that count up
- Motion-trail effects on imagery (like sports photography motion blur)
- Muscle-group highlights on hover (anatomical illustration)
- Action-shot photography with kinetic crops
- Stats that animate dramatically
- Diagonal cuts and angled sections

**Motion principles**: fast, hard-hitting, athletic. Snap-cuts. Quick fades. Energy.

**Reference quality**: Nike, Whoop, Hyrox, Tonal, Strava editorial pages.

---

## Music / Audio

**Visual language**: rhythmic, atmospheric, sensory.

**Type**: ranges wildly by genre. Classical → elegant serif. Electronic → kinetic display. Indie → bespoke grotesk.

**Color**: atmospheric. Often dark mode default with gradient washes that feel like stage lighting.

**Signature moves:**
- Waveform dividers between sections
- Beat-synced animations (when an audio track plays)
- Vinyl-spin loaders
- Equalizer bars as data viz / hover effects
- Album art with hover-zoom and color-extraction backgrounds
- Sticky now-playing bar with thoughtful design
- Visualizer canvas backgrounds in hero

**Motion principles**: rhythmic. Things should feel like they could move with music — even when there's no music playing.

**Reference quality**: Resident Advisor, Pitchfork, Bandcamp, Apple Music marketing pages, NTS Radio.

---

## Travel / Hospitality

**Visual language**: aspirational, photographic, atmospheric, place-specific.

**Type**: a confident serif (or distinctive sans) that signals destination quality. Editorial pacing.

**Color**: derived from destination photography. Earth tones for Africa, blues for Mediterranean, etc.

**Signature moves:**
- Full-bleed photography with slow ken-burns
- Map-driven navigation with custom map styling
- Itinerary timelines as visual scroll experiences
- Property cards with multi-image hover
- Currency / language selectors that feel like an artifact, not an afterthought
- Departure/arrival animations on booking flows
- Section transitions that feel like turning pages of a passport

**Motion principles**: dreamlike, slow, transportive.

**Reference quality**: Airbnb, Aman, Six Senses, Soho House, Atlas Obscura.

---

## Education / Learning

**Visual language**: clear, encouraging, progress-oriented, not childish.

**Type**: highly readable sans for body. Personable serif or display for emotional moments.

**Color**: warm primary, encouraging accents. Avoid corporate-LMS palette.

**Signature moves:**
- Progress visualization that motivates
- Interactive diagrams on hover/click
- Lesson cards with completion states designed (not just checkmarks)
- Streak counters with personality
- Code editor / interactive widgets embedded in content
- Animated illustrations of abstract concepts
- Confetti/reward moments on completion (used sparingly)

**Motion principles**: encouraging, responsive, never patronizing. Reward state changes thoughtfully.

**Reference quality**: Duolingo (motion), Brilliant, Scrimba, Khan Academy, Skillshare.

---

## Gaming

**Visual language**: immersive, kinetic, atmospheric, world-building.

**Type**: bold display fonts that feel like the game's universe. Often custom or game-engine-derived.

**Color**: dramatic, often dark mode with strong accents. Atmospheric.

**Signature moves:**
- Full-screen video hero looping
- Scroll-driven cinematics
- Character/weapon detail viewers (3D rotation)
- Stat radial diagrams animated
- HUD-inspired UI elements (subtle)
- Hover effects with glitch / shader feel
- Particle systems in backgrounds

**Motion principles**: cinematic, dramatic, world-driving. Take risks others wouldn't.

**Reference quality**: Riot Games, PlayStation, Bungie, Larian Studios.

---

## News / Editorial / Magazine

**Visual language**: typographic, hierarchical, content-first.

**Type**: editorial pairings. A serif workhorse (Tiempos, Lyon, Caponi) for body. A distinctive display for headlines.

**Color**: paper, ink, one editorial accent. Restrained by tradition, but the best magazine sites push it.

**Signature moves:**
- Drop caps on article opens
- Pull quotes as typographic moments
- Reading progress indicator (subtle, not the candy-bar at the top)
- Related-articles modules that feel curated, not algorithmic
- Image captions designed (not afterthoughts)
- Multi-column long-form on desktop
- Section dividers as typographic ornaments

**Motion principles**: paper-paced. Page turns. Editorial calm.

**Reference quality**: The New York Times, The Atlantic, The Guardian, Are.na, Pitchfork, Wallpaper.

---

## Fashion

**Visual language**: editorial, bold, photo-driven, distinctly opinionated.

**Type**: ranges from brutalist (Margiela aesthetic) to refined editorial. Always confident.

**Color**: photo-driven. Often monochrome. When color appears, it's a statement.

**Signature moves:**
- Full-bleed editorial photography
- Lookbook scrolls (horizontal or full-screen vertical)
- Product cards with hover-to-reveal model shot
- Marquee text with running tickers
- Type-as-image (huge type that becomes graphic)
- Color-block transitions
- Sound on hover (very rare, used by Off-White etc.)

**Motion principles**: editorial confidence. Slow when refined, kinetic when streetwear.

**Reference quality**: SSENSE, Margiela, Acne Studios, Nike SNKRS, Bottega Veneta.

---

## Portfolio / Personal

**Visual language**: personal, distinctive, opinionated. The most freedom, the highest bar — this IS the design.

**Type**: do something specific. Variable fonts being animated. Custom type. Type-as-art.

**Color**: pick a stance. Two-color brutalist? Full-color maximalist? Monochrome luxury?

**Signature moves:**
- A signature interaction the visitor will remember
- Cursor that does something
- Hover on project cards that feels like a real reveal
- About section that has personality, not corporate boilerplate
- Process / case studies as scroll experiences
- Easter eggs

**Motion principles**: do whatever serves the personality. This is where ambition wins.

**Reference quality**: Awwwards Site of the Year, Bruno Simon, Olivier Larose, Studio for the Whole Could.

---

## Agency / Studio

**Visual language**: meta-design — you're showing you can design by designing the site about it.

**Type**: distinctive. Often custom or boutique foundry (Klim, Pangram, Grilli Type, Optimo).

**Color**: a strong stance. Usually high-contrast.

**Signature moves:**
- Marquee with current projects scrolling
- Case studies with full-bleed visual treatment
- About / team section that feels human
- Cursor follower that changes per section
- Section transitions that demonstrate motion craft
- Animated logos / wordmark
- Sound design (sparingly)

**Motion principles**: prove your craft. Every transition is your CV.

**Reference quality**: Locomotive, Active Theory, Hello Monday, Studio Lumio, &Walsh, Pentagram.

---

## Non-profit / Cause

**Visual language**: human, urgent (when needed), credible, photographic.

**Type**: humanist, readable, with editorial moments for stories.

**Color**: warm, human. Avoid corporate-NGO palette (royal blue + white = lifeless).

**Signature moves:**
- Real photography of real people, well-shot
- Story-driven scroll experiences
- Impact stats that animate meaningfully
- Donation flows designed (not Stripe-default)
- Map of impact with custom styling
- Quote moments designed as type
- Quiet motion that respects the gravity of the topic

**Motion principles**: respectful. Never gimmicky. Motion serves the story.

**Reference quality**: charity:water, Pencils of Promise, Watsi, ProPublica.

---

## Crypto / Web3

**Visual language**: a moving target — has been everything from cyberpunk maximalism to refined fintech. The best now lean refined fintech with one signature move.

**Type**: mono accents, distinctive sans. Numbers tabular.

**Color**: dark mode default. One signature accent. Avoid the rainbow gradient trap.

**Signature moves:**
- Live data (gas, prices, network status)
- Wallet-connect flows with thoughtful states
- Transaction visualizations
- Network graph backgrounds (subtle)
- Token/NFT reveals
- Data-dense without feeling chaotic

**Motion principles**: precise, data-driven. Avoid the "matrix code rain" cliché.

**Reference quality**: Uniswap, Optimism, Arc, Phantom, Linea.

---

## Deriving a playbook for a new domain

If the project is in a domain not covered above, build a playbook in 3 minutes:

**Step 1 — Material audit.** What does this thing physically look, sound, smell like? What's its native texture?

**Step 2 — Industry references.** Find 5 best-in-class examples in the domain. Note: typography, color discipline, motion language, signature moves.

**Step 3 — Native motion.** What naturally moves in this domain? (Cars drive. Charts grow. Food steams. Buildings stand still — so what's the motion equivalent? Light moving across them.)

**Step 4 — Native iconography.** What's the visual shorthand for this category?

**Step 5 — Tone calibration.** Serious, playful, urgent, calm, luxurious, accessible? Pick.

**Step 6 — Pick 2–3 signature moves.** Don't try to do all of them.

**Step 7 — Build the moodboard mentally.** If you opened the homepage, what's the *first impression*? Write that sentence. Now design to it.
