+++
title = 'Keybind Menus'
linkTitle = 'Keybind Menus'
description = 'Written by Candy'
weight = 0
draft = false
+++

Suits in FiskHeroes allow for 5 keybinds for abilities, but what if you need more than 5? Keybind menus allow you to make as many keybinds as you need by nesting them under other keybinds.

### Open/close menu

To make a simple open/close menu you need to make a boolean variable for your menu in your `heropack.json`. Then you can either make it so you have a button for opening and a button for closing, or one button that does both. You can see both in examples below, you can also make the close button only appear when the menu is open and vice versa using `isKeybindEnabled` `/hotline keybind enabled`. This works with function keys `/hotline keybind funcs` to create custom keybinds that execute code to set the boolean variable, then you just use that variable to do whatever you want based on the condition.

```js
function init(hero) {
    hero.addKeyBindFunc("func_MENU_OPEN", menuOpenKey, "Open Menu", 3);
    hero.addKeyBindFunc("func_MENU_CLOSE", menuCloseKey, "Close Menu", 4);
    hero.addKeyBindFunc("func_MENU_TOGGLE", menuToggleKey, "Toggle Menu", 5);
}

function menuOpenKey(player, manager) {
	manager.setData(player, entity.getData("domain:dyn/menu"), true);
    return true;
}

function menuCloseKey(player, manager) {
	manager.setData(player, entity.getData("domain:dyn/menu"), false);
    return true;
}

function menuToggleKey(player, manager) {
    if (entity.getData("domain:dyn/menu")) {
        manager.setData(player, entity.getData("domain:dyn/menu"), false);
    } else {
	    manager.setData(player, entity.getData("domain:dyn/menu"), true);
    }
    return true;
}

function isKeyBindEnabled(entity, keyBind) {
    switch (keyBind) {
		case "SHIELD":
			return (entity.getData('domain:dyn/menu'));
        default:
            return true;
    }
}
```

### Cycle menu

Cycle menus are a bit more complicated, they are used to cycle through multiple options instead of opening one specific menu. You can either have one keybind to cycle but if you have a lot of options then you may want to add a key to cycle backwards as well. Sometimes we make this reverse key only available when sneaking to reduce the number of overall keybinds and simplify the user experience. Below you can see an example of a cycle menu with both buttons. We made it as simple to modify as possible, in `MAX_KEY` you set how many options there are to cycle through. In `DATA` you need to put a `heropack.json` variable, we tend to use a byte data type as you shouldn't need more than 64 options and it saves space and reduces load times. These keybind functions will cycle through the options and once it reaches your set maximum it will reset back to the first option. You can then do whatever you need with the variable by detecting which option it is on like shown in the `isKeybindEnabled` below.

```js
var MAX_KEY = 7;
var DATA = "domain:dyn/menu_cycle";
function init(hero) {
    hero.addKeyBindFunc("func_MENU_NEXT", nextCycleKey, "Next Menu", 4);
    hero.addKeyBindFunc("func_MENU_PREV", prevCycleKey, "Prev. Menu", 5);
}

function nextCycleKey(player, manager) {
	var key = player.getData(DATA);
	manager.setData(player, DATA, (key + 1) % MAX_KEY);
	return true;
}

function prevCycleKey(player, manager) {
	var key = player.getData(DATA);
	if (key == 0)
		manager.setData(player, DATA, (MAX_KEY - 1));
	else
		manager.setData(player, DATA, (key - 1));
	return true;
}

function isKeyBindEnabled(entity, keyBind) {
    switch (keyBind) {
		case "SHIELD":
			return (entity.getData('domain:dyn/menu_cycle') == 2);
        default:
            return true;
    }
}
```