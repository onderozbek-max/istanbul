# Son Durak: Product Decisions & Principles

> **Status:** Draft v0.1 · 2026-11-08 · Owner: Onder
> **Scope:** Product, design, tech and business decisions. The story lives in
> [narrative.md](narrative.md); this doc only references it (DRY).

---

## 1. One-liner

**A story-driven survivor-like set in a zombie-overrun Istanbul.** It plays like Survivor.io
but feels like a Turkish dizi: a squad you care about, a real route across real neighborhoods,
and cliffhangers that bring players back.

## 2. Why this, why now

- **Demand:** mobile gaming is very common among young Turks, and Istanbul is one of the
  world's mobile-game capitals (Peak, Dream Games, Rollic, Spyke...).
- **Gap:** no strong game uses Istanbul as a setting. Turkish studios build placeless global games.
- **Different from the competition:** survivor-likes look and feel interchangeable. Very
  few have characters, story or polished animation.
- **Expansion engine:** the story moves across Turkey (İzmir in Ch. 3), and the tech is
  built for other cities (Athens and others, see §13).

### The uncomfortable truth (and the fix)
Turkey has **low revenue per user** (lira depreciation, regional pricing, low ad rates).
A Turkey-only game can get lots of downloads and earn little.
**Fix: Istanbul flavor, global appeal.** Three audiences:

| Audience | Why | What they need |
|---|---|---|
| Turkish players (13–30) | Volume, word of mouth, TikTok | Local jokes, Turkish VO, recognizable streets |
| Turkish diaspora (Germany ~3M, NL, AT...) | Higher spend, nostalgia | German/English UI, the same local soul |
| Global survivor-like / zombie fans | Biggest market | Universal visual humor, story, polish |

## 3. Product Pillars

Every feature has to support at least one pillar. If it supports none, cut it.

1. **Local soul, universal delivery.** Real places, real food, real humor that still lands
   without subtitles.
2. **Story is the differentiator.** Characters, bonds and cliffhangers are features, not decoration.
3. **Polish where the eyes are.** Spend quality on the heroes, game feel and story scenes,
   not on zombie #347.
4. **One game, every phone.** Same gameplay on a budget Android and a flagship; only the visuals scale.
5. **Data decides.** Release timing, difficulty and economy are tuned from live metrics
   through remote config.
6. **Solo-sized scope.** Built by one AI-assisted builder. YAGNI is policy, not advice.

---

## 4. Core Game Design

### Core loop
`Pick level → auto-attack survivor run (5–10 min) → level-up skill picks → boss →
loot & story beat → upgrade squad / weapons / vehicle → next level`

### Base genre (keep what works)
- One-thumb movement, automatic attacks, a choice of 3 random skills on each level-up.
- Short runs, bosses every 10 levels, persistent upgrades between runs.

### Our differentiators
| # | Feature | Why it matters |
|---|---|---|
| D1 | **Squad with tag-switch:** swap control between heroes mid-run; the others fight automatically | Role variety, more of every hero on screen |
| D2 | **Distinct hero roles:** tank (Kaan), speedster (Defne), versatile (Emre), ranged/support (Lale) | Reasons to invest in everyone |
| D3 | **Vehicle levels:** scooter (Ch. 2), car (Ch. 3), with a garage/upgrade meta | Pace changes; makes the "toolkit" story real |
| D4 | **Human enemies fight differently:** cover, flanking, loot theft vs. zombie swarms | Same controls, new tactics |
| D5 | **Interactive scenery:** simit carts, tea glasses, gas canisters, the döner skewer | Local flavor through gameplay |
| D6 | **Day/night cycle:** day = scavenging and humans, night = zombie horror | Variety and atmosphere |
| D7 | **Bond system:** bonds unlock combo ultimates (see narrative.md, *Romance & Branching*) | Story choices with gameplay payoff |
| D8 | **Street cats as early warning:** they hiss near zombies; collectible cosmetic cats | Shareable, globally loved, monetizable |
| D9 | **Survival resource per chapter:** none → battery charge → fuel | Each chapter feels new without new systems |

