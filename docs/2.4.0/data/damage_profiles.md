+++
title = 'Damage Profiles'
linkTitle = 'Damage Profiles'
description = 'Damage profiles are used for configuring the damage some abilities and attacks do and how.'
weight = 0
draft = false
+++

Damage profiles are used for configuring the damage some abilities and attacks do and how.

### Damage profile fields

Damage profiles can be used in either the power file or the data file. They are split up into three parts... damage amount, damage type, and damage properties. Damage amount takes a double of how much damage you want to attack to do to an entity. Damage type takes a custom damage type and a double of how much each type contributes to the total damage given. For instance below you can see `COSMIC` set to `1.0` this means that someone with 100% cosmic damage immunity will take no damage from the attack. If you instead set `COSMIC` to `0.5` they would take 50% of the damage. If you have two or more damage types defined here they all contribute to an overall total. Having `COSMIC` set to `0.5` and `SHARP` set to `1.0` would deal 75% of the damage to someone with 50% cosmic damage immunity. Finally for damage properties you can see what properties are supported in the [mapping viewer](https://github.com/FiskFille/FiskHeroes-Mapping-Viewer/releases) under damage properties. For the power file all you need to do is define everything you need under the `damageProfile` field.

```json
{
    "fiskheroes:energy_projection": {
      "damageProfile": {
        "damage": 3.0,
        "types": {
          "COSMIC": 1.0
        },
        "properties": {
          "REDUCE_KNOCKBACK": 1,
          "EFFECTS": [
            {
              "id": "minecraft:blindness",
              "duration": 15,
              "amplifier": 2,
              "chance": 1.0
            },
            {
              "id": "minecraft:slowness",
              "duration": 15,
              "amplifier": 5,
              "chance": 1.0
            }
          ]
        }
      },
      "range": 10.0,
      "radius": 0.1,
      "soundEvents": {
        "BEAM_AMBIENT": "fiskheroes:antimatter_beam"
      }
    }
  }
```

### Power file

To define a damage profile in a power file all you need to do is configuring everything under the `damageProfile` field as shown above. You can see what modifiers support damage profiles in the [mapping viewer](https://github.com/FiskFille/FiskHeroes-Mapping-Viewer/releases) under modifiers.

```js
function init(hero) {
    hero.addAttributeProfile("CLAWS", clawsProfile);
    hero.setAttributeProfile(getProfile);
    hero.setDamageProfile(getProfile);
    hero.addDamageProfile("CLAWS", {"types": {"SHARP": 1.0}});
}

function clawsProfile(profile) {
    profile.inheritDefaults();
    profile.addAttribute("PUNCH_DAMAGE", 10.5, 0);
}

function getProfile(entity) {
    return entity.getData("fiskheroes:blade") ? "CLAWS" : null;
}
```
### Data file

To define a damage profile in a data file use `hero.addDamageProfile(PROFILE)` inside the `init` function with your profile within the parenthesis just like you would do in the power file. Then you need to create the function to set the profile just like you would with an attribute profile. With `hero.setDamageProfile(FUNCTION);` you can set any function name you want, you can even use the same function for damage profiles as attribute profiles like shown above. Whatever you name your function you need to create it now if it doesn't already exist. Inside the function you can use any sort of if-else statement here to return the profile you need based on the condition you want. Like a [switch statement](https://www.w3schools.com/js/js_switch.asp), [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) or a standard if-else statement to define the conditions.