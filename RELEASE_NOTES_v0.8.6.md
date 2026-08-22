# PokePCFollowers 0.8.6

Fainted Pokémon are no longer drawn as the overworld follower.

## The bug

The spawn gate and the renderer disagreed about which mon was following.

`shouldSpawn` resolved the follower with `needHealthy = true`, so a fainted
selection correctly fell through to the first healthy party member and a
follower was spawned. But `SpriteRenderer.resolveImage` and
`SpriteRenderer.draw` resolved it with `needHealthy = false`, which honours the
stored selection regardless of HP. The entity that spawned on behalf of a
healthy mon was therefore painted with the sprite of a 0 HP one, and a fainted
Pokémon walked behind the player.

Because a fainted mon cannot be picked in the first place — both the `FOLLOW?`
menu entry and `selectFollower` gate on HP — this only appeared when the
chosen follower fainted in battle after being selected.

## The fix

Every follower resolution on the render path is now healthy-only, matching
`shouldSpawn`: the two `SpriteRenderer` wrappers, the party-menu resync check
and the follower-size options handler.

While the chosen follower is fainted, the first healthy party member follows
instead. The stored selection is left untouched, so the original follower
resumes the moment it is revived — no need to reselect it from the party menu.

With no healthy Pokémon at all, no follower is drawn, which is already what
`shouldSpawn` reports.

A grep guard in the release workflow now fails the build if a render-path
lookup reintroduces `needHealthy = false`.

## Also in this build

- 0.8.5: party submenu labels shortened to `FOLLOWER` and `FOLLOW?` so they fit
  the menu box.
- 0.8.4: the follower no longer disappears entirely when the party lead is
  fainted.
