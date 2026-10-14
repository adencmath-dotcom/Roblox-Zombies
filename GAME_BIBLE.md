# GAME BIBLE — Roblox Zombies

**Project Status:** Early Development  
**Genre:** First-Person Co-op Zombie Survival  
**Platform:** Roblox  
**Primary Reference:** Call of Duty Zombies, particularly Black Ops 3  
**Development Team:** Two developers using Roblox Studio, Team Create, Claude, and ChatGPT

---

## 1. Game Vision

Create a high-quality Roblox zombie survival game inspired by the classic Call of Duty Zombies experience.

The goal is to recreate the atmosphere, map design, tension, progression, and satisfying gameplay loop of classic Zombies while adapting the experience to Roblox.

**Our first priority is building one faithful, fully playable map.** We should prioritize map accuracy, layout, atmosphere, and navigation before expanding the game with additional maps or large numbers of weapons and features.

The game should feel like a carefully crafted Zombies experience, not a generic Roblox zombie simulator.

### Core Design Pillars

1. **Map authenticity:** The initial map should closely match its chosen reference in layout, proportions, landmarks, and atmosphere.
2. **Faithful gameplay:** Preserve the familiar round-based survival loop, points, zombie progression, weapons, and map progression.
3. **Atmosphere:** Lighting, sound, environmental storytelling, and visual details should create tension.
4. **Responsive combat:** Weapons, zombie movement, hit detection, and player feedback should feel satisfying.
5. **Multiplayer cooperation:** Players should be able to survive together, revive teammates if implemented, and work toward shared objectives.
6. **Maintainable code:** Systems must be modular, documented, and safe for multiple developers and AI assistants to work on.

---

## 2. Map Specification

**Initial Map:** TBD — choose the reference map before detailed construction.

**Primary Objective:** Recreate one selected Zombies map as faithfully as practical within Roblox Studio.

### Map Development Priorities

- Match the reference map's overall layout and proportions.
- Recreate room connections, corridors, stairs, chokepoints, and major landmarks.
- Preserve recognizable sightlines and navigation routes.
- Match the placement of major gameplay areas, doors, barricades, and interactable objects where practical.
- Use appropriate materials, lighting, props, and environmental details.
- Ensure players and zombies can navigate the map reliably.
- Validate collision, zombie pathfinding, spawn locations, and multiplayer performance.

### Map Construction Order

1. Collect reference screenshots, videos, and layout information.
2. Create a rough blockout of the complete map.
3. Verify room sizes, connections, elevation changes, and navigation.
4. Test player movement and zombie pathfinding.
5. Add major structures, recognizable landmarks, and map-specific features.
6. Add smaller props, materials, lighting, sounds, and atmosphere.
7. Add gameplay elements such as doors, barricades, power switches, and purchase locations.
8. Perform repeated playtests and correct layout issues.

**Important:** Do not heavily detail rooms before their layout and proportions have been reviewed. Avoid changing established map coordinates or room connections without approval.

### Map Reference

- **Map name:** TBD
- **Reference game/version:** TBD
- **Primary reference materials:** To be documented in `Docs/MAP_REFERENCE.md`
- **Map layout/build plan:** To be documented in `Docs/MAP_BUILD_PLAN.md`

---

## 3. Core Gameplay Loop

The intended gameplay loop is:

1. Players spawn into the map.
2. Zombies spawn and pursue players.
3. Players defeat zombies and earn points.
4. Players spend points on weapons, doors, and other available map features.
5. Later rounds introduce more challenging zombie encounters.
6. Players expand their accessible play area and improve their equipment.
7. The game continues until all players are eliminated or another defined ending condition is reached.

### Round Progression

The round system should eventually support:

- A starting round with manageable difficulty.
- Increasing zombie counts and difficulty across rounds.
- A clear indication of the current round.
- Tracking of remaining zombies.
- A transition between rounds.
- A short break between rounds where appropriate.
- A defined game-over condition.
- Reliable handling of players joining, leaving, dying, or respawning.

Exact zombie counts, health, speed, spawn rates, and difficulty scaling will be defined in configuration rather than scattered throughout scripts.

---

## 4. Points and Economy

Players earn points through gameplay and spend them to unlock progression.

Potential point-earning actions include:

- Damaging zombies.
- Eliminating zombies.
- Repairing barricades, if included.
- Other map-specific interactions approved by the team.

Potential purchases include:

- Opening locked doors.
- Buying weapons.
- Purchasing ammunition.
- Activating specific map features.
- Other progression systems approved by the team.

