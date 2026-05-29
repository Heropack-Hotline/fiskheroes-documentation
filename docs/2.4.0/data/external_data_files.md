+++
title = 'External Data Files'
linkTitle = 'External Data Files'
description = 'Externals within data files can be used to simplify code or provide universal code that can be used on multiple suits without changing every single instance or just using bloated code.'
weight = 0
draft = false
+++

Externals within data files can be used to simplify code or provide universal code that can be used on multiple suits without changing every single instance or just using bloated code.

### Creating external

Assuming you already know the directories setup, create a JS script within `data/heroes/externals`. For this tutorial I will be using Iron Man from the [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) as an example. Iron Man from the [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) uses the superhero landing tick handler external.

```js
function tick(entity, manager) {
    var t = entity.getData("fiskheroes:dyn/superhero_landing_ticks");

    if (t == 0 && !entity.isSprinting() && !entity.isOnGround() && entity.motionY() < -1.25 && entity.getData("fiskheroes:flight_boost_timer") > 0 && entity.world().blockAt(entity.pos().add(0, -2, 0)).isSolid()) {
        manager.setDataWithNotify(entity, "fiskheroes:dyn/superhero_landing_ticks", t = 12);
        entity.playSound("fiskheroes:suit.ironman.landing", 1, 1.15 - Math.random() * 0.3);
    }
    else if (t > 0) {
        manager.setData(entity, "fiskheroes:dyn/superhero_landing_ticks", --t);
    }

    manager.incrementData(entity, "fiskheroes:dyn/superhero_landing_timer", 2, 8, t > 0);
}
```

The name of the variable doesn't necesarily matter, but ensure that whatever the domain that you're using is based on `domain:external/file_name`\n\nNow all you have to do is implement the variable into the tick handler by taking the variable from above and calling the function. ```js\nvar landing = implement(\"fiskheroes:external/superhero_landing\");```

### External data files continued

While the previous page was just one example of using externals, there are other ways to use it, like using a function to set isModifierEnabled or isKeybindEnabled's default. Inside externals, the possibilities to create universal code can be used amongst numerous heroes can be extremely beneficial in the long run. Referencing `super_boost.js` from the [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip), you can see many instances of creating keybinds, or having predefined `isModifierEnabled` or `isKeyBindEnabled` functions that has all of your needs in one place. Inside your external file, creating your `isModifierEnabled` function to only allow the boosted modifier during a condition to create something like the following:

```js
function isModifierEnabled(entity, modifier) {
    if (modifier.name() == "fiskheroes:controlled_flight") {
        var boost = entity.getData("fiskheroes:dyn/flight_super_boost");
        return boost != 1 && (modifier.id() == "boosted") == (boost > 0);
    }
    return true;
}
```

Once you have implemented your external into your data file, `var super_boost = implement(\"fiskheroes:external/super_boost\");` all you have to do is call the variable name `super_boost` in the default's return like this:

```js
function isModifierEnabled(entity, modifier) {
    switch (modifier.name()) {
    case "fiskheroes:energy_projection":
        return entity.getHeldItem().isEmpty();
    case "fiskheroes:charged_beam":
        return !(entity.isSprinting() && entity.getData("fiskheroes:flying")) && entity.getHeldItem().isEmpty();
    default:
        return super_boost.isModifierEnabled(entity, modifier);
    }
}
```

Just like the isModifierEnabled function created in the external, functions like the tick handler or isKeybindEnabled can also be recreated to simplify the code in your data file. The referenced external `super_boost.js` is a great tool to use if you want to further your understanding.