# ARCHITECTURE — Roblox Zombies

## 1. Purpose

This document defines the Roblox project's Explorer hierarchy, system responsibilities, communication interfaces, and technical rules.

The goal is to keep the codebase organized so multiple developers and AI assistants can collaborate without creating conflicting systems.

**Important:** Proposed structures below are plans, not confirmation that these objects already exist. Inspect Roblox Studio before creating, renaming, or modifying anything.

## 2. Core Architecture Principles

- Keep gameplay systems modular.
- Use server-authoritative logic for important gameplay actions.
- Keep shared configuration separate from gameplay logic.
- Avoid duplicate systems with overlapping responsibilities.
- Use consistent names for scripts, folders, RemoteEvents, and map objects.
- Make changes within the assigned task's scope.
- Document approved architectural changes.
- Prioritize map accuracy and reliable navigation.

## 3. Proposed Roblox Explorer Hierarchy

The following hierarchy is a proposed target structure. Adapt it to the existing project after inspecting Roblox Studio.

Workspace
- Map
  - Rooms
  - Corridors
  - Doors
  - Barricades
  - Interactables
  - PlayerSpawns
  - ZombieSpawns
- Gameplay
  - PurchasePoints
  - PowerSwitches
  - InteractionMarkers
- LiveEntities
  - Zombies
  - DroppedItems

ReplicatedStorage
- Shared
  - Config
    - WeaponConfig
    - ZombieConfig
    - RoundConfig
    - MapConfig
  - Types
  - Utilities
- Remotes
  - CombatRemote
  - InteractionRemote
  - WeaponRemote
  - UIUpdateRemote
- Assets
  - Weapons
  - Zombies
  - Effects
  - Audio

ServerScriptService
- Bootstrap.server.lua
- Services
  - RoundService
  - ZombieService
  - CombatService
  - PointsService
  - InteractionService
  - MapStateService
  - WeaponService

StarterPlayer
- StarterPlayerScripts
  - Client
    - InputController
    - WeaponController
    - InteractionController
    - UIController

StarterGui
- HUD
- Menus
- GameOverUI

ServerStorage
- ServerAssets
  - ZombieTemplates
  - WeaponTemplates

## 4. System Responsibilities

### RoundService
Owns:
- Current round.
- Round transitions.
- Zombie spawn budgets.
- Round completion conditions.
- Round difficulty progression.

Does not own:
- Weapon damage.
- Player point balances.
- Physical map construction.

### ZombieService
Owns:
- Zombie spawning and lifecycle.
- Zombie AI coordination.
- Target selection.
- Zombie cleanup.
- Coordination with round spawning.

Does not own:
- Player point balances.
- Purchase validation.
- Weapon firing input.

### CombatService
Owns:
- Server-side combat validation.
- Damage application.
- Hit validation.
- Kill attribution where required.
- Communication with PointsService after valid gameplay events.

Does not trust the client to decide whether damage or kills are valid.

### WeaponService
Owns:
- Weapon state and server-side firing validation.
- Ammunition and reload state where applicable.
- Weapon configuration.
- Weapon purchase or equip integration.

### PointsService
Owns:
- Player point balances.
- Valid point rewards.
- Point deductions.
- Purchase affordability checks.
- Consistent point updates.

### InteractionService
Owns:
- Validating player interaction requests.
- Checking distance and eligibility.
- Routing approved interactions to the appropriate system.
- Preventing repeated or unauthorized interaction requests.

### MapStateService
Owns:
- Shared map progression state.
- Door states.
- Power state.
- Other approved map-wide unlocks.

Physical map objects should not independently implement competing progression systems.

## 5. Shared Interfaces

These are proposed interface contracts. Confirm and document actual function names and parameters before implementation.