Exact point values and prices are **TBD** and should be configurable.

### Economy Rules

- The server must validate point rewards and purchases.
- Clients must never be trusted to award themselves points or authorize purchases.
- Purchases must not succeed if the player lacks sufficient points.
- A successful purchase must deduct the correct amount exactly once.
- Failed purchases must not consume points.
- UI displays must stay synchronized with server-authoritative values.

---

## 5. Zombies

Zombies are the primary enemy and should reproduce the recognizable behavior of classic round-based Zombies.

### Required Behavior

- Spawn at approved locations.
- Detect and pursue valid targets.
- Navigate rooms and corridors.
- Attack players within an appropriate range.
- Take damage and die.
- Reward players according to the approved points rules.
- Be cleaned up correctly after death or removal.
- Scale in difficulty as rounds progress.

### Design Requirements

- Zombie health, speed, damage, and spawn behavior should be configurable.
- Pathfinding must account for doors, obstacles, and map navigation.
- Zombies should not become permanently stuck during normal gameplay.
- Spawn logic must avoid unfairly placing enemies directly on top of players.
- The server controls zombie health, damage, death, and rewards.

Special zombies and boss enemies are out of scope until the basic zombie experience is stable.

---

## 6. Weapons and Combat

The initial playable version should focus on one reliable weapon before adding a large arsenal.

### Weapon Requirements

- Responsive player input.
- Accurate hit detection.
- Server-validated damage.
- Ammunition tracking.
- Reloading.
- Appropriate firing rate and weapon feedback.
- Clear hit, kill, and ammunition feedback.
- Configurable weapon statistics.

Future weapons may include different damage profiles, firing rates, magazine sizes, reload times, and purchase costs.

Weapon behavior should be data-driven wherever practical so that adding another weapon does not require rewriting the combat system.

---

## 7. Doors, Barricades, and Map Progression

The map should gradually open as players spend points and interact with the environment.

Potential systems include:

- Purchasable doors.
- Blocked passages.
- Barricades and repair interactions.
- Power switches.
- Weapon purchase locations.
- Other map-specific progression features.

### Rules

- Each interactable must have a clear state and defined cost, if applicable.
- The server validates interactions and purchases.
- A door must not charge multiple times for one purchase.
- Map progression must remain consistent for all players.
- Physical map objects should not independently implement competing gameplay logic.
- Map-specific costs and behavior should be configurable.

---

## 8. Multiplayer

The game should support cooperative play.

Multiplayer considerations include:

- Server-authoritative gameplay.
- Consistent rounds and zombie states for all players.
- Reliable point tracking and purchases.
- Correct handling of players joining or leaving.
- Appropriate spawning and respawning behavior.
- Stable zombie targeting when multiple players are present.
- Clear game-over and victory conditions, if implemented.

The initial player-count target is **TBD**.

Multiplayer testing is required before considering core gameplay complete.

---

## 9. User Interface and Audio

### Initial UI Priorities

- Current round.
- Player points.
- Weapon and ammunition information.
- Remaining zombies or round status.
- Interaction and purchase prompts.
- Player health or damage feedback, if included.
- Game-over and restart screens.

### Audio Priorities

- Weapon firing and reloading.
- Zombie movement and attacks.
- Zombie death sounds.
- Round transitions.
- Purchases and interactions.
- Ambient environmental sounds.
- Music and tension-building audio where appropriate.

Use original, licensed, or otherwise authorized assets. Any sounds, music, textures, models, and other assets must be appropriate for use in the project.

---

## 10. Technical Architecture

The codebase should be modular and easy to maintain.

**The actual Roblox Studio hierarchy is authoritative.** Any architecture document must distinguish between systems that currently exist and systems that are only planned.

Proposed system responsibilities:

- **RoundService:** Round state, progression, and spawn budgets.
- **ZombieService:** Zombie spawning, lifecycle, and AI coordination.
- **CombatService:** Server-side combat validation and damage.
- **PointsService:** Point rewards, balances, and spending.
- **InteractionService:** Validation and handling of player interactions.
- **MapStateService:** Shared state for doors, power, and map progression.
- **Weapon configuration:** Data-driven weapon statistics.
- **Zombie configuration:** Data-driven zombie statistics.
- **Round configuration:** Round difficulty and spawn settings.

These are proposed names, not a claim that these scripts already exist.

### Architecture Rules

