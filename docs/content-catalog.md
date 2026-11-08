# Project Istanbul: Content Catalog (Vertical Slice + Planned)

> **Status:** v0.1 · 2026-11-08 · Owns: starting numbers for heroes, weapons, passives,
> evolutions, enemies, bosses, pickups, interactables, and the L1–30 level list.
> **Rules that use these numbers:** [game-design.md](game-design.md).
> After implementation, `game/content/**/*.tres` is the source of truth. IDs below are the
> resource IDs (snake_case). Display names come from localization keys, not from these tables.

---

## 1. Heroes

| ID | Name | HP | Armor | Move (m/s) | Signature weapon | Tag-in move | Ultimate | Available |
|---|---|---|---|---|---|---|---|---|
| `hero_arda` | Arda | 100 | 0 | 3.2 | Fork | **Stab-Dash:** 2 m dash, 20 dmg to enemies passed | **Fork Frenzy:** chain-dashes through up to 7 enemies (40 dmg each) over 1.2 s, invulnerable | Slice (start) |
| `hero_kaan` | Kaan | 180 | 2 | 2.6 | Anchor | **Mini Slam:** r 1.5 m, 25 dmg, knockback 1 m | **Ground Slam:** r 3.5 m, 80 dmg, stun 1 s, knockback 2 m | Slice (L30) |
| `hero_mila` | Mila | 70 | 0 | 4.2 | Twin Batons | **Dash:** 3 m through enemies, 15 dmg | **Sprint Blitz:** 3 rapid dashes (35 dmg each), leaves a 40% slow trail for 3 s | Chapter 2 |
| `hero_ada` | Ada | 80 | 0 | 3.2 | Slingshot | **Calm Pulse:** r 3 m, slow 40% for 2 s | **Calm Field:** r 5 m, slow 60% for 4 s + volley of 12 bolts (20 dmg each) | Chapter 2 |

**Companion signature weapons** (scale with hero meta level, not with in-run cards):
| ID | Behavior | Damage | Cooldown | Area / range | Notes |
|---|---|---|---|---|---|
| `wpn_anchor` | `melee_spin` | 30 | 2.5 s | r 2.2 m, 360° | Knockback 1 m |
| `wpn_batons` | `melee_arc` | 6 × 2 hits | 0.5 s | 1.4 m, 90° | Fastest attack in the game |
| `wpn_slingshot` | `straight_multi` | 10 | 0.9 s | 8 m, speed 14 m/s | Pierce 2, targets nearest |

---

## 2. Card Weapons

Behaviors map 1:1 to weapon strategy classes (architecture.md §4.4). Damage is base, before stats.

| ID | Name (EN / TR) | Behavior | Targeting | Dmg | CD (s) | Area / range | Proj | Pierce | Slice |
|---|---|---|---|---|---|---|---|---|---|
| `wpn_fork` | Fork / Çatal | `melee_arc` | Facing | 12 | 0.8 | 1.6 m, 60° | 1 | all in arc | Yes (signature) |
| `wpn_tea_glass` | Tea Glass / Çay Bardağı | `lob_aoe` | Densest cluster within 6 m | 18 | 2.0 | Lob 4 m, splash r 1.2 m | 1 | AoE | Yes |
| `wpn_simit` | Simit Ricochet / Simit | `ricochet` | Nearest | 10 | 1.5 | Bounce range 3 m | 1 | 3 bounces | Yes |
| `wpn_seagulls` | Seagulls / Martılar | `orbit_dive` | Nearest within 4 m | 8 | 1.2 per gull | Orbit r 2.2 m | 2 gulls | 1 | Yes |
| `wpn_doner_skewer` | Döner Skewer / Döner Şişi | `pierce_line` | Facing | 20 | 2.2 | Line 6 m × 0.5 m | 1 | all | Yes |
| `wpn_chestnut_mortar` | Chestnut Mortar / Kestane | `cluster_lob` | Random enemy on screen | 25 + 3 × 8 | 3.5 | r 1.0 m + 3 sub-pops r 0.5 m | 1 | AoE | Yes (unlock L6) |
| `wpn_tram_bell` | Tram Bell / Tramvay Zili | `pulse` | Self-centered | 10 | 3.0 | r 2.5 m, knockback 1.5 m | — | AoE | Yes (unlock L11) |
| `wpn_lahmacun` | Lahmacun Barrage / Lahmacun | `straight_multi` | Facing + nearest | 7 | 1.0 | 9 m, speed 12 m/s | 2 | 1 | Later |
| `wpn_pickle_juice` | Pickle Juice / Turşu Suyu | `zone` | Random near enemies | 5 / 0.5 s | 4.0 | r 1.4 m, 3 s, slow 25% | 1 zone | AoE | Later |

