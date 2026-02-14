+++
title = 'Modifier Enabled'
linkTitle = 'Modifier Enabled'
description = 'Written by Candy'
weight = 0
draft = false
+++

Similar to keybind enabled, the `isModifierEnabled` function allows you to make modifiers conditional.

### Using modifier enabled

To use modifier enabled first define the function in the `init` function like shown below. Then you can create the `isModifierEnabled` function with `entity, modifier` as parameters. Inside this function you can use any sort of if-else statement here to return the condition you want based on the modifier. Below a [switch statement](https://www.w3schools.com/js/js_switch.asp) is used but you can also use a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) or a standard if-else statement to define the conditions. Whatever you choose to use you need to test for the modifier's name and return whatever condition you want. You can see what conditions you can use by looking at the mapping viewer `/hotline homepage`. The `modifier` parameter from the function can support multiple functions. The ones that matter the most are `name()` and `id()`. These are pretty self explanatory, you can see both in use below. You can see more functions that `modifier` supports in the mapping viewer at JS Accessors >  JSModifier. You can see how to set modifier ids at `/hotline modifiers`. Now any modifier you defined will only show be active if they meet the condition you set and contain the correct id if you defined one. So if you set flying as conditional, you won't be able to fly unless that condition is met.

```js
function init(hero) {
    hero.setModifierEnabled(isModifierEnabled);
}

function isModifierEnabled(entity, modifier) {
    switch (modifier.name()) {
    case "fiskheroes:web_swinging":
        return entity.getHeldItem().isEmpty() && entity.getData("fiskheroes:utility_belt_type") == -1;
    case "fiskheroes:leaping":
        return modifier.id() == "springboard" == (entity.getData("fiskheroes:ticks_since_swinging") < 5);
    default:
        return true;
    }
}
```