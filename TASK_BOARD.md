# TASK BOARD — Roblox Zombies

## 1. Purpose

This board tracks development tasks, ownership, dependencies, reviews, testing, and completion.

Every meaningful change should have a task. Keep tasks small enough that one developer or AI assistant can complete them without unnecessarily modifying unrelated systems.

## 2. Status Definitions

- **PLANNED:** Defined but not started.
- **IN PROGRESS:** Work is actively being performed.
- **REVIEW:** Implementation is ready for review.
- **TESTING:** Review passed and the change is being tested.
- **BLOCKED:** Work cannot continue until a dependency or decision is resolved.
- **DONE:** Acceptance criteria have been met and required tests have passed.

## 3. Ownership Rules

- Each task must have one primary owner.
- Identify which AI assistant is implementing and which is reviewing, if applicable.
- Do not let multiple AI assistants edit the same script or map section simultaneously.
- The reviewer should check the actual implementation, not just the written explanation.
- The project integrator resolves conflicts and approves shared interface changes.
- Never mark work DONE based only on an AI's claim that it is finished.

## 4. Current Project Priorities

### Phase 1 — Planning and Reference Collection

- [ ] **MAP-001 — Select the First Reference Map**
  - Status: REVIEW
  - Decision: Der Eisendrache (Black Ops III, Awakening DLC). Map name and reference version recorded in `GAME_BIBLE.md`; team agreement on target scope still pending.
  - Owner: Team
  - Implementer: Team
  - Reviewer: Team
  - Dependencies: None
  - Scope: Decide which Call of Duty Zombies map to recreate first.
  - Acceptance criteria:
    - The map is named in `GAME_BIBLE.md`.
    - The reference game/version is documented.
    - The team agrees on the target scope.

- [ ] **MAP-002 — Collect Map References**
  - Status: IN PROGRESS
  - Owner: adencmath-dotcom
  - Implementer: Claude
  - Reviewer: TBD
  - Progress: Draft `Docs/MAP_REFERENCE.md` created from written guides. Still needs footage verification, door costs, Mystery Box spots, and zombie spawn windows.
  - Dependencies: MAP-001
  - Scope: Collect screenshots, layout references, and relevant video footage.
  - Acceptance criteria:
    - Important rooms and connections are documented.
    - Major landmarks are identified.
    - Reference materials are organized in `Docs/MAP_REFERENCE.md`.

- [ ] **MAP-003 — Establish Map Coordinates and Naming**
  - Status: REVIEW
  - Owner: adencmath-dotcom
  - Implementer: Claude
  - Reviewer: cameron290
  - Progress: Proposal written in `Docs/MAP_BUILD_PLAN.md`. **On hold:** the GAME-001 audit found an existing build in "Arlo num num" at a much larger scale, so the proposal must be revised to match it (see `Docs/STUDIO_AUDIT.md`).
  - Dependencies: MAP-001
  - Scope: Establish a shared scale, coordinate conventions, and object naming rules.
  - Acceptance criteria:
    - The team agrees on map coordinates and naming.
    - Map sections have stable identifiers.
    - Instructions are recorded in `ARCHITECTURE.md` or `Docs/MAP_BUILD_PLAN.md`.

### Phase 2 — Map Blockout

- [ ] **MAP-004 — Build the Map Blockout**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: MAP-002, MAP-003
  - Scope: Construct the main rooms, corridors, stairs, and connections using simple geometry.
  - Acceptance criteria:
    - The main layout matches the approved reference as closely as practical.
    - All required rooms are connected correctly.
    - Room proportions and elevation changes have been reviewed.
    - Detailed decoration has not obscured unresolved layout issues.

- [ ] **MAP-005 — Validate Navigation and Collision**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: MAP-004
  - Scope: Test player movement, collision, and planned zombie routes.
  - Acceptance criteria:
    - Players can traverse intended routes.
    - Required passages are not unintentionally blocked.
    - Zombie navigation has been tested.
    - Identified problems are documented.

- [ ] **MAP-006 — Detail the Approved Map Layout**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: MAP-005
  - Scope: Add major structures, landmarks, materials, props, lighting, and atmosphere.
  - Acceptance criteria:
    - The approved layout remains intact.
    - The major landmarks are recognizable.
    - Performance is checked.
    - Unintended geometry changes are avoided.

### Phase 3 — First Playable Gameplay Loop

