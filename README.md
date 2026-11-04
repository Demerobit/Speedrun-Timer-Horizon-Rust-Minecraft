# Speedrun Timer Horizon : Rust Minecraft

An RTA speedrun timer native mod for [Horizon](https://playhorizon.dev/) — Minecraft: Java
Edition 26.3 rewritten in Rust. Shows `HH:MM:SS.mmm` in a corner of the screen with unlimited
hours and live milliseconds.

- **Starts** on your first movement after a world loads (armed at zero while you stand still).
- **Stops** when you take the exit portal back to the Overworld after the End. Dying is not a
  finish: the death screen suspends the reading and the run keeps counting.
- **Auto-reset**: leaving a world for about a second rearms the timer at zero for the next one.
- **Corner** is changeable (Options > Mods > Speedrun Timer > Settings), F3/F1 respected.
- **Saves** every finished run to `horizon-mods/.horizon-mod-data/speedrun_timer/runs.csv`
  (+ `last_run.txt`, personal best); the settings page has a button that opens that folder.
- Commands: `/speedrun`, `/speedrun start`, `/speedrun stop`, `/speedrun reset`.

## Install (players)

Put `dist/speedrun_timer-1.0.0.hnmod` in the game folder's `horizon-mods/`, turn it on in
Options > Mods, then in Settings > Native mods (experimental) press **Build** and confirm the
native-code warning. Play the **Native mods** instance.

## Build from source

    git clone https://github.com/Demerobit/Speedrun-Timer-Horizon-Rust-Minecraft.git
    cd Speedrun-Timer-Horizon-Rust-Minecraft
    cargo test
    git clone https://github.com/horizon-rust/horizon-mods
    python3 horizon-mods/native/tools/native.py check /path/to/this/repo
    python3 horizon-mods/native/tools/native.py package /path/to/this/repo

Needs Rust stable; for the game check also Python 3.11+, `rsync`, and on Linux
`libasound2-dev`, `libudev-dev`, `pkg-config`. Loader: horizon-mixins bundle on Horizon's
native hook points (game 26.3, hooks 1).

## License

MIT
