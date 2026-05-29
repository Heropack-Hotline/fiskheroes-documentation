+++
title = 'Keybind Enabled'
linkTitle = 'Keybind Enabled'
description = 'The `isKeyBindEnabled` function allows you to make certain abilities that require keybinds conditional.'
weight = 0
draft = false
+++

The `isKeyBindEnabled` function allows you to make certain abilities that require keybinds conditional.

### Using keybind enabled

```js
function init(hero) {
    hero.setKeyBindEnabled(isKeyBindEnabled);
}

function isKeyBindEnabled(entity, keyBind) {
    switch (keyBind) {
    case "ENERGY_PROJECTION":
        return !entity.getData("fiskheroes:gravity_manip");
    case "GRAVITY_MANIPULATION":
        return !entity.getData("fiskheroes:energy_projection");
    case "AIM":
        return !entity.getData("fiskheroes:energy_projection");
    default:
        return true;
    }
}
```

To use keybind enabled first define the function in the `init` function like shown above. Then you can create the `isKeyBindEnabled` function with `entity, keyBind` as parameters. Inside this function you can use any sort of if-else statement here to return the condition you want based on the modifier. Above a [switch statement](https://www.w3schools.com/js/js_switch.asp) is used but you can also use a [ternary operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator) or a standard if-else statement to define the conditions. Whatever you choose to use you need to test for the keybind's id and return whatever condition you want. You can see what conditions you can use by looking at the [mapping viewer](https://github.com/FiskFille/FiskHeroes-Mapping-Viewer/releases). Now any keybind you defined will only show up if they meet the condition you set.