### Characters (stats summary; personalities in narrative.md)
| Hero | HP | Speed | Damage | Unique |
|---|---|---|---|---|
| Emre | Mid | Mid | Mid | Spec in any direction; hacking and crafting |
| Kaan | High | Low | High | Ground Slam; draws aggro |
| Defne | Low | Very high | Mid | Dash strikes; kiting |
| Lale | Low | Mid | Mid (ranged) | *Calm* aura slows zombies (also a story clue) |

---

## 5. Content Structure

- **Chapter = 100 levels = 10 districts × 10 levels.** *(Decision D-001)*
- Level x5 = mini-boss, level x0 = district boss + major story beat.
- **Solo-builder rule:** 100 levels are *assembled* from reusable parts, not hand-crafted
  one by one: `district map × wave script × modifier (night, fog, horde, human ambush) × boss`.
  About 10 maps per chapter, 30–40 wave scripts, ~10 modifiers.
- Story beats every 2–4 levels (motion-comic panels, banter, letters).

## 6. Chapter Release & Gating Policy *(Decision D-002)*

**Intent (Onder):** unlock the next chapter once ~5% of players reach the end of the current one.
**Adopted version (with safeguards):**

1. **Production is never the gate.** Chapter N+1 is finished and tested *before* the trigger
   can fire. The gate is about pacing, not about buying build time.
2. **Count the right players.** The trigger counts *qualified active players*: reached
   level 10 **and** active in the last 28 days. Not total installs.
3. **Trigger:** the next chapter unlocks when **5% of qualified active players** have
   reached the chapter's final level, **or** when the **first 1% of finishers have waited
   21 days**, whichever comes first.
4. **Make the wait public:** an in-game community progress bar
   (*"Survivors who reached Ataköy: 3.2% / 5%"*). Unlock day becomes a marketing event.
5. **Finishers always have something to do:** the endgame (§7) is live before Chapter 1 ships.
6. **Everything is tunable:** the threshold %, the qualifying rules and the max wait live in
   remote config. They change without an app update.
7. **Know the trap:** difficulty and gear tuning set the pace, so check the actual
   level-funnel data before trusting any fixed %.

## 7. Endgame (for players waiting on the next chapter)

- **Night Shift:** an endless survival mode with weekly leaderboards.
- **Hard Mode:** replay finished districts with modifiers and better loot.
- **Weekly events:** light, playful local themes (e.g., "Simit Rush", "Ferry Panic").
  No religious holidays or political dates as event themes.
- **First Arrivals badge** for early finishers; status matters to superfans.

---

## 8. Quality & Performance *(Decision D-003)*

**Principle:** quality tiers, not lowest-common-denominator art. High-end phones get the
premium version; budget phones get a lighter one. **Gameplay is identical on every tier.**

| Scales by tier (visual only) | Never scales (gameplay) |
|---|---|
| Texture resolution, render resolution | Enemy count and spawn timing |
| VFX/particle density, post-processing, shadows | Hitboxes, speeds, damage |
| Animation detail at a distance | Level layouts, difficulty |
| Corpse persistence, decals, ambient props | Rewards and economy |

**How:**
- **Enemies are cheap by design:** GPU instancing or sprite batching, simple shaders,
  distant LOD. Enemy count is tuned so it runs on the low tier, and the visuals scale up from there.
- **Heroes get the premium budget:** full animation sets, hit reactions, personality idles.
- **Game feel is mostly free:** hit-stop, screen shake, knockback, punchy death animations, audio.
- **Auto-detect the tier on first launch,** and let players override it in settings.
- **Keep the download small:** base install < 150 MB. HD assets download after install,
  only on capable phones (Play Asset Delivery / iOS On-Demand Resources).
- **Performance budgets:** low tier 30 fps steady on a ~3 GB RAM Android; high tier 60 fps.
  Tested on real devices, every milestone.
- **Cost to remember:** every tier multiplies QA. Ship with **3 tiers max** (Low / Mid / High).

## 9. Art, Animation & Audio Direction

- **Style:** 2D, top-down 3/4, hand-painted environments + ink-outlined characters (D-007).
  Details: design-system.md. Final direction picked from style frames (execution-plan.md M4).
- **Story presentation:** **motion comics** (animated comic panels) instead of 3D cutscenes.
  Cheap, AI-art-friendly, stylish, and they read like a dizi.
