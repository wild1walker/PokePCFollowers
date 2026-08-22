# PokePCFollowers 0.8.4

Bug-fix release for the Gen1Recomp 0.1.86+ sandbox path.

## Fainted lead no longer suppresses the follower

On Red and Blue under the 0.1.86+ sandbox, no follower appeared whenever the
Pokémon in party slot 1 was at 0 HP — even when a different, healthy Pokémon
was explicitly selected through the party menu `FOLLOWER` action.

The sandbox has no `debug` library, so PokePC cannot replace the engine's
private `shouldSpawn` upvalue. Instead it briefly satisfies the native
Yellow/Pikachu spawn gate for the duration of each native call. That gate ends
with a party scan requiring one mon that is both named `PIKACHU` **and** above
0 HP. The shim spoofed the species of slot 1 but left its HP untouched, so a
fainted lead failed the HP half of the test; the scan then continued to the
remaining slots, none of which carried the spoofed species, and returned false.

The shim now borrows the selected follower's own party slot — obtained through
the version-neutral `starterInParty` wrapper — falling back to the first
healthy slot and finally to slot 1. Both halves of the native test are now
satisfied by the same mon, and no HP value is ever mutated.

A fully fainted party still spawns no follower: PokePC's own spawn predicate
requires a healthy follower before the shim is ever engaged.

## Preserved behavior

- Red, Blue, Yellow and Gold follower support.
- All 251 follower assets and Pokédex-proportional sizing.
- Crystal 251 integration.
- Follower selection, restoration and supported voxel rendering.
- Unique Menu Icons and Dramatic Shape-family compatibility.
