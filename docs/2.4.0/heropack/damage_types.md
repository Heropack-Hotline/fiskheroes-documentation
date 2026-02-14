+++
title = 'Damage Types'
linkTitle = 'Damage Types'
description = 'Written by Candy'
weight = 0
draft = false
+++

Through your `heropack.json` you can add custom damage types to make certain heroes deal more or less damage to others.

### Default damage types

There are already several damage types you have access to from the base mod, they include... `ATLANTEAN_STEEL, BLUNT, BULLET, CACTUS, COLD, COSMIC, ELECTRICIITY, ENERGY, ETERNIUM, EXPLOSION, FIRE, MAGIC, SHARP, SHURIKEN, SOUND, and THORNS` In order to use these check the base mods `heropack.json` `/hotline homepage` and make sure to use the correct formatting in your data or power file. You can use damage types in damage profles `/hotline damage profiles`.

### Creating your own damage types

Creating damage types is very easy, in your heropack.json look for or create a section named \"damageTypes\": and add a new entry with the all capital name using underscores in place of spaces and with the value of what you want the name to look like in-game. It's important to keep the name of the entry simple as that can allow for compatibility between different packs. If my pack has a damage type named LIGHT and your pack has a damage type named LIGHT they both will work together and suits that I have that deal that damage will affect suits you have that are weak to that damage. But if you name your damage type LIGHT_SOURCE_DAMAGE instead, it will have no compatibility. This is also important to consider in case your damage type may be taken out of context, for instance having a damage type named BLACK for making a suit weak to attacks by a black lantern is way too vague and can have the unintended consequence of making other packs strong against your suit when they really shouldn't be if they use the same name for a completely different reason.

```json
{
  "damageTypes": {
    "ENTRY_NAME": "Entry Value",
    "LIGHT": "Light"
  }
}
```