### Level-up effects (L2 → L5)
| ID | L2 | L3 | L4 | L5 |
|---|---|---|---|---|
| `wpn_fork` | +4 dmg | Adds a back-thrust | +25% range | +8 dmg, arc 120° |
| `wpn_tea_glass` | +1 projectile | +25% area | +1 projectile | +10 dmg, leaves 1 s scald zone (Burn) |
| `wpn_simit` | +1 bounce | +1 projectile | +1 bounce, +4 dmg | +1 projectile |
| `wpn_seagulls` | +1 gull | +3 dmg | +1 gull | Dives knock back; 5% chance a gull "steals a simit" (heal 2) |
| `wpn_doner_skewer` | +6 dmg | +50% width | −0.4 s CD | Fires front and back |
| `wpn_chestnut_mortar` | +1 projectile | +2 sub-pops | +8 dmg | +1 projectile, sub-pops apply Burn |
| `wpn_tram_bell` | +20% radius | +6 dmg | −0.6 s CD | Pulse applies 30% slow for 2 s |
| `wpn_lahmacun` | +1 projectile | +1 pierce | +1 projectile | +1 projectile, +3 dmg |
| `wpn_pickle_juice` | +1 zone | +25% area | +1.5 s duration | +1 zone, slow 40% |

---

## 3. Passives

| ID | Name (EN / TR) | Per level | Max | Pairs with (evolution) | Slice |
|---|---|---|---|---|---|
| `pas_sneakers` | Sneakers / Spor Ayakkabı | +8% move speed | 5 | Pickle Juice | Yes |
| `pas_puffer_jacket` | Puffer Jacket / Şişme Mont | +1 armor | 5 | Tram Bell | Yes |
| `pas_ayran` | Ayran | +0.3 HP/s regen | 5 | Chestnut Mortar | Yes |
| `pas_turkish_coffee` | Turkish Coffee / Türk Kahvesi | −6% cooldowns | 5 | Lahmacun Barrage | Yes |
| `pas_butter` | Butter / Tereyağı | +10% might | 5 | Döner Skewer | Yes |
| `pas_teapot` | Teapot / Demlik | +8% area | 5 | Tea Glass | Yes |
| `pas_pul_biber` | Chili Flakes / Pul Biber | +4% crit chance | 5 | Seagulls | Later |
| `pas_sesame` | Sesame / Susam | +1 projectile | **2** | Simit | Later |

**Rule:** each passive pairs with exactly one weapon (1:1), so evolutions are easy to learn.

---

## 4. Evolutions

| ID | From (weapon L5 + passive) | Name (EN / TR) | Effect | Slice |
|---|---|---|---|---|
| `evo_semaver_storm` | Tea Glass + Teapot | Samovar Storm / Semaver Fırtınası | Lobs 4 glasses; each leaves a 3 s boiling zone (Burn, r 1.5 m) | Yes |
| `evo_iskender_lance` | Döner Skewer + Butter | İskender Lance / İskender Mızrağı | Line 10 m × 1.0 m, fires front+back+sides, leaves a 2 s butter-burn trail; ×1.5 dmg (multiplicative) | Yes |
| `evo_chestnut_volcano` | Chestnut Mortar + Ayran | Chestnut Volcano / Kestane Volkanı | A chestnut cart erupts at the player's position every 5 s: 8 lobs + healing steam (+5 HP per eruption) | Yes |
| `evo_tram_line` | Tram Bell + Puffer Jacket | Tram Line / Tramvay Hattı | Every 6 s a ghost tram charges across the screen through the player's lane: 120 dmg, knockback 3 m; pulse continues | Yes |
| `evo_golden_simit` | Simit + Sesame | Golden Simit / Altın Simit | Infinite bounces for 4 s; splits into 2 on every 3rd bounce | Later |
| `evo_gull_frenzy` | Seagulls + Pul Biber | Gull Frenzy / Martı Sürüsü | 8 gulls, dives always crit, steal-heal chance 15% | Later |
| `evo_oven_fire` | Lahmacun + Turkish Coffee | Oven Fire / Fırın Ateşi | Rapid-fire lahmacun stream, 6 per volley, applies Burn | Later |
| `evo_pickle_trail` | Pickle Juice + Sneakers | Pickle Trail / Turşu İzi | Zones spawn along the player's path every 0.5 s while moving | Later |