- **Signature move:** the dizi cliffhanger (freeze frame, triple zoom across faces, strings).
- **Voice:** Turkish VO for key scenes and cliffhangers first (Turkey has a strong dubbing
  culture); English/German subtitles and later VO.
- **Music:** modern beats mixed with ney, bağlama and darbuka. Check licensing on every
  AI-generated track.
- **Consistency is the hard part:** train a custom style model (e.g., Scenario) on approved
  art and generate everything through it.

## 10. Monetization

- **Rewarded ads:** revives, double loot, extra skill reroll. Always optional.
- **Season pass ("Survivor Pass"):** cosmetics plus upgrade materials, refreshed per event cycle.
- **Cosmetics:** hero outfits, scooter/car skins, **cats**.
- **Starter / chapter packs:** clear-value bundles, priced regionally.
- **Regional pricing:** Turkish lira pricing set deliberately; diaspora markets priced locally.
- **Avoid early:** paid random loot (gacha). Turkey is strict on gambling, stores require
  published odds, and it hurts trust. Revisit only with legal review.
- **No hard energy walls** in the first 30 levels. Retention first, monetization second.

## 11. Architecture & Tech

- **City-as-data (open/closed principle):** every place-specific asset (districts,
  bosses, NPCs, food, landmarks, music, factions, strings) lives in a **content pack**
  (data + assets). The engine knows nothing about Istanbul. New city = new pack, no engine changes.
- **Engine: open decision (D-004).** Lean **Godot 4** (text-based scenes and scripts are
  easy for AI agents to edit). **Week-1 stress test:** 500 enemies at 30 fps on a low-end
  Android. If Godot fails, or its ad/IAP plugins are too immature, switch to **Unity 6**.
- **Backend:** Firebase (analytics, Crashlytics, Remote Config, A/B tests). No custom server
  for v1.
- **Payments & ads:** RevenueCat (IAP), AppLovin MAX or AdMob (mediation).
- **Save data:** local + cloud save (Play Games / Game Center).

### Toolchain (solo AI builder)
| Need | Tool |
|---|---|
| Coding | Code Puppy / Cursor / Claude Code |
| Art | Scenario (custom style model), Midjourney, Recraft; Aseprite/Krita for cleanup |
| Animation | Spine or Rive (2D), Mixamo + Blender (if 3D) |
| Audio | Suno/Udio (music), ElevenLabs (SFX, temp VO), human VO for key scenes |
| Localization | AI translation + native reviewers (TR, EN, DE; later EL, AR) |
| Marketing | CapCut, TikTok, Instagram Reels |
| Stores | Apple Developer ($99/yr), Google Play ($25 once), a Mac or cloud build for iOS |

## 12. Metrics & Targets