- [ ] **GAME-001 — Inspect and Document Existing Scripts**
  - Status: REVIEW
  - Owner: adencmath-dotcom
  - Implementer: Claude
  - Reviewer: cameron290
  - Progress: Audit of "Arlo num num" written to `Docs/STUDIO_AUDIT.md`. Found a working prototype ("FROSTBOUND — The Citadel") and six decisions for the team (§5), including imported Call of Duty assets.
  - Dependencies: Access to the current Roblox Studio project
  - Scope: Audit the actual hierarchy and existing scripts before creating replacements.
  - Acceptance criteria:
    - Existing gameplay systems are documented.
    - Existing and planned objects are clearly distinguished.
    - Duplicate systems and risks are identified.

- [ ] **GAME-002 — Implement One Basic Weapon**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: GAME-001
  - Scope: Implement a single usable weapon.
  - Acceptance criteria:
    - Firing and reloading work.
    - Ammunition is tracked correctly.
    - Damage is validated by the server.
    - The weapon can be tested in multiplayer.

- [ ] **GAME-003 — Implement One Basic Zombie**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: MAP-005, GAME-001
  - Scope: Implement spawning, pursuit, attacks, damage, death, and cleanup.
  - Acceptance criteria:
    - Zombies spawn at approved locations.
    - Zombies pursue and attack players.
    - Zombies take damage and die correctly.
    - Cleanup works without leaving broken entities.

- [ ] **GAME-004 — Implement Points**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: GAME-001, GAME-002, GAME-003
  - Scope: Implement server-authoritative point rewards and spending.
  - Acceptance criteria:
    - Valid actions award the correct configured points.
    - Invalid client requests cannot award points.
    - Balances update correctly.
    - Point spending cannot produce unauthorized purchases.

- [ ] **GAME-005 — Implement Round Progression**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: GAME-003
  - Scope: Implement round starts, zombie spawn budgets, round completion, and difficulty progression.
  - Acceptance criteria:
    - Rounds start and end correctly.
    - Zombie counts and difficulty follow configuration.
    - The game does not get stuck between rounds.
    - Player deaths and departures are handled appropriately.

- [ ] **GAME-006 — Implement Initial HUD**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: GAME-002, GAME-004, GAME-005
  - Scope: Display round, points, weapon information, and ammunition.
  - Acceptance criteria:
    - The HUD displays the correct values.
    - Values remain synchronized with the server.
    - No unrelated UI is introduced.

### Phase 4 — Map Progression and Testing

- [ ] **MAP-007 — Implement Purchasable Doors**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: TBD
  - Reviewer: TBD
  - Dependencies: GAME-004, approved map layout
  - Scope: Implement server-validated door purchases.
  - Acceptance criteria:
    - Door costs are configurable.
    - Successful purchases deduct points exactly once.
    - Failed purchases do not deduct points.
    - Door state is consistent across players.

- [ ] **TEST-001 — Full Gameplay Playtest**
  - Status: PLANNED
  - Owner: TBD
  - Implementer: Team
  - Reviewer: Team
  - Dependencies: GAME-002 through GAME-006
  - Scope: Play from the first round until game over.
  - Acceptance criteria:
    - The complete gameplay loop works.
    - Errors and unexpected behavior are documented.
    - Multiplayer issues are recorded.
    - Known issues have assigned follow-up tasks.

## 5. Active Work

Add tasks here when implementation begins.

### Task Template

**Task ID:**  
**Feature:**  
**Status:** PLANNED / IN PROGRESS / REVIEW / TESTING / BLOCKED / DONE  
**Owner:**  
**Implementing AI:**  
**Reviewing AI:**  
**Dependencies:**  
**Authorized files or map sections:**  

**Required behavior:**
- 

**Acceptance criteria:**
- 

**Tests required:**
- 

**Known issues:**
- 

**Related changes:**
- 

## 6. Blocked Tasks

Record anything waiting on a decision, dependency, or access.

| Task ID | Blocker | Needed from | Next action |
|---|---|---|---|
| None recorded | — | — | — |

## 7. Completed Tasks

Move completed tasks here or mark them DONE in the active sections.

| Task ID | Completed date | Verified by | Notes |
|---|---|---|---|
| None yet | — | — | — |

## 8. Task Completion Rules

A task can be marked DONE only when:
1. The requested change is implemented.
2. The implementation remains within the approved scope.
3. Acceptance criteria are satisfied.
4. Required tests were actually performed.
5. The reviewer has checked the changes.
6. Relevant documentation is updated.
7. Any remaining limitations are recorded.

Do not mark a task DONE if it has only been written, planned, or partially implemented.
