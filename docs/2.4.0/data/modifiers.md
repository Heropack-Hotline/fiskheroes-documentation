+++
title = 'Modifiers'
linkTitle = 'Modifiers'
description = 'Written by Candy'
weight = 0
draft = false
+++

Modifiers or powers are what give your suit most of its abilities. You can use them as intended or get more creative with them.

### Using modifiers

To get started you want to create a new `.json` file In your power folder name whatever you want your power to be; make sure its in all lowercase with no special characters, you can use underscores in place of spaces. Below is an example of a power file from the base mod. You can see the name value and then the modifier section with `fiskheroes:healing_factor` and `fiskheroes:potion_immunity` listed under it. These are modifiers they are abilities that are from the mod and you cannot create you own, you can only use what the mod gives you to create your suits. However, you can get extremely creative in how you use these modifiers. Under the modifier is more properties to define how the modifier should act when in game as well as the sounds that they play when used. You can see a full list of every modifier and all the properties they support by looking at the mapping viewer's modifier section `/hotline homepage` You can also see what values the properties support by looking at the power properties section. Looking at base mod powers can also be a great way to see how these properties are applied. Many modifiers also support damage profiles `/hotline damage profiles`.

```json
{
    "name": "Healing Factor",
    "modifiers": {
      "fiskheroes:healing_factor": {
        "delay": 80,
        "soundEvents": {
          "HEAL": "fiskheroes:healing_factor"
        }
      },
      "fiskheroes:potion_immunity": {
        "potionEffects": ["minecraft:poison", "minecraft:wither"]
      }
    }
  }  
```

### Bar notation

You can have multiple of each modifier with different properties by giving the modifier a modifier id. To give a modifier an id you need distinguish it with a  `|` symbol followed by a unique identifier like shown below. You can set when each ability is used using the `ifModifierEnabled` function in your suit's data file `/hotline modifier enabled`.

```json
{
    "name": "Spider Physiology",
    "modifiers": {
      "fiskheroes:leaping": {
        "leapAmount": [1.0, 0.25]
      },
      "fiskheroes:leaping|springboard": {
        "leapAmount": [2.0, 0.75],
        "soundEvents": {
          "LEAP": ["fiskheroes:web_swinging_whoosh", "fiskheroes:web_swinging_fall_loop"]
        }
      }
    }
  }
```