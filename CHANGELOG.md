# CHANGELOG — Roblox Zombies

This file records meaningful changes to the project, including map edits, scripts, architecture, gameplay behavior, and bug fixes.

Entries should be factual and concise. Record what actually changed, who made the change, and what was tested.

## Change Entry Template

### [YYYY-MM-DD] — [Short description]

- **Task ID:** 
- **Author / Implementer:** 
- **Reviewer:** 
- **Category:** Map / Gameplay / Architecture / UI / Audio / Bug Fix / Documentation
- **Status:** Implemented / Reviewed / Tested

**Changes made:**
- 

**Files or map sections affected:**
- 

**Testing performed:**
- 

**Known issues or risks:**
- 

**Follow-up tasks:**
- 

---

## Project History

### [2026-10-13] — Remove imported Call of Duty asset data

- **Task ID:** GAME-001 follow-up (`STUDIO_AUDIT.md` §5, item 1)
- **Author / Implementer:** Claude, at the project owner's request
- **Reviewer:** Pending
- **Category:** Bug Fix / Assets
- **Status:** Implemented

**Changes made:**
- Deleted `ServerStorage.ImportedData`: 208 modules of mesh and texture data named after Black Ops III asset files (dragon, keeper, Apothicon sword, Gauntlet of Siegfried, Skull of Nan Sapwe, skeleton, zombie head).
- `ReplicatedStorage.Citadel.Config`: removed `ImportedModel` from the Sword, Skull and Gauntlet, so they use the standard weapon viewmodel.
- `ReplicatedStorage.Citadel.ImportedMesh`: `Prepare()` now returns early when `ImportedData` is missing.
- `CitadelClient.ZombieVisuals`: skips the imported skeleton when no templates exist (previously the client would wait 45 seconds for them); zombies show the default rig.
- All edits were recorded as one Studio undo step.

**Files or map sections affected:**
- Studio, "Arlo num num": `ServerStorage.ImportedData` (deleted), `ReplicatedStorage.Citadel.Config`, `ReplicatedStorage.Citadel.ImportedMesh`, `StarterPlayerScripts.CitadelClient.ZombieVisuals`.

**Testing performed:**
- All four affected scripts, plus server and client `Main`, compile (checked with `loadstring`).
- No objects with Black Ops III asset names remain in the place.
- NOT TESTED in play: wonder weapon viewmodels and zombie appearance have not been checked in a playtest.

**Known issues or risks:**
- The 18 `Texture_Perk_*` modules (perk logo artwork) and Call of Duty names in `Config` and `PerkMachines` remain; awaiting a team decision.
- The deletion can be undone with Studio undo during this session, or from the place's version history afterwards.

**Follow-up tasks:**
- Playtest the wonder weapons and zombies.
- Decide on the perk artwork and names.

---

### [2026-10-13] — Ironheart respects the four-perk limit

- **Task ID:** GAME-001 follow-up
- **Author / Implementer:** Claude
- **Reviewer:** Pending
- **Category:** Bug Fix
- **Status:** Implemented

**Changes made:**
- Added one line to the purchase handler in `ServerScriptService.CitadelServer.Main` (line 134): buying Ironheart is refused with "Four-perk limit reached." when the player already holds four perks, matching the check `Progression` uses for the other nine perks.

**Files or map sections affected:**
- Studio: `ServerScriptService.CitadelServer.Main` in "Arlo num num" (place ID 95925940792219).

**Testing performed:**
- The script compiles (checked with `loadstring` in Studio).
- NOT TESTED in play: buying four perks and then Ironheart has not been tried.

**Known issues or risks:**
- None known.

**Follow-up tasks:**
- Playtest: buy four perks, then try Ironheart.

---

### [2026-10-13] — Audit of the "Arlo num num" Studio place

- **Task ID:** GAME-001
- **Author / Implementer:** Claude
- **Reviewer:** cameron290 (pending)
- **Category:** Documentation
- **Status:** Implemented

**Changes made:**
- Created `Docs/STUDIO_AUDIT.md` documenting the existing build: about 21,400 map parts, about 50 game scripts, and 208 imported data modules.
- Put the MAP-003 proposal on hold, because the existing build uses a much larger scale.
- Moved GAME-001 to REVIEW.

**Files or map sections affected:**
- `Docs/STUDIO_AUDIT.md` (new), `Docs/MAP_BUILD_PLAN.md`, `TASK_BOARD.md`, `CHANGELOG.md`. No Studio changes.

**Testing performed:**
- NOT TESTED — read-only inspection. No playtest was run, and `CitadelServer.Tests` was not run.

**Known issues or risks:**
- Imported Call of Duty asset data in `ServerStorage.ImportedData`.
- The map is modified at runtime by `Reconstruction` and `LayoutRebuild`.
- Ironheart can be bought past the 4-perk limit. (Corrected: an earlier note said every perk machine granted Ironheart, which was wrong.)

