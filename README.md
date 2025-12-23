## What does this do?

This system enables datapacks to add up to 20 custom items which are entirely unobtainable in Survival, so that they may be used freely in crafting recipes.

## Why would I need this?

Completely custom items are, currently, out of reach for datapacks. The best option available is building off of existing items using [item components](https://minecraft.wiki/w/Data_component_format), whereby we can make an existing item look and behave as something entirely different. See [here](https://datapack.wiki/guide/adding-new-features/custom-items/intro) for a tutorial.

However, there's one system that gets in our way: crafting. Crafting recipes, while also customizable, cannot currently *read* item components (only write them). Thus, a custom item is conflated with its vanilla base in any crafting recipe which uses the base. Smartly-chosen base items, ones which do not craft into anything and whose other functionalities can be disabled via item components, ensure a custom item cannot ever be accidentally used in place of its base, but the reverse cannot be prevented so easily.

This system does just that: enables custom items which can *themselves* be crafted into other items (custom or vanilla), with no possibility of conflation with vanilla items and no alteration of any vanilla Survival gameplay.

## How do I use this?

Add the contents of `data/` to your pack. If your pack alters any of the vanilla loot tables which produce music discs, you may need to use a tool like [Weld](https://weld.smithed.dev/). Note that this is **not** a standalone pack, as it's not very big and rather likely to require some merging of vanilla files.

To add a custom item, assign it to one of the [20 Music Discs](https://minecraft.wiki/w/Music_Disc) (besides `music_disc_5`, which serves as the one remaining obtainable disc), with the `jukebox_playable` component disabled.

## How does this work?

## What are its limitations?
