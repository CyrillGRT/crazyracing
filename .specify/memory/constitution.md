# crazyracing Constitution

## Core Principles

### I. Open Source by Default
Game source code and project documentation MUST remain publicly available under the MIT
License. Contributions MUST include only material the contributor has the right to share.
Third-party assets and code MUST retain their own license and attribution requirements; the
project license MUST NOT be assumed to override those terms. This keeps the game inspectable,
reusable, and safe to distribute.

### II. Lightweight by Design
New systems and dependencies MUST have a clear project need. Prefer Godot and GDScript built-in
features; adding a third-party dependency or service requires explicit project-owner approval.
Avoid complexity that does not provide a measurable benefit to the player or development workflow.

### III. Web and Mobile Are First-Class
Project structure, input, rendering, and platform-facing features MUST account for browser,
Android, and iOS builds. A feature is not considered complete solely because it works on desktop;
platform-specific behavior and export requirements MUST be documented and checked when applicable.

### IV. Performance Is a Product Requirement
Design and implementation MUST keep low-end laptops and older mobile hardware in scope. Prefer
scalable, inexpensive rendering and runtime approaches. More costly techniques MUST be justified
by a demonstrated quality need and measured on target hardware before adoption.

### V. No Gameplay Without a Feature Specification
Gameplay systems MUST be introduced through a reviewed Spec Kit feature specification and plan.
Until then, the project scaffold MUST remain free of kart, track, camera, physics, multiplayer,
and game UI implementation. This keeps early architectural assumptions visible and reviewable.

## Platform and Technology Constraints

The project uses Godot 4 and GDScript. Web browser, Android, and iOS are target platforms, with
low-end PCs and older mobile devices included in the performance baseline. The current project
uses Godot's Compatibility renderer as a portable starting point; a renderer change requires a
documented platform and performance comparison. No paid dependency, hosted service, plugin, or
multiplayer backend may be introduced without project-owner approval.

## Development Workflow

Use GitHub Spec Kit to capture requirements before implementation. Keep changes small and
reviewable, document platform limitations, and verify affected Godot scenes and scripts in the
engine. Do not claim a platform build is verified unless it has actually been exported and run
on that platform. Contributors MUST follow the repository's license and preserve relevant
third-party notices.

## Governance

This constitution governs project specifications and implementation plans. Amendments MUST be
recorded in this file and MUST update the version and amendment date. Versioning follows semantic
rules: MAJOR for incompatible governance changes, MINOR for new or materially expanded
principles, and PATCH for clarifications that do not change policy. Feature plans and code
reviews MUST be checked against these principles; exceptions MUST state their reason, scope, and
duration for review by the project owner.

**Version**: 1.0.0 | **Ratified**: 2026-10-02 | **Last Amended**: 2026-10-02
