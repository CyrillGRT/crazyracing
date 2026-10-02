# crazyracing

A lightweight Godot 4 project scaffold for a future casual 3D kart racer. This repository currently contains no gameplay.

## Open source

crazyracing is an open-source game project. Its code and project documentation are released under the [MIT License](LICENSE). Any future third-party art, audio, fonts, or other content may have separate license and attribution terms; check those notices before reuse.

## Requirements

- Godot 4.7 or newer in the Godot 4 series
- Git
- GitHub Spec Kit CLI (`specify`) for spec-driven planning

## Open and run

Open this directory in Godot, then press **F6** to run the main scene or **F5** to run the project. From a terminal:

```sh
godot --path .
```

If your executable is named `godot4`, substitute that command. Running the project currently opens an empty 3D scene.

## Project layout

- `project.godot` — project and renderer settings
- `scenes/main.tscn` — empty launch scene
- `.specify/` and `.agents/skills/` — GitHub Spec Kit setup for Codex

## Rendering and platforms

The project uses Godot's Compatibility renderer (OpenGL on desktop and WebGL 2 for web exports). This gives the initial project one conservative rendering path for browsers and older mobile devices. It limits access to some advanced rendering features compared with Forward+, which is a deliberate starting trade-off for the stated targets; revisit it if later art or effects require those features.

Web, Android, and iOS are intended targets. Exporting requires the matching Godot export templates and platform toolchains. Android exports need the Android SDK/JDK; iOS export requires macOS with Xcode. No export presets, signing credentials, or platform SDKs are included in this repository.

## Spec Kit

Spec Kit's Codex skills are installed under `.agents/skills/`. Start with `$speckit-constitution` to establish project principles, then use `$speckit-specify`, `$speckit-plan`, and `$speckit-tasks` for future work.