---

## 5. Enemies

Speeds: hero base is 3.2 m/s; **nothing basic outruns the base hero** (runners are close).
Budget cost = cost per spawn in the spawn director's budget (game-design.md §6).

| ID | Name | HP | Speed | Contact dmg | XP | Budget | Knockback resist | Behavior | First level |
|---|---|---|---|---|---|---|---|---|---|
| `enm_walker` | Walker / Yürüyen | 10 | 1.2 | 5 | 2 | 1.0 | 0% | Shambles toward the player | L1 |
| `enm_runner` | Runner / Koşucu | 6 | 2.9 | 4 | 3 | 1.5 | 0% | Sprints toward the player | L1 (seg C) |
| `enm_crawler` | Crawler / Sürünen | 8 | 1.0 | 6 | 2 | 1.5 | 50% | Emerges from manholes (1.0 s telegraph), low silhouette | L1 (scripted) |
| `enm_brute` | Brute / İriyarı | 80 | 0.9 | 15 | 10 | 6.0 | 80% | Slow tank, shoulder-charge 4 m every 6 s (0.8 s telegraph) | L4 |
| `enm_spitter` | Spitter / Tükürükçü | 15 | 1.1 | 4 | 4 | 3.0 | 0% | Keeps 5 m distance; spit projectile 6 dmg, 4 m/s, every 3 s (0.6 s telegraph) | L6 |
| `enm_exploder` | Exploder / Patlayan | 20 | 1.4 | 0 | 4 | 3.0 | 30% | Within 1.2 m: 0.8 s fuse, explodes r 2.0 m, 20 dmg; **hurts zombies too** | L8 |
| `enm_tourist` | Tourist / Turist | 12 | 1.3 | 5 | 2 | 1.2 | 0% | Like a walker; 30% Jeton drop chance. (Selfie stick, no camera flashes: photosensitivity) | L11 |
| `enm_fisherman` | Fisherman / Balıkçı | 25 | 1.0 | 6 | 5 | 4.0 | 20% | Casts a line every 4 s, range 5 m (0.7 s line telegraph); pulls the player 1.5 m (Grabbed) | L21 |

**Elite variant (any type):** ×4 HP, ×1.5 damage, +15% scale, purple outline (`elite` token,
plus a crown-shaped marker for colorblind players), drops a Mini Chest. First elite: L7.

**Visual rules:** each type has a unique silhouette readable at 48 px (design-system.md §6).
Zombies wear everyday Istanbul clothes; desaturated palette; no gore close-ups.

---

## 6. Bosses and Mini-Bosses

All telegraphs ≥ 0.8 s for bosses. Damage values are base (scaled by nothing else).

### L5 · Kestaneci (Chestnut Vendor), mini-boss · HP 600
- **Chestnut Spray:** cone of 5 lobbed chestnuts, ground telegraph 0.8 s, 8 dmg each, leaves small burning patches (2 s).
- **Cart Charge:** line telegraph 1.0 s, charges 7 m/s for 6 m, 20 dmg.
- **Counterplay:** dodge sideways; the cart can be baited into a gas canister.
- **Reward:** Boss Chest; unlocks **Chestnut Mortar** in the card pool from L6.

