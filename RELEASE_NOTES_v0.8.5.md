# PokePCFollowers 0.8.5

Party submenu label fix, on top of the 0.8.4 fainted-lead spawn fix.

## Follower labels now fit the submenu box

The party submenu window is sized for the stock Gen 1 entries and clips at
eight characters. The nine-character label used for the active follower ran
past the right border and lost its final glyph.

- The Pokémon currently following now reads `FOLLOWER` (8 characters).
- Every other party member reads `FOLLOW?` (7 characters).

Only the displayed strings changed. Selection behavior, the saved follower
slot, the confirmation text box and the shared Gen 1 / Gen 2 submenu hook are
untouched, as is the fallback event listener used by older mod APIs.

## Also in this build (from 0.8.4)

- The follower no longer disappears when the party lead is fainted. The
  sandbox spawn-gate shim now borrows the selected follower's own party slot
  rather than slot 1, so the engine's native `species == PIKACHU and hp > 0`
  test is satisfied by a single healthy mon. A fully fainted party still
  spawns no follower.

## Preserved behavior

- Red, Blue, Yellow and Gold follower support.
- All 251 follower assets and Pokédex-proportional sizing.
- Crystal 251 integration.
- Unique Menu Icons and Dramatic Shape-family compatibility.
