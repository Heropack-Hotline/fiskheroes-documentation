+++
title = 'Fabricator Recipes'
linkTitle = 'Fabricator Recipes'
description = 'Written by Candy'
weight = 0
draft = false
+++

To make your suits survival friendly they need to have recipes so players can obtain them.

### Creating recipes

Either go to or create the folder chain `../assets/domain/data/fabricator/recipes/` in your heropack and create a `.json` file with the same name as your suits data file. Here you can enter in the item you want and the amount of said item required to create the suit in the suit fabricator. You can use any item, but most use tutridium gems with a few suits using vibranium or gold titanium ingots.

```json
{
    "items": {
      "fiskheroes:tutridium_gem": 36
    }
  }
```

### What should your recipe be?

Figuring out what the cost of your suit should be can be tricky, try to think about how powerful your suit is and look at other similar suits recipes in the base mod `/hotline homepage` to get an idea on what to set your recipe to. You can also make it cost something extra if you want, for instance you could put a dragon egg as a material required, this would mean only one of these suits can exist on a server.