### L10 · The Vatman (Tram Driver), district boss · HP 2,500
- **Phase 1 (100–60%), the tram:** Vatman rides the derailed-then-restarted red tram on the rail lane.
  - *Tram Rush:* the rail lane glows red for 1.2 s, then the tram crosses at 14 m/s: 35 dmg to the player and **kills all zombies in its path** (lure them!).
  - *Bell Shockwave:* ring telegraph 0.8 s, r 3.5 m, 12 dmg.
  - *Passenger Spill:* the doors open and 12 walkers pour out.
- **Phase 2 (60–25%), on foot:** the tram derails; Vatman fights with the brake lever.
  - *Lever Slam:* circle r 1.8 m, 0.8 s telegraph, 25 dmg.
  - *Sparks:* 3 lines of electric sparks along the rails (0.9 s telegraph), 10 dmg.
- **Phase 3 (< 25%), enraged:** +25% speed; Bell Shockwave fires twice in a row.
- **Reward:** Boss Chest; unlocks **Tram Bell** from L11; motion-comic beat.

### L15 · Tour Guide (Turist Rehberi), mini-boss · HP 2,000
- Raises a flag that **buffs tourists within 4 m (+20% speed)**, so kill-priority matters.
- *Megaphone Blast:* cone 60°, 4 m, 0.8 s telegraph, 15 dmg, knockback 1.5 m.
- Summons 2 tourist groups (8 each) every 15 s.

### L20 · The Bride (Gelin), district boss · HP 4,500
- **Phase 1:** *Bouquet Throw:* marks one zombie, which becomes an Elite after 2 s (kill it fast).
  *Veil Spin:* r 2.5 m, 0.9 s telegraph, 18 dmg.
- **Phase 2 (< 50%), the halay:** a linked **halay dance line** of 10 zombies sweeps the arena
  in a wide arc (telegraphed path 1.2 s); touching the line = 15 dmg + knockback. Break the line by killing the leader (handkerchief).
- **Reward:** Boss Chest + motion-comic beat.

### L25 · Big Fisherman (Koca Balıkçı), mini-boss · HP 3,500
- Casts **3 lines at once** (fan, 0.8 s telegraph), pull 2 m.
- *Net Throw:* circle r 2.2 m, 1.0 s telegraph, roots 1.2 s.
- Calls fisherman adds (4) every 20 s.

### L30 · Kaan, story fight · Composure 5,000 (non-lethal)
- **Phases 1–2 (vs Kaan):** he thinks Arda is infected.
  - *Anchor Swing:* 270° arc r 2.5 m, 1.0 s telegraph, 20 dmg.
  - *Anchor Throw:* line 7 m, 0.9 s telegraph, 18 dmg, then he reels it back (second hit on the way back).
  - *Ground Slam:* r 3 m, 1.2 s telegraph, 25 dmg.
  - At 50% Composure: a horde wave arrives from both bridge ends and attacks **both** of you (foreshadows teaming up).
- **At 0 Composure:** short cutscene; they realize the truth; Kaan joins.
- **Phase 3 (survive 90 s together):** a huge horde from both ends of the bridge.
  **Tag-switch tutorial** here (1 prompt, icon + 4 words).
- **Reward:** Kaan unlocked; Boss Chest; motion-comic beat; end of the slice.

---

## 7. Levels 1–30

Template: game-design.md §6. Durations are targets for an average player.

### District 1 · İstiklal Avenue (Levels 1–10)
| L | Type | Mods | Intro | Duration | Story hook |
|---|---|---|---|---|---|
| 1 | Route | — | Walker, Runner, Crawler (scripted) | 3.5 min | Cold open, call drops (see level-001) |
| 2 | Arena | — | Simit carts | 4 min | Arda tries the phone again: no signal |
| 3 | Route | — | Gas canister combos | 4 min | Bark: "Metro's closed. Of course it is." |
| 4 | Arena | — | **Brute** | 5 min | — |
| 5 | Mini-boss | — | **Kestaneci** | 5 min | Chestnut cart becomes a weapon idea |
| 6 | Route | — | **Spitter** | 5 min | — |
| 7 | Arena | — | First **Elite** | 6 min | — |
| 8 | Route | night | **Exploder** | 5 min | Streetlights fail one by one |
| 9 | Arena | horde | — | 6 min | — |
| 10 | Boss | — | **Vatman** | 7 min | Motion comic: tram crash, Arda heads downhill to Karaköy |

