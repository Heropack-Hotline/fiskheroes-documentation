+++
title = 'Keybind Funcs'
linkTitle = 'Keybind Funcs'
description = 'Written by Candy'
weight = 0
draft = false
+++

Keybind Functions allow you to run code that runs code once depending on the conditions of your choosing.

### Creating a keybind func

Within your suit's data files, ensure that you are within the init function. Similar to like other keybinds, you'll want to include the following: ```js\nhero.addKeyBindFunc(\"func_ABILITY_NAME\", functionName, \"Name of Ability\", #);```

### Important Info

For the keybind field, 1-5 is the list of the 5 main keybinds of the mod from top to bottom. You can also use -1 which is equal to the attack/destroy key, or LMB by default.

### Uses for Keybind Funcs

Using Ant-Man from the base mod as an example. Ant-Man's Giant Mode is controlled by a keybind function. Depending on if the ability is toggled or not, it will toggle to the inverse and sets the size state to -1 or 1 using a ternary operator around if giant mode is activated.

```js
function giantModeKey(player, manager) {
    var flag = player.getData("fiskheroes:dyn/giant_mode");
    manager.setData(player, "fiskheroes:dyn/giant_mode", !flag);
    manager.setData(player, "fiskheroes:size_state", flag ? -1 : 1);
    return true;
}
```

The keybind function will always alter the product to the inverse of itself, making the ability toggeable on and off. But it is only toggled based on if the keybind is pressed, it is not a constant check like a tick handler. So keep that in mind when deciding on implementation.