+++
title = 'Attribute Profiles'
linkTitle = 'Attribute Profiles'
description = 'Written by Candy'
weight = 0
draft = false
+++

Attribute profiles allow you to change the stats of a suit dynamically, allowing you to better balance your suit.

### Uses for attribute profiles

Attribute profiles can be used in many scenarios, most commonly for blades. They can change any attribute depending on a condition and you can have as many profiles as you need. You could make the player slower or faster when using a specific ability, you could make the player jump higher when holding a carrot, and so on and so forth.

### Using attribute profiles

Attribute profiles are defined in the data file formatted as `.addAttribute(KEY, VALUE, OPERATOR);`. The key field takes any attribute from the mod which are... `ARROW_DAMAGE, BASE_SPEED, BASE_SPEED_LEVELS, BOW_DRAWBACK, DAMAGE_REDUCTION, FALL_RESISTANCE, FISKTAG_ARMOR, FISKTAG_HEALTH, IMPACT_DAMAGE, JUMP_HEIGHT, KNOCKBACK, MAX_HEALTH, PUNCH_DAMAGE, REACH_DISTANCE, SPRINT_SPEED, STEP_HEIGHT, WEAPON_DAMAGE`. You probably will not be using either of the fisktag related attributes. The value field takes a double for the value of whatever attribute you chose and operator determines whether the value is read as a percent or not. If you set operator to `1` and the value to `0.5` then it reads as 50% if you set operator to `0` and value to `4.0` it reads as 4.0. As always look at the base mod's `/hotline homepage` suits for a general idea of what values these should be set at to keep them balanced.

### Default profile

The default attribute profile is defined in the `init` function and is defined with `hero` this is what your suit's attributes will be always unless something else overwrites it, like another attribute profile.

```js
{
    hero.addAttribute("PUNCH_DAMAGE", 4.0, 0);
    hero.addAttribute("WEAPON_DAMAGE", 1.0, 0);
    hero.addAttribute("FALL_RESISTANCE", 2.5, 0);

    hero.addKeyBind("BLADE", "key.blade", 1);

    hero.addAttributeProfile("BLADE", bladeProfile);
    hero.setAttributeProfile(getProfile);
    hero.setDamageProfile(getProfile);
    hero.addDamageProfile("BLADE", {"types": {"SHARP": 1.0}});
}

function bladeProfile(profile) {
    profile.inheritDefaults();
    profile.addAttribute("PUNCH_DAMAGE", 7.0, 0);
}

function getProfile(entity) {
    return entity.getData("fiskheroes:blade") ? "BLADE" : null;
}
```

### New profiles

To create a new attribute profile you need to define it in the `init` function as `hero.addAttributeProfile(STRING, FUNCTION);`. You can set the name of your profile, usually written in all caps in the string field surround by quotes like `\"BLADE\"`. For the function field you would write the function that you are going to use to assign your attributes, we usually write functions in camelCase, so like above if your profile name is `\"BLADE\"` you would write the function as `bladeProfile`. Then the last thing you do in the `init` function is define where you are going to set your profiles which is `hero.setAttributeProfile(getProfile);`. Moving to a new functions you need to create like shown above. Name it the same thing you put in the function field earlier and define your attributes the same way you would for default but with `profile` instead of `hero` here you can also use `profile.inheritDefaults()` to use any attributes from the default profile here unless overwritten, if you don't use this everything will be overwritten when the new profile is in use. You can also use `profile.revokeAugments()` to nullify augments when the profile is active. Finally create the `getProfile` functon and you have a few choices here. You can use any sort of if-else statement here to return the profile you need based on the condition you want. Above a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) is used but you can also use a [switch statement](https://www.w3schools.com/js/js_switch.asp) or a standard if-else statement.
