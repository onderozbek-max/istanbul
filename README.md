# Son Durak ("Last Stop")

A story-driven **survivor-like mobile game** set in a zombie-overrun Istanbul.
It plays like Survivor.io but feels like a Turkish dizi: a squad you care about, a real walk
home across real neighborhoods, and cliffhangers that bring players back.

> **Status (2026-11-08):** design foundation complete. No game code yet.
> **Next:** milestone **M0** (project setup + engine stress test). See [Kickoff](#kickoff-next-steps).

---

## The Game in 30 Seconds

Emre, 20, is eating döner on İstiklal Avenue when the outbreak hits. He stabs his first zombie
with a fork, calls his mom ("I'm coming home"), and the network dies. Each level is one stretch
of the walk from **Taksim to Ataköy** (Chapter 1), then by hacked e-scooter to **Sarıyer**
(Chapter 2), then by car to **İzmir** (Chapter 3). Along the way: a best friend (Kaan),
a long-time crush (Defne), a mysterious girl (Lale), gangs, a gated-community management board
gone mad, and a dad who knows more than his letters admit.

- **Genre:** survivor-like (auto-attack, one-thumb movement, level-up cards, bosses)
- **Platforms:** Android + iOS, portrait
- **Engine:** Godot 4 (confirmed after the M0 stress test)
- **Differentiators:** story and characters, Istanbul as a playable place, premium hero
  animation and game feel, gameplay-identical quality tiers for budget phones

---

## Repository Map

```
README.md                  you are here (human overview)
AGENTS.md                  entry point for coding agents (rules + reading order)
docs/
  product.md               strategy, pillars, monetization, roadmap, DECISION LOG
  narrative.md             story bible: characters, factions, Chapters 1-3, branching, guardrails
  prd.md                   vertical slice requirements (Levels 1-30) + acceptance criteria
  game-design.md           rules, formulas, progression, economy, telemetry, bot simulator
  content-catalog.md       starting numbers: heroes, weapons, enemies, bosses, levels 1-30
  design-system.md         look and feel: art, colors, type, HUD, readability, juice, a11y
  architecture.md          code structure, patterns, dependency rules, testing, Godot pitfalls
  level-001-istiklal.md    the opening level in full detail
  execution-plan.md        milestones M0-M7, review protocol, prompt kit
reviews/                   review packets (executor) + feedback (lead) + QUESTIONS.md
game/                      Godot project (created in M0)
art/                       source art + PROVENANCE.csv (created in M4)
tools/, reports/           scripts and generated reports (created as needed)
```

## What Each Doc Is For

| Doc | Answers the question | Read it when | Owner |
|---|---|---|---|
| [product.md](docs/product.md) | **Why** are we building this, for whom, how does it make money, what have we decided? | Strategy or scope questions; before any big change (check the decision log, §17) | Onder |
| [narrative.md](docs/narrative.md) | **What's the story?** Who are the characters and what happens in Chapters 1–3? | Writing dialogue, designing bosses, any story content. **Guardrails are binding.** | Onder + lead |
| [prd.md](docs/prd.md) | **What exactly does the slice have to do,** and how do we know it works? | Planning any feature; checking "is this in scope?" | Onder |
| [game-design.md](docs/game-design.md) | **How does the game work?** Formulas, card rules, progression, economy, telemetry | Implementing or tuning any system | Lead |
| [content-catalog.md](docs/content-catalog.md) | **What are the numbers?** Stats for every hero, weapon, enemy, boss and level | Entering content data; balancing | Lead (then the `.tres` files) |
| [design-system.md](docs/design-system.md) | **How should it look, sound and feel?** | Any art, UI, VFX, audio, accessibility or localization work | Lead |
| [architecture.md](docs/architecture.md) | **How is the code organized,** and which patterns/rules apply? | Before writing any code | Lead |
| [level-001-istiklal.md](docs/level-001-istiklal.md) | **What happens in the first level,** second by second? | Building Level 1; template for future level docs | Lead |
| [execution-plan.md](docs/execution-plan.md) | **Who does what, in which order,** and how are reviews done? | Starting a milestone; writing or reading a review | Onder + lead |
| [AGENTS.md](AGENTS.md) | **What must a coding agent read and obey?** | Every agent session starts here | Lead |

### How the docs fit together
```
product.md (why)  ->  prd.md (what, slice)  ->  execution-plan.md (when, who)
      |                    |
narrative.md (story)       +-> game-design.md (rules) -> content-catalog.md (numbers)
                           +-> design-system.md (look and feel)
                           +-> architecture.md (code)
                           +-> level-001-istiklal.md (one level, all of the above applied)
```

### Source-of-truth rules
1. **Each fact lives in exactly one doc;** others link to it (no copy-paste).
2. **Docs own intent.** Once implemented, `game/content/**/*.tres` owns the numbers.
3. **Decisions** live only in the decision log (`docs/product.md` §17).
4. **Every number in the docs is a starting value.** Playtests and the bot simulator decide the final values.

---

## How We Work

| Role | Who | Does |
|---|---|---|
| Owner | Onder | Decides, prioritizes, plays every milestone build on a phone, recruits playtesters |
| Lead / reviewer | Opus | Owns the docs, reviews milestone packets, writes revision instructions |
| Executor | Agentic coding model | Builds milestones per the docs, writes tests, writes review packets |

**Loop:** build milestone → review packet (`reviews/REVIEW-M<N>.md`) → Onder plays the build →
lead review (`reviews/FEEDBACK-M<N>.md`) → executor revises → approve → next milestone.
Details and prompts: [execution-plan.md](docs/execution-plan.md) §5–6.

**Milestones at a glance:** M0 engine gate (wk 1) · M1 first playable (wk 2–3) · M2 systems
(wk 4–5) · M3 Level 1 gray box (wk 6–7) · M4 look and feel (wk 8–11) · demand test (wk 10–12) ·
M5 District 1 (wk 12–14) · M6 Districts 2–3 + Kaan (wk 15–18) · M7 playtest (wk 19–20).

---

## Kickoff: Next Steps

### Step 1: Before you move anything (15 min)
- [ ] Confirm with your employer's policy (outside activities / IP / use of company resources)
      that this is fine as a personal project. It protects your ownership of the game.

### Step 2: Move the repo to your personal environment (10 min)
On this machine:
```bash
cd ~/Documents/istanbul
git bundle create son-durak.bundle --all     # one file with the full git history
```
Transfer `son-durak.bundle` to your personal machine, then:
```bash
git clone son-durak.bundle son-durak
cd son-durak
git remote remove origin                     # the bundle becomes "origin"; drop it
# optional: create a PRIVATE repo on your personal GitHub and push
git remote add origin <your-private-repo-url> && git push -u origin main
```
(Keep the repo **private**: it's your unreleased game design.)

### Step 3: Set up the personal machine (1–2 h)
- [ ] **Godot 4.x stable** (standard build, not .NET), from godotengine.org
- [ ] **Android build tools:** Android Studio (SDK + platform tools), JDK 17, Godot Android
      export templates (Godot: *Editor → Manage Export Templates*)
- [ ] **A low-end Android phone** for testing (3–4 GB RAM, entry-level, ~2023). A used one is
      fine. **Required for M0-T4**: the engine decision depends on real-device numbers.
- [ ] **Your agentic coding tool,** pointed at the repo folder, with permission to edit files and run shell commands
- [ ] Optional: `uv` (Python) for report scripts later

### Step 4: Make the three owner decisions (10 min)
Write these into `reviews/QUESTIONS.md` or the decision log:
1. **D-002 chapter gate:** accept the adapted 5% rule (product.md §6), or keep the original.
2. **Executor:** run the bake-off (execution-plan.md §2), or just pick one model.
3. **Low reference device:** which exact phone you'll test on.

### Step 5: Kick off M0 (paste into your executor)
```
You are the executor for "Son Durak", a mobile survivor-like set in Istanbul.
Read AGENTS.md first, then the docs in the order it lists. The docs are the source of truth.
Your job right now: milestone M0 from docs/execution-plan.md §4, tasks T1-T5.
Rules: follow docs/architecture.md exactly (Godot 4 only, static typing, SoA swarm,
data-driven content, dependency rules). Write tests. Keep files under 600 lines.
Do not change design intent; log number changes under "Deviations" in the review packet.
Stop and write a question into reviews/QUESTIONS.md if you hit any "stop and ask" case.
When done, write reviews/REVIEW-M0.md using the template in execution-plan.md §5.2,
including the required screenshots. Then stop.
```
For a **bake-off,** run the same prompt in two branches (`bakeoff/<model>`), limited to T1–T3.
You'll need to do T4 together with the executor: connect the phone, install the APK, run the benchmark.

### Step 6: Bring it back for review
When `reviews/REVIEW-M0.md` exists, give the lead (Opus) access to the repo (or paste the packet
+ screenshots + `git log`) with the review prompt:
```
Review milestone M0 of Son Durak. Read reviews/REVIEW-M0.md, inspect the diff (<from>..<to>),
run tools/test.sh and the bot simulator where relevant, view the screenshots, and write
reviews/FEEDBACK-M0.md per execution-plan.md §5.3. Update docs if decisions changed.
```
The review prompt is portable: any Opus-class model in your personal environment can play
the lead role, because all context lives in the repo, not in a chat history.

### What "M0 done" looks like
- The Godot project opens and its tests pass headless.
- A benchmark with **500 zombies + 200 projectiles + 300 XP droplets** has run on your low-end phone.
- `REVIEW-M0.md` reports p50/p95 frame times and recommends Godot (or the fallback).
- The engine decision (D-004) gets made at that review. Then M1: **your first playable in about 2 weeks.**

---

## Conventions (summary)
- Godot 4 only, static typing, files ≤ 600 lines, tests green before merging to `main`.
- Branches `m<N>/t<K>-<slug>`; commits `m1/t5: add lob_aoe behavior`.
- No secrets, no real brands, narrative guardrails are binding.
- Full rules: [AGENTS.md](AGENTS.md) and [architecture.md](docs/architecture.md) §9.