| System | Example interface | Purpose |
|---|---|---|
| RoundService | `GetCurrentRound()` | Returns the current round |
| RoundService | `StartNextRound()` | Starts the next round through approved server logic |
| ZombieService | `SpawnZombie(spawnId, configId)` | Requests a configured zombie spawn |
| PointsService | `GetPoints(player)` | Reads a player's balance |
| PointsService | `AwardPoints(player, amount, reason)` | Awards a validated reward |
| PointsService | `TrySpendPoints(player, amount, reason)` | Attempts a server-side deduction |
| MapStateService | `GetDoorState(doorId)` | Reads a door's shared state |
| MapStateService | `TryUnlockDoor(player, doorId)` | Attempts an approved door purchase |
| CombatService | `ApplyValidatedDamage(...)` | Applies damage after server validation |

The examples above are not authorization to create these exact functions immediately. Review existing scripts and establish a consistent interface before implementation.

## 6. Remote Communication

RemoteEvents and RemoteFunctions are communication mechanisms, not security boundaries.

Client requests may include:
- Fire a weapon.
- Reload a weapon.
- Interact with a door.
- Request an interaction.
- Request an approved weapon purchase.

The server must validate:
- Player eligibility.
- Distance to the target.
- Weapon ownership and state.
- Ammunition and fire rate.
- Target validity.
- Purchase cost and point balance.
- Request frequency.
- Whether the requested action is currently permitted.

Clients must never directly determine:
- Zombie health or death.
- Awarded points.
- Purchase success.
- Round state.
- Authoritative damage.
- Shared door or power state.

Never create new remotes without checking whether an existing approved remote can serve the same purpose.

## 7. Map Object Conventions

Use consistent names and identifiers for gameplay objects.

Examples:
- `Room_StartingRoom`
- `Door_Courtyard`
- `ZombieSpawn_Corridor01`
- `PlayerSpawn_01`
- `Purchase_WallWeapon01`
- `PowerSwitch_Main`

Gameplay identifiers should remain stable even if visual models are adjusted.

The full scale, coordinate, section ID and naming rules for Der Eisendrache are in `Docs/MAP_BUILD_PLAN.md` (proposed in MAP-003).

Where practical, store gameplay properties in configuration or clearly defined attributes instead of relying on arbitrary object names.

Before changing map coordinates, room connections, or named gameplay objects, confirm the change is approved.

## 8. Runtime Ownership

- Static geometry belongs in the map hierarchy.
- Runtime zombies belong in the designated live-entity hierarchy.
- Zombie templates belong in a server-controlled storage location.
- Shared configuration belongs in an agreed shared configuration location.
- Client-only interface behavior belongs in client scripts.
- Authoritative gameplay decisions belong on the server.

Avoid unnecessary duplication of models, controllers, or gameplay state.

## 9. Map Development Requirements

Map construction is the project's first major priority.

Before detailed decoration:
1. Confirm the reference map.
2. Establish coordinate and scale conventions.
3. Build the blockout.
4. Validate room connections and elevation.
5. Test player collision and movement.
6. Test zombie pathfinding.
7. Approve the layout before extensive detailing.

Any automation that creates or edits geometry must be restricted to an explicitly assigned room, section, or object group.

## 10. Change Policy

Before making architectural changes:
1. Identify the affected systems and dependencies.
2. Check the current Roblox Studio hierarchy.
3. Explain the proposed change.
4. Obtain approval for breaking changes.
5. Update this document after implementation.

Never silently rename, delete, replace, or rewrite established systems.

## 11. Testing Requirements

Test changes in isolation before testing integration.

Minimum checks where applicable:
- No new script errors.
- No broken references.
- No duplicate gameplay controllers.
- Server-side validation works.
- Multiplayer state remains consistent.
- Map navigation still works.
- No unintended geometry changes.
- Existing approved features still work.

Record what was actually tested and any remaining issues in `TASK_BOARD.md` or `CHANGELOG.md`.

## 12. Architecture Decisions

Record approved decisions here.

| Date | Decision | Reason |
|---|---|---|
| 2026-10-13 | First map: Der Eisendrache (Black Ops III) | Chosen by project owner |
| TBD | Final service structure | Awaiting inspection of current project |
| TBD | Target player count | Awaiting team decision |

Update this document whenever an approved architectural decision changes.
