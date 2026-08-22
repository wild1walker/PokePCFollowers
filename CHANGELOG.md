# Changelog

## 0.8.5 - 2026-08-22

### Changed
- Shorten the party submenu follower labels so they fit the submenu box. The
  active follower now reads `FOLLOWER` (8 characters) instead of the
  9-character label that had its final glyph clipped by the window border, and
  every other party member reads `FOLLOW?` (7 characters).

## 0.8.4 - 2026-08-22

### Fixed
- Follower no longer disappears entirely when the party lead is fainted. The
  sandbox spawn-gate shim spoofed the species of party slot 1 but not its HP,
  so the engine's native `shouldSpawn` test (species == PIKACHU *and* hp > 0)
  failed on a 0 HP lead and no other slot carried the spoofed species. The
  shim now borrows the selected follower's own slot, falling back to any
  healthy slot, so both halves of the native test are satisfied by the same
  mon. A fully fainted party still correctly spawns no follower.

## 0.8.2 - 2026-08-14

### Changed
- Target Gen1Recomp 0.1.86+ and its per-mod sandbox.
- Route the legacy implementation through a sandbox-safe bootstrap using `mod.assets:path` and `mod:read`.
- Replace the Gen 1 debug-upvalue follower-spawn fallback with a narrow runtime compatibility seam.
- Keep cross-mod integration on public `mod.find(...).exports` surfaces.

### Preserved
- Red, Blue, Yellow and Gold follower support.
- All 251 follower sprites, Pokédex sizing, Crystal 251 integration and voxel compatibility.
- Unique Menu Icons compatibility and saved follower selection.

## 0.8.1 - 2026-08-12

### Changed
- Let Unique Menu Icons own party-menu icons and color handling when both mods are enabled.
- Prevent PartyMenu wrappers from stacking during hot reloads.
