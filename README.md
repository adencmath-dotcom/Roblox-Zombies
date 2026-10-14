# Roblox Zombies — Development Repository

## Project Overview

This repository contains the shared documentation, planning, architecture, task tracking, and collaboration rules for a Roblox Zombies game inspired by Call of Duty Zombies, particularly Black Ops 3.

The project aims to deliver a faithful, polished, cooperative, round-based zombie survival experience on Roblox.

**First priority:** Recreate one selected Zombies map as accurately as practical, then build a complete playable gameplay loop around it.

This repository is the shared planning hub for the human development team and AI assistants.

**Important:** This GitHub repository does not automatically synchronize Roblox Studio scripts or geometry. Roblox Studio Team Create remains the shared live development environment unless a separate code synchronization workflow is configured.

## Project Goals

- Recreate one recognizable Zombies map.
- Preserve the reference layout, landmarks, and navigation.
- Implement round-based zombie survival.
- Implement weapons, combat, and points.
- Add map progression through doors and other interactions.
- Support cooperative multiplayer.
- Maintain modular, documented, secure gameplay systems.
- Use AI assistants without conflicting edits or accidental overwrites.

## Documentation Guide

| File | Purpose |
|---|---|
| `GAME_BIBLE.md` | Game vision, gameplay requirements, and development priorities |
| `ARCHITECTURE.md` | Proposed Explorer hierarchy, system responsibilities, and interfaces |
| `TASK_BOARD.md` | Tasks, owners, dependencies, progress, and acceptance criteria |
| `CHANGELOG.md` | History of meaningful project changes and decisions |
| `AI_RULES.md` | Shared instructions for Claude, ChatGPT, and other AI contributors |
| `Docs/MAP_REFERENCE.md` | Screenshots, reference links, landmarks, and layout notes |
| `Docs/MAP_BUILD_PLAN.md` | Map sections, construction order, coordinates, and validation |
| `Docs/TESTING.md` | Playtest procedures and regression checklists |

Some documents may not exist yet. Create them as the project develops.

## Development Workflow

### 1. Select a task

Review `TASK_BOARD.md` and choose a task with clear acceptance criteria.

### 2. Assign one implementer

Choose one primary developer or AI assistant to implement the task. Assign another person or AI to review it when practical.

### 3. Confirm scope

Identify the exact scripts, folders, map sections, or objects that may be changed.

Avoid concurrent edits to the same script or map section.

### 4. Implement and test

Make the smallest change that satisfies the task. Test it in Roblox Studio when possible.

### 5. Review and integrate

Check the actual changes, confirm that existing features still work, and resolve any conflicts.

### 6. Update documentation

Record meaningful changes in `CHANGELOG.md`. Update architecture, task status, or map documentation when necessary.

## Map-First Development Plan

1. Choose the first reference map.
2. Collect reference materials.
3. Establish map coordinates and naming conventions.
4. Build the full blockout.
5. Validate player collision and zombie navigation.
6. Approve the layout.
7. Add landmarks, details, lighting, and atmosphere.
8. Implement one weapon and one basic zombie.
9. Implement points and round progression.
10. Add map progression and multiplayer testing.
11. Polish and expand only after the core loop is stable.

Do not heavily detail an unapproved blockout or make large-scale map changes without approval.

## AI Collaboration Rules

Every AI assistant must follow `AI_RULES.md`.

Before making changes, the assistant should:
- Read relevant project documentation.
- Inspect the actual Studio hierarchy and scripts when access is available.
- Confirm the assigned task and authorized scope.
- Check for conflicting edits.
- Preserve existing work.
- Report changes and actual test results honestly.

No AI assistant should assume it has access to another assistant's conversation history.

## Technical Notes

The architecture documented in `ARCHITECTURE.md` may initially be a proposal. It must be reconciled with the actual Roblox Studio project before new systems are implemented.

Important gameplay decisions, including damage, points, purchases, and round progression, must be validated on the server.

Use original, licensed, or otherwise authorized assets where appropriate.

## Current Project Status

- **Development stage:** Early planning and setup.
- **First map:** Not yet finalized.
- **Map blockout:** Not confirmed complete.
- **Gameplay systems:** Must be audited in Roblox Studio before their status is declared.
- **Next milestone:** Select the reference map and document its layout.

Update this section as verified progress is made.

## Repository Maintenance

- Keep documentation current.
- Use descriptive task IDs.
- Record important decisions and changes.
- Never include passwords, API keys, or other secrets.
- Do not claim an implementation or test is complete without verification.
- Use version history and appropriate backups before major changes.

## Important Links

- **Roblox Studio:** https://create.roblox.com/
- **Roblox Creator Documentation:** https://create.roblox.com/docs
- **GitHub Documentation:** https://docs.github.com/


