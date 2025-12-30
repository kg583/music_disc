## What does this do?

`music_disc` enables datapacks to add up to 20 custom items which are entirely unobtainable in Survival, so that they may be used freely in crafting recipes.

## Why would I need this?

Recipe files are currently unable to read [item components](https://minecraft.wiki/w/Data_component_format). This limits the ability to use the vanilla crafting system with [custom items](https://datapack.wiki/guide/adding-new-features/custom-items/intro), as they can always be conflated with their vanilla bases. Custom crafting systems are the standard remedy, but may not be the preferred choice for your datapack, perhaps due to a smaller item collection or a need to be more "interwoven" with vanilla gameplay.

 `music_disc` offers an alternative: custom items which can *themselves* be crafted into other items (custom or vanilla), with no possibility of conflation with vanilla items and no alteration of any vanilla Survival gameplay.

## How do I use this?

Add the contents of `data/` to your pack. To add a custom item, assign it to one of the [20 Music Discs](https://minecraft.wiki/w/Music_Disc) (except `music_disc_5`, which serves as the base for all other discs). Provide your custom item to the player by providing the corresponding music disc, with the `jukebox_playable` component disabled and visual components (i.e. `item_name`, `item_model`) set to the item's resources. You'll also likely need to tweak `max_stack_size`.

```mcfunction
/give @p minecraft:music_disc_13[!jukebox_playable,item_name="Your Item",item_model="your_pack:your_item"]
```

If your pack alters any of the vanilla loot tables which produce music discs, you may need to use a tool like [Weld](https://weld.smithed.dev/). If your pack adds any additional sources of music discs, use the `music_disc` loot tables to provide correctly modified copies.

```
{
  "type": "minecraft:item",
  "name": "minecraft:music_disc_cat"
}
// becomes
{
  "type": "minecraft:loot_table",
  "value": "music_disc:cat"
}
```

Note that this is **not** a standalone pack, as it's not very big and rather likely to require some merging of vanilla files. Vanilla files were pulled from version `1.21.11`, though should work without alteration as far back as `1.21`.

## How does this work?

All vanilla sources of music discs are made to produce copies of `music_disc_5`; this was chosen as the one true disc™ since it's the only disc involved in vanilla crafting via disc fragments. Each copy's [`jukebox_playable`](https://minecraft.wiki/w/Data_component_format#jukebox_playable), [`item_name`](https://minecraft.wiki/w/Data_component_format#item_name), [`item_model`](https://minecraft.wiki/w/Data_component_format#item_model), and [`rarity`](https://minecraft.wiki/w/Data_component_format#rarity) components are set to match the intended disc. In doing so, these copies are made indistinguishable by any Survival means from the real thing.

Thus, every disc besides `music_disc_5` becomes unobtainable in Survival, freeing them for use as truly unique custom item bases.

## What are its limitations?

Since we're hijacking vanilla items, there are only the twenty to go around for *all* datapacks. Two packs which use e.g. `music_disc_stal` for different things have no way to tell *each other* apart when crafting, so conflation remains a potential issue. The count of twenty can also only increase whenever Mojang adds a new music disc; I intend to update this repository whenever this happens.

Of course, the best outcome would be for completely custom items, or recipes which can read item components, to be added before I have to bother.
