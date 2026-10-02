# Feature Specification: Arcade Kart Driving Prototype

**Created**: 2026-10-03
**Status**: Draft

## Goal

Give the player a directly launchable single-player 3D arcade driving prototype to evaluate the core kart handling on a simple oval course.

## Scope

- **Included**: Keyboard driving, third-person follow camera, forgiving acceleration/braking/steering/reverse, controllable drifting, placeholder oval course and collidable barriers.
- **Excluded**: Multiplayer, purchases or other monetization, opponents, progression, final art, third-party assets, controller and touch controls.

## User Stories and Acceptance Criteria

### US1 — Start and drive (P1)

As a player, I want to launch straight into a driving session and control the kart with a keyboard.

- **AC1.1**: The project opens directly to the kart on the oval course, without a menu.
- **AC1.2**: W/up accelerates; S/down slows forward motion and, when held after stopping, reverses; A/left and D/right steer; Space initiates a drift.
- **AC1.3**: The third-person camera keeps the kart and the upcoming course visible as the kart moves and turns.
- **AC1.4**: The scene launches on Web, Android, and iOS. Keyboard driving is required in a desktop browser; connected keyboards may be used on mobile. Other controls are out of scope.

### US2 — Handle turns and recover from slides (P1)

As a casual player, I want responsive steering and forgiving traction so I can drive through turns without fighting the controls.

- **AC2.1**: Steering changes the kart's direction predictably at ordinary driving speeds and does not cause an unexpected spin during a sustained turn.
- **AC2.2**: Steering with the drift action produces a controllable slide; releasing drift restores grip smoothly enough to continue around the course.
- **AC2.3**: Releasing driving controls stops acceleration and steering; the kart gradually loses speed.

### US3 — Drive the oval course (P1)

As a player, I want a clear continuous course with barriers so I can practice the handling and recover after collisions.

- **AC3.1**: Placeholder geometry makes the oval route, driving surface, kart direction, and barriers easy to distinguish.
- **AC3.2**: Barriers prevent the kart from passing through them and visibly affect its movement on contact.
- **AC3.3**: After contacting a barrier, the player can steer away and continue without restarting the scene.

## Constraints and Requirements

- **FR-001**: Driving actions MUST be distinct from their current keyboard bindings so controller or touch inputs can be added later without changing the actions. Those inputs are not part of this feature.

## Success Criteria

- **SC-001**: In a five-minute play session, a first-time keyboard player can complete three laps while retaining control of the kart.
- **SC-002**: On a documented low-end PC/browser profile and an iPhone 11-class reference device, at least 95% of one-second samples during a five-minute session reach 30 FPS or higher. The plan records the exact PC/browser test profile.

## Assumptions and Open Questions

- **Assumption**: This is free-drive practice with no lap counter, race timer, win/loss state, or race opponents.
- **Assumption**: The keyboard mapping in AC1.2 is the prototype default; controller and touch bindings are future work.
- **Assumption**: The project plan will select and document a representative low-end PC/browser profile before performance verification.