- Avoid putting the entire game into one large script.
- Keep shared configuration separate from gameplay logic.
- Use clear, documented interfaces between systems.
- Validate important actions on the server.
- Avoid duplicate systems with overlapping responsibilities.
- Do not rename, delete, or replace existing systems without approval.
- Update `ARCHITECTURE.md` when approved architectural changes are made.

---

## 11. Visual Direction

The visual style should be grounded in the selected reference map.

Priorities:

1. Accurate map layout and silhouettes.
2. Recognizable landmarks and environmental structures.
3. Appropriate lighting, shadows, and atmosphere.
4. Consistent materials and environmental detail.
5. Performance appropriate for Roblox multiplayer.

Avoid adding decorative features that noticeably conflict with the reference map.

Use original or properly authorized assets rather than assuming that assets from Call of Duty can be redistributed.

---

## 12. Development Priorities

### Phase 1 — Reference and Planning
- [ ] Select the first map.
- [ ] Collect reference materials.
- [ ] Document the layout and important landmarks.
- [ ] Establish naming conventions and coordinate standards.

### Phase 2 — Map Blockout
- [ ] Build the main layout.
- [ ] Connect all major rooms and corridors.
- [ ] Verify proportions and elevation changes.
- [ ] Test player navigation.
- [ ] Test zombie navigation.
- [ ] Review the blockout before detailing.

### Phase 3 — Map Construction
- [ ] Build major structures and landmarks.
- [ ] Add environmental details and materials.
- [ ] Establish lighting and atmosphere.
- [ ] Add gameplay markers and interactable locations.
- [ ] Test performance and navigation again.

### Phase 4 — First Playable Gameplay Loop
- [ ] Implement one weapon.
- [ ] Implement one basic zombie type.
- [ ] Implement combat and zombie elimination.
- [ ] Implement points.
- [ ] Implement round progression.
- [ ] Implement the basic UI.
- [ ] Complete a full playtest from the first round through game over.

### Phase 5 — Map Progression
- [ ] Add purchasable doors.
- [ ] Add required map interactions.
- [ ] Add barricades or power systems where appropriate.
- [ ] Test progression in multiplayer.

### Phase 6 — Polish and Expansion
- [ ] Improve animations, sound, and feedback.
- [ ] Balance weapons, points, and rounds.
- [ ] Fix performance and pathfinding issues.
- [ ] Add more weapons or enemy types only after the core loop is stable.
- [ ] Consider additional maps after the first map meets the team's quality goals.

---

## 13. Out of Scope for the Initial Version

Unless explicitly approved, do not prioritize:

- Multiple complete maps.
- Large weapon collections.
- Complex boss fights.
- Elaborate Easter eggs.
- Extensive progression or prestige systems.
- Unnecessary monetization features.
- Major rewrites while core systems are being developed.

The first goal is one polished map and one complete, repeatable Zombies gameplay loop.

---

## 14. Team and AI Collaboration Rules

This project is developed collaboratively using Roblox Studio Team Create and multiple AI assistants.

All developers and AI assistants must follow `AI_RULES.md`.

### Rules

- Read the relevant project documentation before making changes.
- Inspect the existing Studio hierarchy and scripts when access is available.
- Do not assume that another AI has access to prior conversations.
- Work only within the assigned task's scope.
- Do not overwrite another developer's work.
- Avoid editing the same script or map section concurrently.
- Do not make unrelated changes or broad rewrites.
- Preserve approved map geometry, coordinates, and interfaces.
- Report exactly what changed and what was tested.
- Document architectural changes and important decisions.
- Never claim a test passed unless it was actually performed.

### Source of Truth

1. Current Roblox Studio project and approved shared assets.
2. This Game Bible for game vision and scope.
3. `ARCHITECTURE.md` for approved technical responsibilities and interfaces.
4. `TASK_BOARD.md` for task ownership and progress.
5. `CHANGELOG.md` for recorded changes.
6. `AI_RULES.md` for collaboration requirements.

If these sources conflict, stop and identify the conflict instead of guessing.

---

## 15. Decisions To Finalize

- [ ] Official game title.
- [ ] First map to recreate.
- [ ] Target player count.
- [ ] Target visual fidelity versus Roblox performance.
- [ ] Initial weapon.
- [ ] Initial zombie statistics.
- [ ] Round difficulty and spawn scaling.
- [ ] Point rewards and purchase prices.
- [ ] Required map progression features.
- [ ] Initial UI and audio scope.
- [ ] Asset sourcing and licensing approach.

**Final principle:** Build the map and the fundamentals correctly before expanding the game. Every feature should support the goal of delivering an authentic, polished, cooperative Zombies experience on Roblox.
