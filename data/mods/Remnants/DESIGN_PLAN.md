## Plan: Remnants (Narrative Mod)

Goal: define and build Remnants, a playable mod where the character always wakes up in a custom house and the story progresses through chapter-based events and decisions.

## Agreed Direction
- The run starts in a fixed, author-designed house with fixed props and items (for example books, notes, and narrative objects).
- After leaving the house, the world remains procedurally generated as in standard CDDA.
- The procedural world can include selected fixed story anchors (specific buildings, key points, and NPC placements).
- This hybrid structure is the core design strategy for Remnants.

Included scope:
- Mod structure and metadata.
- Controlled house start (scenario, location, and mapgen).
- Narrative progression based on events and state.
- Chapters, objectives, and branching paths.
- Testing and quality criteria for iteration.

Excluded for now:
- Official repository publication.
- Multi-language localization in version 1.
- Complex custom art or soundtrack assets.

### 1) Narrative Vision and Design
- Mod pitch in 3-5 lines.
- Theme and narrative tone.
- Player fantasy for the first 30 minutes.
- Chapter structure (chapter 1, 2, 3, and branching endings).
- Success and failure conditions.

Deliverables:
- Story synopsis.
- Chapter table with objective, trigger, and outcome.

### 2) Gameplay Experience Requirements
- Experience style: guided, semi-guided, or sandbox with narrative thread.
- Target run duration.
- Desired difficulty by chapter.
- Starting constraints (gear, wounds, resources, weather, time).
- Replayability rules (branch variations and optional randomization).

Deliverables:
- Gameplay rules document.
- Difficulty matrix by chapter.

### 3) Mod Architecture
- Mod folder and file scope.
- Metadata definition.
- Dependencies.
- ID and naming conventions.
- Domain organization (scenario, mapgen, overmap, narrative events, missions, dialogues, NPCs, utilities).

Deliverables:
- Target folder structure.
- Naming convention guide.

### 4) Fixed House Intro
- Create a dedicated intro scenario.
- Create a dedicated start location that points to the custom house.
- Build the custom house mapgen and immediate surroundings.
- Place fixed narrative objects (books, notes, key loot, flavor props).
- Add safety fallback behavior if spawn constraints fail.

Deliverables:
- Validated scenario and start location.
- Reproducible intro map.

### 5) Procedural World with Story Anchors
- Keep default procedural overmap generation after the intro house.
- Add limited fixed overmap specials for story progression.
- Define placement constraints (distance to city, rarity, uniqueness, biome rules).
- Ensure anchors do not break normal world generation flow.

Deliverables:
- List of fixed anchor locations.
- Placement rule table.

### 6) Narrative State System
- Global progression variables (chapter, flags, key decisions).
- Chapter transition events.
- Decision tracking for branching outcomes.
- Content gating by narrative state.
- Save/load consistency for all narrative state.

Deliverables:
- Narrative state variable list.
- Transition diagram.

### 7) Events, Dialogues, Objectives, and NPCs
- Opening event sequence and onboarding.
- Chapter-specific dialogues.
- Main and optional objectives.
- Fixed or conditional NPCs tied to chapter progress.
- Gameplay consequences of decisions (access, allies, threats, resources).
- Climax and ending triggers.

Deliverables:
- Chapter scripts.
- Objective and NPC trigger matrix.

### 8) Branching and Replayability
- A/B/C branch paths for key decisions.
- Irreversible states and points of no return.
- Route-specific encounter and reward variation.
- Dead-end prevention and recovery paths.

Deliverables:
- Branch map.
- Branch validation checklist.

### 9) Balance and Pacing
- Tune early scarcity and availability.
- Tune pressure and difficulty curve per chapter.
- Add pacing windows for exploration and recovery.
- Balance risk/reward for optional story objectives.

Deliverables:
- Balance table by chapter.
- Tuning changelog.

### 10) Testing Strategy
- Happy-path test from intro to ending.
- Branch-by-branch narrative tests.
- Regression tests after event/dialogue/NPC changes.
- Save/load tests at critical state transitions.
- Robustness tests for unusual player actions.

Deliverables:
- Manual QA checklist.
- Narrative bug report template.

### 11) Delivery Roadmap
- Milestone 1: vertical slice (fixed house intro + full chapter 1).
- Milestone 2: chapter 2 and first major branch.
- Milestone 3: chapter 3 and endings.
- Milestone 4: polish, balance, and QA.

Deliverables:
- Milestone schedule and exit criteria.

### 12) Acceptance Criteria
- The character always starts in the intended custom house.
- The world outside remains procedural.
- At least one fixed story anchor location spawns correctly.
- At least one narrative NPC appears through defined rules.
- Main route is completable without blockers.
- Save/load preserves narrative state correctly.

### 13) Collaboration and Open Questions
- Open narrative design questions.
- Pending architecture decisions.
- Technical risks and mitigations.
- Design changelog.

## Internal Repository References
- Modding base: doc/MODDING.md
- In-repo mod policy: doc/IN_REPO_MODS.md
- Existing mod examples: data/mods/

## Implementation Checklist (Fixed House Intro v0.1)

### Added in current prototype
- Dedicated start location for Remnants scenario.
- Scenario hook that runs intro EOC at game start.
- Intro house mapgen update that replaces the initial house tile with a fixed layout.
- Fixed tutorial supplies and books placed in specific coordinates.
- Intro tutorial popup messages for new players.

### Files used for this phase
- `start_locations.json`: dedicated scenario start location (`sloc_remnants_house`).
- `scenarios.json`: scenario points to dedicated start location and intro EOC.
- `mapgen_intro_house.json`: fixed house layout and object placement.
- `eoc_intro_tutorial.json`: onboarding/tutorial logic at scenario start.

### Next tasks for v0.2
- Split the house into stronger authored spaces (bedroom, bathroom, kitchen, study, storage, exit hall).
- Add chapter-aware tutorial steps (inside-house tasks and an "exit house" completion check).
- Add one starter mission so tutorial state is visible in the mission log.
- Add fallback logic if mapgen update cannot apply on edge cases.

### Acceptance checks for this phase
- Starting Remnants always uses `sloc_remnants_house`.
- Intro EOC executes on new game start.
- Initial house is transformed into fixed layout.
- Fixed books and tutorial items spawn consistently.
- Player receives onboarding guidance immediately.