### District 2 · Karaköy & Galata (Levels 11–20)
| L | Type | Mods | Intro | Duration | Story hook |
|---|---|---|---|---|---|
| 11 | Route | — | **Tourist** | 5 min | Steep streets downhill from Tünel |
| 12 | Arena | — | **Paşa the cat** (early-warning hisses) | 5 min | Paşa adopts Arda |
| 13 | Route | — | Stairs as chokepoints | 5 min | Historic stairs down to Karaköy |
| 14 | Arena | — | — | 6 min | Galata Tower square |
| 15 | Mini-boss | — | **Tour Guide** | 6 min | — |
| 16 | Route | — | — | 6 min | Karaköy café streets |
| 17 | Arena | — | — | 6 min | Waterfront by the pier |
| 18 | Route | night | — | 6 min | — |
| 19 | Arena | horde | — | 7 min | — |
| 20 | Boss | — | **The Bride** | 8 min | Motion comic: the wedding café; Arda sees the bridge |

### District 3 · Galata Bridge (Levels 21–30)
| L | Type | Mods | Intro | Duration | Story hook |
|---|---|---|---|---|---|
| 21 | Route | — | **Fisherman** | 6 min | Upper deck, fishing lines everywhere |
| 22 | Arena | — | — | 6 min | Lower-deck restaurant row |
| 23 | Route | fog | — | 6 min | Fog rolls in off the Golden Horn |
| 24 | Arena | — | — | 7 min | Mid-bridge |
| 25 | Mini-boss | — | **Big Fisherman** | 7 min | — |
| 26 | Route | night | — | 7 min | Lower deck at night |
| 27 | Arena | ambush | — | 7 min | Glimpse of a huge figure with an anchor |
| 28 | Route | night, fog | — | 7 min | — |
| 29 | Arena | horde | — | 8 min | — |
| 30 | Boss | — | **Kaan** | 9 min | Motion comic: Kaan joins; Eminönü ahead |

---

## 8. Pickups

| ID | Name | Effect | Source |
|---|---|---|---|
| `pk_xp_s` / `_m` / `_l` | Adrenaline droplet (green / blue / purple) | XP 1× / 5× / 25× | Enemy deaths. **Auto-merge:** if > 150 droplets exist, the oldest merge into larger ones (readability + perf) |
| `pk_jeton` | Jeton | +1–5 Jeton (meta) | 5% of enemies (tourists 30%) |
| `pk_simit` | Simit | Heal 25 HP | Simit carts, 0.5% of enemies |
| `pk_magnet` | Magnet / Mıknatıs | Pulls all XP on the map | ~1 per 2 min (director-placed), 10% from elites |
| `pk_chest_mini` | Mini Chest (Kutu) | 1 upgrade | Elites |
| `pk_chest_boss` | Boss Chest | Evolution or 1–3 upgrades | Bosses / mini-bosses |

## 9. Interactables (environment)

| ID | Prop | HP | When destroyed | Notes |
|---|---|---|---|---|
| `int_simit_cart` | Simit cart (red glass box) | 30 | Drops 2 Simits | Common in District 1 |
| `int_chestnut_cart` | Chestnut cart | 30 | Burning zone r 1.5 m, 5 s, 6 dmg/s to **enemies only** | Seeds the Chestnut Mortar idea |
| `int_gas_canister` | Gas canister (tüp) | 10 | Explosion r 2.5 m: 60 dmg to enemies, **15 to the player** | Risk/reward |
| `int_tea_tray` | Café table with a tea tray | 15 | 6 tea glasses burst outward, 10 dmg each | Comic SFX "ŞANGIR!" |
| `int_cafe_chairs` | Café chairs | — | Knocked aside (cosmetic, physics-lite) | Pure juice |
| `int_shutter` | Shop shutter | — | Objective door (opens on script) | Route-level exits |
| `int_manhole` | Manhole | — | Crawler spawn point (1.0 s telegraph: lid rattles) | Telegraph = audio + visual |
