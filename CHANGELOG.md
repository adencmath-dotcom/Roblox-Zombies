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
