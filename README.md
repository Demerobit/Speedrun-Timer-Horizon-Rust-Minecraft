# Speedrun Timer (Horizon native mod)

An RTA timer for [Horizon](https://playhorizon.dev/) ("Minecraft Rust Edition"), compiled
into the game as a native mod. Shows `HH:MM:SS.mmm` in a corner of the screen —
unlimited hours, live milliseconds.

- **Starts** on your first movement after a world loads (armed at zero while you stand still).
- **Stops** when you take the exit portal back to the Overworld after the End.
- **Dying is not a finish**: the death screen suspends the reading; the run keeps counting.
- **Auto-reset**: leaving a world for about a second rearms the timer at zero for the next one.
- **Corner** is changeable (Options > Mods > Speedrun Timer > Settings), with F3/F1 respected.
- **Saves** every finished run to `horizon-mods/.horizon-mod-data/speedrun_timer/runs.csv`
  (+ `last_run.txt`, personal best), and the settings page has a button that opens that folder.
- Commands: `/speedrun`, `/speedrun start`, `/speedrun stop`, `/speedrun reset`.

## Install (players)

Put `dist/speedrun_timer-1.0.0.hnmod` in the game folder's `horizon-mods/` (or install it
from the launcher's Mods page), turn it on in Options > Mods, then in
Settings > Native mods (experimental) press **Build** and confirm the native-code warning.
Play the **Native mods** instance.

## Build from source

    git clone https://github.com/<your-username>/speedrun-timer
    cd speedrun-timer
    cargo test                                     # the timer logic, on no game
    git clone https://github.com/horizon-rust/horizon-mods
    python3 horizon-mods/native/tools/native.py check /path/to/speedrun-timer
    python3 horizon-mods/native/tools/native.py package /path/to/speedrun-timer

Needs Rust (stable) and, to check against the game, Python 3.11+, `rsync`,
`libasound2-dev`, `libudev-dev` and `pkg-config` on Linux. The bundle pins Horizon
`6f8c7a0e5d531d3834c4d0be4659a1db8e7e5c2a` (Nightly 2026-10-28) and uses hook points
API 1 only, so the launcher builds it on any Horizon that has them.

## Structure

- `mixins/speedrun_timer/horizon-mixin.toml` — the bundle manifest (id, hooks, injections)
- `mixins/speedrun_timer/runtime.rs` — the timer logic and its unit tests
- `frame.rs`, `hud.rs`, `command.rs`, `list.rs`, `settings.rs`, `click.rs` — one helper per hook point
- `compatibility.json` — game, hook-points API and the revisions it was tested on

## License

MIT
