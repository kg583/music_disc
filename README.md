## What does this do?

`music_disc` enables datapacks to add up to 20 custom items which are entirely unobtainable in Survival, so that they may be used freely in crafting recipes.

## Why would I need this?

Completely custom items are, currently, out of reach for datapacks. The best option available is building off of existing items using [item components](https://minecraft.wiki/w/Data_component_format), whereby we can make an existing item look and behave as something entirely different. See [here](https://datapack.wiki/guide/adding-new-features/custom-items/intro) for a tutorial.

However, there's one system that gets in our way: crafting. Crafting recipes, while also customizable, cannot currently *read* item components (only write them). Thus, a custom item is conflated with its vanilla base in any crafting recipe which uses the base. Smartly-chosen base items, ones which do not craft into anything and whose other functionalities can be disabled via item components, ensure a custom item cannot ever be accidentally used in place of its base, but the reverse cannot be prevented so easily.

Custom crafting systems are the standard remedy, but this may not be right for your datapack, perhaps due to a smaller custom item collection or a desire to be more interwoven with vanilla. `music_disc` thus offers an alternative: custom items which can *themselves* be crafted into other items (custom or vanilla), with no possibility of conflation with vanilla items and no alteration of any vanilla Survival gameplay.

## How do I use this?

Add the contents of `data/` to your pack. To add a custom item, assign it to one of the [20 Music Discs](https://minecraft.wiki/w/Music_Disc) (besides `music_disc_5`, which serves as the one remaining obtainable disc). Provide your custom item to the player by providing the corresponding music disc, with the `jukebox_playable` component disabled and visual components (i.e. `item_name`, `item_model`) set to the item's resources.

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

Note that this is **not** a standalone pack, as it's not very big and rather likely to require some merging of vanilla files.

## How does this work?

To freely craft with custom items in vanilla Survival, we would need to use as bases items which are entirely unobtainable. There are actually quite a lot of these, but all of them have some critical shortcoming.

- **Technical blocks** (e.g. commands blocks): Since these are *blocks*, they can be placed. While various properties of the block can be altered using item components, the mere ability to place them (in Survival, at least; see [`can_place_on`](https://minecraft.wiki/w/Data_component_format#can_place_on)) cannot be turned off.
- **Spawn eggs**: Spawn eggs have two uses which item components cannot disable: spawning things (duh) and altering mob spawners.
- **Knowledge book**: Similar to spawn eggs, its bestowment of knowledge, even if made explicitly empty, cannot be disabled.
- **Debug stick**: You can alter which properties the stick sets for any block (see [`debug_stick_state`](https://minecraft.wiki/w/Data_component_format#debug_stick_state)), but it remains a debug stick all the same.

This leaves us instead in need of items which, while perhaps obtainable in vanilla Survival, can be "hidden" without disrupting gameplay. Our need is met by music discs, whose musical contents (and interaction with comparators in a jukebox!) are entirely controlled by the [`jukebox_playable`](https://minecraft.wiki/w/Data_component_format#jukebox_playable) component.

All vanilla sources of music discs are made to produce copies of `music_disc_5`; this was chosen as the one true disc™ since it's the only disc involved in vanilla crafting via disc fragments. Each copy's [`item_name`](https://minecraft.wiki/w/Data_component_format#item_name), [`item_model`](https://minecraft.wiki/w/Data_component_format#item_model), and [`rarity`](https://minecraft.wiki/w/Data_component_format#rarity) components are set to match the intended disc. In doing so, these copies are made indistinguishable by any Survival means from the real thing.

Thus, every disc besides `music_disc_5` becomes unobtainable in Survival, freeing them for use as truly unique custom item bases.

## What are its limitations?
