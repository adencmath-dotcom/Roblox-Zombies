# MAP BUILD PLAN — Der Eisendrache

**Task:** MAP-003  
**Status:** PROPOSED — needs agreement from both developers before the blockout (MAP-004) starts.  
**Layout source:** `Docs/MAP_REFERENCE.md`

> ⚠️ **On hold (2026-10-13):** the team is working in "Arlo num num" (place ID 95925940792219), which already contains a large Der Eisendrache build at a much larger scale (doorways about 14 studs wide). The scale, origin and naming below were written for an empty place and conflict with that build. See `Docs/STUDIO_AUDIT.md` before using anything in this document.

**Studio place (original):** Project Zomblox (place ID 81227088977620), an empty baseplate when checked.

---

## 1. Scale

| Rule | Value |
|---|---|
| Base scale | **1 metre = 3.5 studs** (1 stud ≈ 0.286 m, close to Roblox's own 0.28 m physics scale) |
| From Black Ops III units | 1 game unit ≈ 1 inch → **1 unit ≈ 0.089 studs** (multiply unit distances by 0.089) |
| Standard door opening | 5 studs wide × 8 studs tall |
| Standard ceiling | 12 studs (taller in halls, courtyards and the Church) |
| Corridor | at least 8 studs wide, so zombies and players can pass |
| Stair step | 1 stud rise × 1.5 studs run; max slope for ramps 40° |
| Wall thickness | 1 stud (2 studs for exterior castle walls) |

**Before committing to this:** build one test doorway and one test corridor, walk through them with a default R15 character, and confirm they feel right. If they feel off, change the base scale *once*, here, before any room is built.

## 2. Coordinates

| Rule | Value |
|---|---|
| Origin `(0, 0, 0)` | Centre of the **Spawn** room floor |
| Axes | **North = −Z**, East = +X, Up = +Y (matches Studio's default orientation) |
| Floor levels | Ground floor of Spawn = Y 0. Undercroft is negative Y. Upper floors are positive Y. |
| Grid | Move snap **1 stud**; rotate snap **15°**. Room corners sit on whole studs. |
| Rocket Test Pad | Built as a separate area placed **at least 600 studs from the castle**, since it is reached only by teleporter or Wundersphere. Exact position decided in MAP-004. |

Each section records its anchor point (its floor centre) in the table in §4 once it is blocked out. After that, the anchor must not move without approval (`AI_RULES.md` §8).

## 3. Explorer structure

Follows `ARCHITECTURE.md` §3:

```
Workspace
└─ Map
   ├─ Rooms
   │  └─ Room_<SectionId>          (Model, one per section)
   │     ├─ Blockout               (Folder: Floor, Wall, Ceiling, Stairs, Ramp parts)
   │     └─ Detail                 (Folder: added only after the layout is approved)
   ├─ Corridors
   ├─ Doors
   ├─ Barricades
   ├─ Interactables
   ├─ PlayerSpawns
   └─ ZombieSpawns
```

Every `Room_<SectionId>` model gets a **`SectionId`** attribute and has its **WorldPivot at its anchor point**.

## 4. Section IDs

These IDs are stable. A room's visuals can change, but its ID cannot without approval.

| SectionId | Area (see `MAP_REFERENCE.md`) | Level | Anchor (X, Y, Z) | Editor |
|---|---|---|---|---|
| `Spawn` | Spawn / tram room | Ground | 0, 0, 0 | — |
| `MuleKickTunnel` | Mule Kick Tunnel | Ground | TBD | — |
| `LowerCourtyard` | Lower Courtyard | Ground | TBD | — |
| `UpperCourtyard` | Upper Courtyard | Upper | TBD | — |
| `Church` | Church | Upper | TBD | — |
| `Gatehouse` | Gatehouse | Ground/Upper | TBD | — |
| `LivingQuarters` | Small bedroom, Samantha's Room | Upper | TBD | — |
| `KnightsHall` | Knight's Hall | Upper | TBD | — |
| `Armory` | Armory (power room) | Upper | TBD | — |
| `Bastion` | Bastion (Death Ray) | Upper, outdoors | TBD | — |
| `Clocktower` | Clocktower | Upper | TBD | — |
| `TrophyRoom` | Trophy Room | Below Clocktower | TBD | — |
| `Undercroft` | Undercroft (pyramid, Jug, teleporter) | Underground | TBD | — |
| `RocketPad` | Rocket Test Pad | Separate area | TBD | — |

The **Editor** column is how we avoid editing the same section at once: write your name there when you start working on a section, and clear it when you push.

## 5. Object naming

Format: `Type_<SectionId>_<Detail>`, PascalCase, no spaces. Numbers use two digits.

| Object | Pattern | Example |
|---|---|---|
| Room model | `Room_<SectionId>` | `Room_LowerCourtyard` |
| Door between sections | `Door_<From>_<To>` (alphabetical order) | `Door_LowerCourtyard_Spawn` |
| Power-locked door | `PowerDoor_<From>_<To>` | `PowerDoor_LowerCourtyard_Undercroft` |
| Barricade / window | `Barricade_<SectionId>_<NN>` | `Barricade_Spawn_01` |
| Zombie spawn | `ZombieSpawn_<SectionId>_<NN>` | `ZombieSpawn_KnightsHall_02` |
| Player spawn | `PlayerSpawn_<NN>` | `PlayerSpawn_01` |
| Wall-buy | `WallBuy_<SectionId>_<Weapon>` | `WallBuy_LowerCourtyard_Vesper` |
| Perk machine | `Perk_<SectionId>_<Perk>` | `Perk_Undercroft_Juggernog` |
| Mystery Box spot | `MysteryBox_<SectionId>_<NN>` | `MysteryBox_LowerCourtyard_01` |
| Power switch | `PowerSwitch_Main` | — |
| Trap | `Trap_<SectionId>_<Name>` | `Trap_Bastion_DeathRay` |
| Teleporter / launch pad | `Teleporter_<SectionId>`, `LaunchPad_<From>_<To>` | `LaunchPad_Bastion_RocketPad` |
| Landmark | `Landmark_<SectionId>_<Name>` | `Landmark_Undercroft_Pyramid` |

**Gameplay data goes in attributes, not names.** Examples: a door's `Cost` and `DoorId`, a spawn's `SectionId`. Scripts read attributes, so renaming a visual model never breaks gameplay (`ARCHITECTURE.md` §7).

## 6. Blockout rules (for MAP-004)

- All blockout parts are **Anchored**, `SmoothPlastic`, and named `Floor`, `Wall`, `Ceiling`, `Stairs` or `Ramp`.
- Each section uses **one solid colour**, so section boundaries are visible at a glance. Doors are bright yellow.
- No props, textures or lighting until the layout is approved (`GAME_BIBLE.md` §2).
- Scripts or Studio automation that create geometry may only touch **one** `Room_<SectionId>` model per run (`AI_RULES.md` §8).
- After blocking out a section, walk it with a default character and record its anchor in §4.

## 7. Decisions needed from the team

- [ ] Agree on the scale of 1 m = 3.5 studs, after the test doorway.
- [ ] Agree on Spawn as the origin and North = −Z.
- [ ] Agree on the section list in §4 (add, merge or rename sections now, before building).
- [ ] Agree on the naming patterns in §5.
- [ ] Confirm the project place: Project Zomblox (81227088977620, empty) or Arlo num num (95925940792219, existing build).
