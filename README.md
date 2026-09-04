# EasWorldChangeGuard

Small Paper plugin that mitigates an EasyArmorStands 3.3.0 session-boundary item leak on mixed creative/survival servers.

## What it fixes

EasyArmorStands can keep an active editing session when a player moves between worlds or changes game mode. On servers where players have EasyArmorStands access in both creative and survival worlds, this can allow a creative-world armor stand equipment edit to remain usable after the player returns to survival.

This plugin closes the player's EasyArmorStands session and open inventory after:

- `PlayerChangedWorldEvent`
- `PlayerGameModeChangeEvent`
- `PlayerTeleportEvent` when the destination world is different

## Target server

- Paper 26.2
- Paper API 1.21.11
- EasyArmorStands 3.3.0
- Java 25

## Install

1. Keep the official `EasyArmorStands-3.3.0.jar` installed.
2. Put `EasWorldChangeGuard-1.0.0.jar` into `plugins/`.
3. Restart the server.
4. Confirm both plugins are enabled with `/plugins`.

## Build

The build uses EasyArmorStands 3.3.0 as a compile-only dependency. Put the official jar here before building:

```text
libs/EasyArmorStands-3.3.0.jar
```

Then run:

```bash
./gradlew clean build
```

The output jar will be in:

```text
build/libs/EasWorldChangeGuard-1.0.0.jar
```

## Verification scenario

1. Start editing an armor stand with EasyArmorStands in a creative world.
2. Move through a portal into a survival world.
3. The EasyArmorStands inventory/session should close during the transition.
4. The creative-world armor stand item should not be removable from survival context.