**Follow-up tasks:**
- Team decisions in `STUDIO_AUDIT.md` §5; revise MAP-003 and `ARCHITECTURE.md` to match the existing build.

---

### [2026-10-13] — Propose map scale, coordinates and naming

- **Task ID:** MAP-003
- **Author / Implementer:** Claude
- **Reviewer:** cameron290 (pending)
- **Category:** Documentation / Architecture
- **Status:** Implemented (proposal)

**Changes made:**
- Created `Docs/MAP_BUILD_PLAN.md`: scale (1 m = 3.5 studs), origin at the Spawn floor, North = −Z, 14 stable section IDs, object naming patterns, and blockout rules.
- Linked it from `ARCHITECTURE.md` §7; moved MAP-003 to REVIEW.

**Files or map sections affected:**
- `Docs/MAP_BUILD_PLAN.md` (new), `ARCHITECTURE.md`, `TASK_BOARD.md`, `CHANGELOG.md`

**Testing performed:**
- NOT TESTED — no Studio place was open, so the conventions were not checked against existing objects, and the scale has not been tried with a test doorway.

**Known issues or risks:**
- The scale is a starting value; confirm it with a test doorway before building rooms.

**Follow-up tasks:**
- Team agreement on `MAP_BUILD_PLAN.md` §7, then MAP-004 (blockout).

---

### [2026-10-13] — Draft Der Eisendrache map reference

- **Task ID:** MAP-002
- **Author / Implementer:** Claude
- **Reviewer:** Pending
- **Category:** Documentation
- **Status:** Implemented (draft)

**Changes made:**
- Created `Docs/MAP_REFERENCE.md`: areas, connections, perks, wall-buys, power, Pack-a-Punch, Wunderspheres, traps and dragon statues, each tagged with a confidence level.
- Marked MAP-002 IN PROGRESS on `TASK_BOARD.md`.

**Files or map sections affected:**
- `Docs/MAP_REFERENCE.md` (new), `TASK_BOARD.md`, `CHANGELOG.md`

**Testing performed:**
- NOT TESTED — documentation only. Facts come from written guides and have not been checked against gameplay footage.

**Known issues or risks:**
- Several room connections and Wundersphere pairs conflict between sources (marked ❓).
- Door costs, Mystery Box spots and zombie spawn windows are not yet recorded.

**Follow-up tasks:**
- Verify against a full map walkthrough video; then MAP-003.

---

### [2026-10-13] — First map selected: Der Eisendrache

- **Task ID:** MAP-001
- **Author / Implementer:** Project owner (decision); Claude (documentation)
- **Reviewer:** Pending — team
- **Category:** Documentation
- **Status:** Implemented

**Changes made:**
- Recorded Der Eisendrache (Black Ops III, Awakening DLC) as the first map.
- Moved MAP-001 to REVIEW pending team agreement on target scope.

**Files or map sections affected:**
- `GAME_BIBLE.md`, `TASK_BOARD.md`, `ARCHITECTURE.md`, `README.md`, `CHANGELOG.md`

**Testing performed:**
- NOT TESTED — documentation only; no Studio changes.

**Known issues or risks:**
- Target scope (which areas of the map to build first) is not yet agreed.

**Follow-up tasks:**
- MAP-002 (collect references), MAP-003 (coordinates and naming).

---

### [Initial Setup] — Shared Development Documentation

- **Category:** Documentation
- **Status:** Created

**Changes made:**
- Established the shared Game Bible.
- Established a proposed architecture document.
- Established a task ownership and progress board.
- Established shared AI collaboration rules.
- Established this changelog.

**Files or map sections affected:**
- `GAME_BIBLE.md`
- `ARCHITECTURE.md`
- `TASK_BOARD.md`
- `AI_RULES.md`
- `README.md`
- `CHANGELOG.md`

**Testing performed:**
- Documentation templates prepared for team review.
- Roblox Studio implementation has not been verified by this entry.

**Known issues or risks:**
- The selected reference map remains undecided.
- The proposed architecture must be compared against the actual Roblox Studio hierarchy.
- No gameplay implementation should be assumed complete based on documentation alone.

---

## Important Decisions

Record major decisions that affect the project's direction.

| Date | Decision | Reason | Approved by |
|---|---|---|---|
| 2026-10-13 | Initial map: Der Eisendrache | Establish a clear map-building target | Project owner |
| TBD | Approve final system architecture | Avoid conflicting implementations | Team |
| TBD | Set target player count | Guide multiplayer and performance testing | Team |

## Logging Rules

- Never claim a test passed unless it was actually performed.
- Record failed tests and unresolved issues.
- Mention deleted or renamed scripts explicitly.
- Record changes to map coordinates, room connections, or gameplay object identifiers.
- Do not include secrets, credentials, or private access tokens.
- Add new entries at the top of the project history once actual development begins.