| Metric | Soft-launch target (rough casual benchmarks) |
|---|---|
| D1 / D7 / D30 retention | ≥ 40% / ≥ 15% / ≥ 6% |
| Avg. session length | 8–15 min |
| Level funnel | No single level loses > 5% of players (find and fix those levels) |
| Story-scene skip rate | < 50% (if higher, the story isn't working) |
| Bond-scene engagement | Tracked per choice; informs which pairings to invest in |
| CPI vs. LTV | LTV(D90) > 1.3 × CPI before scaling paid user acquisition |
| Crash-free sessions | ≥ 99.5% |
| Chapter gate | % of qualified active players at the final level (§6) |

## 13. Expansion Strategy

1. **Inside the story:** the route itself is the roadmap (Istanbul → İzmir → ...).
   Each chapter is a new region pack.
2. **Spin-off cities:** same engine, new content pack, new local team of heroes.
   Candidates: **Athens**, Lisbon, Naples, Marseille, Tbilisi, Beirut.
3. **Cross-border caution:** Turkish–Greek topics (coffee, baklava, "Constantinople") can be
   a playful crossover event *or* a review-bomb. Get local writers involved before launch.

---

## 14. Roadmap (solo, AI-assisted)

| Phase | Duration | Exit criteria |
|---|---|---|
| **0. Engine stress test** | Week 1 (M0) | 500 enemies at 30 fps on a low-end Android (D-004) |
| **1. Core prototype** | Weeks 2–3 (M1) | Gray-box run is fun for Onder + 5 testers |
| **2. Systems + Level 1** | Weeks 4–11 (M2–M4) | Level 1 fully beautiful and playable |
| **3. Demand test** | Weeks 10–12, parallel to M4's end | Key art + Level 1 footage TikTok/ads tests (~$100–300) show strong CTR, or stop before district production |
| **4. Vertical slice** | Weeks 12–20 (M5–M7) | Levels 1–30, Kaan, motion comics, external playtest |
| **5. Soft launch (TR)** | Months 5–7 | Hit the §12 retention targets; tune the economy |
| **6. Chapter 1 complete** | Months 7–10 | All 100 levels + Night Shift endgame; global launch |
| **7. Chapter 2** | Built in parallel from month 8 | Ready **before** the §6 gate can fire |

**Publisher option:** after Phase 3 or 5, pitch Istanbul publishers (Rollic, Supersonic, etc.)
to fund user acquisition. Their tests can replace your marketing budget.

## 15. Compliance & Sensitivity

- **Data privacy:** KVKK (Turkey), GDPR (EU/diaspora). If minors might play, add age gates
  and COPPA-style handling.
- **Age rating:** target 16+ (human enemies, stylized violence).
- **Gambling:** no casino mechanics, no paid random loot in v1.
- **Content guardrails:** see narrative.md, *Writer Guardrails* (no real state actors,
  no earthquake imagery, no religion or politics as targets, no unlicensed brands or crests).
- **AI assets:** confirm commercial rights for every tool used; keep a provenance log.

## 16. Non-Goals for v1 (YAGNI)

No multiplayer, no PvP, no open world, no AR, no player-gender choice, no guilds/chat,
no gacha, no custom backend, no more than 3 quality tiers. Each one needs data to earn its way in.

## 17. Decision Log

| ID | Date | Decision | Rationale | Status |
|---|---|---|---|---|
| D-001 | 2026-11-08 | Chapters are 100 levels (10 districts × 10) | Clear progression, enough content runway, modular build | Adopted |
| D-002 | 2026-11-08 | Next chapter unlocks at 5% of *qualified active* players, with a 21-day max wait | Keeps Onder's intent; fixes the denominator and protects superfans | Adopted (pending Onder's review) |
| D-003 | 2026-11-08 | Visual quality tiers with gameplay parity; HD assets downloaded after install | Premium look on good phones without excluding budget Androids | Adopted |
| D-004 | 2026-11-08 | Engine: Godot 4 if the stress test passes, else Unity 6 | AI-friendliness vs. ad-SDK maturity and enemy-count performance | Open |
| D-005 | 2026-11-08 | Story via motion comics + Turkish VO for key scenes | Dizi feel at solo-builder cost | Adopted |
| D-006 | 2026-11-08 | Branch-and-bottleneck narrative; triangle targets the highest-bond girl | Meaningful choice at affordable scope | Adopted |
| D-007 | 2026-11-08 | 2D, top-down 3/4 view, **portrait** orientation; skeletal heroes, flipbook enemies | One-thumb play; cheapest path to premium hero animation; best low-end performance | Adopted |
| D-008 | 2026-11-08 | Content data as Godot custom Resources (`.tres`) in per-city packs | Typed, text-based (AI-editable), editor-friendly; city-as-data | Adopted |
| D-009 | 2026-11-08 | Two level types: Route (corridor + hold zones) and Arena (survive the timer) | Route sells the "walk home" journey; Arena keeps the genre core | Adopted |
| D-010 | 2026-11-08 | Enemies/projectiles as a data-oriented swarm (SoA + spatial hash + MultiMesh), no node per enemy | Only realistic path to 300+ enemies on budget Androids | Adopted |
| D-011 | 2026-11-08 | Operating model: Opus = lead/reviewer, separate executor model, milestone review gates | Speed of execution plus a consistent design authority | Adopted |

## 18. Open Questions

1. Final engine choice (D-004): depends on the week-1 stress test.
2. Exact gate threshold: is 5% right once real funnel data exists?
3. Hand-painted 2D style direction (D-007 settles 2D): pick from style frames in M4.
4. Self-publish vs. publisher deal: decide after the demand test.
5. Name: is *Son Durak* clear and searchable enough on stores worldwide?
