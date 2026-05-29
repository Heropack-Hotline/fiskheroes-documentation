+++
title = 'Data Variables'
linkTitle = 'Data Variables'
description = 'Using data variables you can create custom timers and toggles for individual suits.'
weight = 0
draft = false
+++

Using data variables you can create custom timers and toggles for individual suits.

### Data var types

The data variable types you have access to are as follows... `BOOLEAN`, `BYTE`, `DOUBLE`, `DOUBLE_INTERP`, `FLOAT`, `FLOAT_INTERP`, `INTEGER`, `LONG`, `SHORT`, and `STRING`. `DOUBLE_INTERP` and `FLOAT_INTERP` are interpolated versions of their respective data types to be used for rendering.

### Using data vars

These data variables are defined in your `heropack.json` and should look something like this...

```json
{
    "dataVars": {
    "steeled": "BOOLEAN",
    "steel_timer": "FLOAT_INTERP",
    "steel_cooldown": "FLOAT",
    "nanites": "BOOLEAN",
    "nanite_timer": "FLOAT_INTERP",
    "nanite_cooldown": { "type": "FLOAT", "resetWithoutSuit": true, "resetOnDeath": true }
  }
}
```

The most common use which is shown twice here is for timers, but you can use them for anything you need to store temporary data for. In these examples `steeled` is our toggle data, its a Boolean that lets us know whether the timer is off or on. `steel_timer` is the timer that goes from 0 to 1 interpolated so any animation or texture operation used during the timer comes out smooth. Finally `steel_cooldown` is the cooldown which doesn't need to be interpolated as it is purely for gameplay and has nothing to do with visuals. You can also define more as shown in `nanite_cooldown`. `resetWithoutSuit` defaults to false when not defined and `resetOnDeath` defaults to true. You can change these if you want the data or cooldown to persist after the player has died so they cant just cheat their way into bypassing an extra long cooldown on an ability.

### Accessing data vars

You can access custom data variables just about anywhere. Similar to how you would access [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) variables like `\"fiskheroes:shield_timer\"` you access your custom variables by using `\"your_domain:dyn/your_variable\"` making sure you add `dyn/` before the actual name of your variable. Once accessed you can compare or even change the value by using `manager.setData` or `manager.incrementData`.