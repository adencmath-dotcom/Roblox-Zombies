# STUDIO AUDIT — "Arlo num num"

**Task:** GAME-001  
**Date:** 2026-10-13  
**Auditor:** Claude (read-only — nothing in Studio was changed)  
**Place:** "Arlo num num", place ID 95925940792219, game ID 10770767441

This is **not** the place recorded earlier as Project Zomblox (place ID 81227088977620), which was an empty baseplate. Renaming a place does not change its ID, so these are two different places.

---

## 1. Summary

The place already contains a substantial, working prototype titled **"FROSTBOUND — The Citadel"** (from `Config.Title`):

- A Der Eisendrache–inspired map of about **21,400 parts** in `Workspace.CitadelMap`.
- About **50 game scripts**: a full round-based loop with combat, points, power, a door, a mystery box, a perk, Pack-a-Punch-style upgrades, teleporters, barricades, downs and revives, saved profiles, camos, gums, bows and wonder weapons.
- **208 ModuleScripts of imported texture and model data** in `ServerStorage.ImportedData` (see §5 — this needs a decision).

Most Phase 3 tasks on the board (GAME-002 to GAME-006) already have an implementation of some kind. The docs should be updated to describe this build rather than plan a new one.

---

## 2. Code

| Location | Contents |
|---|---|
| `ServerScriptService.CitadelServer` | `Main` (Script, 200 lines) plus 21 modules: `MapBuilder`, `Reconstruction`, `LayoutRebuild`, `RoomKit`, `RoomReconstruction`, `Architecture`, `InteriorDetail`, `PropDetail`, `Landscape`, `SculptMesh`, `DragonSculpture`, `ChurchReference`, `CourtyardCryptReference`, `UndercroftReference`, `ResearchHallMeshes`, `Combat`, `Director`, `Progression`, `Profiles`, `PerkMachines`, `Tests` |
| `ReplicatedStorage.Citadel` | `Config` (63 lines), `MapLayout` (39 lines), `BowGeometry`, `ImportedMesh`, 18 perk-icon texture modules |
| `StarterPlayerScripts.CitadelClient` | `Main` (LocalScript, 198 lines), `Input`, `UI`, `Journal`, `PerkIcons`, `ZombieVisuals` |
| `ServerStorage.ImportedData` | 208 data modules (textures and models) |

Read in full: `Main`, `Config`, `MapLayout`, `MapBuilder`, `Combat`, `Tests`. **Not yet read:** `Director` (zombie AI), `Progression`, `Profiles`, `PerkMachines`, the reconstruction modules, and all client code.

### Networking
- Created at runtime by `Main`: `ReplicatedStorage.Citadel.Network.Intent` (client → server) and `.Event` (server → client). Two RemoteEvents in total.

### How the map is built
- `Main` calls `MapBuilder.Build()` when the server starts. If `CitadelMap` already exists, it **runs `Reconstruction.Apply` and `LayoutRebuild.Apply` on it at runtime**. Hand edits made in Studio may therefore be changed or moved when the game runs. This must be understood before anyone edits the map by hand.
- `MapLayout` converts positions from "a user-supplied 1469×659 plan" image at **0.55 studs per pixel**. Its own comment says heights are estimates.

---

## 3. Gameplay systems found

| System | Status | Where | Notes |
|---|---|---|---|
| Rounds and spawning | Exists | `Director`, `Config.Round` | Count = (5 + 3 × round) × player scaling; health 75 × 1.13^(round−1); speed capped at 19 |
| Weapons and firing | Exists | `Combat` | Server raycasts from the player's head; sequence numbers and a 45-actions-per-second limit; ammo, reload and switching tracked on the server |
| Points | Exists | `Combat.Damage`, `Main` | Server-awarded: 10 per hit, 50 / 100 (headshot) / 130 (melee) per kill; 500 to start; 10 per board repaired, capped at 50 per round |
| Purchases | Exists | `Main` prompt handler | Server checks distance (14 studs), line of sight, a 0.4 s cooldown and the balance before spending |
| Doors | 1 door | `ChapelGate` (750) | Only one purchasable door exists |
| Power | Exists | `Power relay` | Gates perks, upgrades, teleports and the bow |
| Perks | Exists | `Ironheart tonic` (2500, via `Main`); the other 9 machines are created at runtime by `Progression` | 4-perk limit. Ironheart's purchase path in `Main` does **not** check that limit, so it can be bought as a fifth perk |
| Mystery box | Exists | `Arsenal cache` (950) | Random pool of 3 weapons |
| Pack-a-Punch | Exists | `Aether forge` (5000) | Damage × 2.5, magazine × 2 |
| Wall-buy | 1 | `Bastion AR` (1000) | — |
| Teleporters | 4 | Undercroft lift / Return to castle; Rocket transit / Castle transit | Need power |
| Barricades | 6 | `CitadelMap.Entries` | 5 boards each |
| Downs and revive | Exists | `Main` | 30 s bleed-out; solo self-revive once |
| Profiles and saving | Exists | `Profiles` | Settings, kills, camos, highest round |
| Extras beyond first-version scope | Exist | `Config`, `Progression` | 20 camos, 5 gums, 4 elemental bows, dragon soul feeding, 3 wonder weapons (sword, skull, gauntlet), grenades, slide and sprint |
| Max players | 6 | `Config.MaxPlayers` | The Game Bible lists this as TBD |
| Tests | Exists | `CitadelServer.Tests` | 6 unit checks of configuration and settings; run from the server console |

---

## 4. Map contents

Main areas in `Workspace.CitadelMap`, with bounding-box centres:

| Model | Centre (X, Y, Z) | Size (studs) | Likely section in `MAP_REFERENCE.md` |
|---|---|---|---|
| 01 • Gondola station reference reconstruction | −34, 26, 147 | 171 × 54 × 352 | Spawn |
| 02 • Gatehouse supply room reference reconstruction | −32, 8, 2 | 35 × 17 × 27 | Gatehouse / Lower Courtyard supply room |
| 03 • Mission control interior / Mission control chapel | 10, 43, −208 | 79 × 55 × 81 | Church |
| Upper courtyard and workshop | 121, 29, −141 | 56 × 46 × 80 | Upper Courtyard |
| 04 • Snow courtyard and western arcade | −122, 24, −119 | 82 × 34 × 87 | Lower Courtyard? |
| Barracks and lower arcade | −116, 36, −165 | 59 × 56 × 55 | Living Quarters / Knight's Hall? |
| Clock tower • reconstructed | −129, 39, −7 | 26 × 78 × 25 | Clocktower |
| 05 • Pyramid chamber video reconstruction | 0, −18, −66 | 68 × 26 × 68 | Undercroft |
| 04 • Rocket overlook | 272, 24, 33 | 74 × 56 × 76 | Rocket Pad |
| Reference plan • connected routes / exterior ramparts | — | up to 369 × 35 × 377 | Layout guides |
| Alpine valley, bedrock, snow dressing | — | up to 1080 × 120 × 1080 | Scenery |

Player spawn: `CitadelSpawn` at (17.6, 0.2, 2.75).

### Scale
The existing build is **much larger** than the scale proposed in `MAP_BUILD_PLAN.md`:

| Feature | Existing build | MAP-003 proposal |
|---|---|---|
| Doorway (Gondola station north doorway) | 14 studs wide | 5 studs wide |
| Chapel gate | 22 × 18 studs | 5 × 8 studs |
| Barricade | 10 studs wide | — |

The proposal must be revised to match the existing build, or the team must decide to rescale the build. Rescaling 21,400 parts is a large change.

---

## 5. Risks and decisions needed

1. **Imported Call of Duty assets (high priority).** `ServerStorage.ImportedData` holds 208 modules named after Black Ops III asset files, such as `i_c_zom_dlc3_dragon_head`, `i_wpn_t7_zmb_dlc3_gauntlet_dragon`, `i_wpn_t7_zmb_zod_sword_blade` and `i_c_zom_der_zombie_head1`. `Config` also uses Call of Duty names such as "Wrath of the Ancients", "Apothicon Sword", "Skull of Nan Sapwe" and "Gauntlet of Siegfried". `GAME_BIBLE.md` §9 and §11 require original or authorized assets. Assets extracted from a commercial game can lead to copyright takedowns or moderation action against the game on Roblox. **The team should decide whether to remove or replace them before publishing.**
2. **The map is rebuilt at runtime.** See §2. Agree on a rule, either "edit the map in Studio and disable runtime rebuilds" or "edit the builder modules only", before anyone edits geometry.
3. **Architecture differs from `ARCHITECTURE.md`.** The real code uses `CitadelServer` modules (`Combat`, `Director`, `Progression`…) rather than the proposed `RoundService` / `PointsService` structure. Under `AI_RULES.md` §9, the existing implementation takes precedence, so `ARCHITECTURE.md` should be updated to describe it.
4. **Scope is well beyond the first version.** Camos, gums, bows, wonder weapons and dragon quests are listed as out of scope in `GAME_BIBLE.md` §13. The team should decide whether to keep, freeze or remove them.
5. **Ironheart skips the 4-perk limit** (see §3). *Fixed 2026-10-13 in `Main` line 134; not yet playtested.* A minor inconsistency. An earlier version of this audit wrongly said every perk machine granted Ironheart; the other perks are handled by `Progression` and work correctly.
6. **Which place is the project?** Project Zomblox (empty) and Arlo num num (this build) are different places. The docs should name one.

---

## 6. Testing

**NOT TESTED.** This audit only read the place's contents and code. No playtest was run, because it would have interrupted the live Team Create session, and `CitadelServer.Tests` was not run.
