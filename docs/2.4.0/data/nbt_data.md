+++
title = 'NBT Data'
linkTitle = 'NBT Data'
description = 'Written by Candy'
weight = 0
draft = false
+++

Named Binary Tags or NBT data is a data format Minecraft uses to store information for entities, items, blocks, and more.

### Uses for NBT data

In fiskheroes NBT data can be used to store more permanent data on suits. If you want code to only be run once per suit you can set a boolean NBT value to true and unless you change it back to false it will never change unlike custom data variables. With NBT you can allow for unlocking of abilities or customization of your suit.

### Using NBT data

To access NBT data you first need to tell your suit what item to look for. Usually we assign NBT data to the chestplate unless the suit doesn't have one. Below you can see the `nbt` variable as defined as the NBT data of the currently worn chestplate. You may also notice that this code is in an if statement to make sure this code is run server side. NBT data can cause desync on the client if you don't run it server side. It can also end up effecting multiple suits instead of just one. Here we are using a boolean, you can see what other functions you can use by using the mapping viewer `/hotline homepage` and going to `JS Accesors` then `JSNBT` or `JSDataManager`. We created a boolean NBT tag named `\"used\"` and set it to true, this code will only be run once because once `\"used\"` is set to true it won't go back, and the byte `\"amount\"` will always be set to 3. Most of the time we set NBT data in either a tick handler `/hotline tick handlers` or a function key `/hotline keybind funcs`.

```js
hero.setTickHandler((entity, manager) => {
    if (PackLoader.getSide() === "SERVER" && player.is("PLAYER") && !player.is("DISPLAY")) {
        nbt = player.getWornChestplate().nbt();
        if (nbt.getBoolean("used") != true) {
            manager.setByte(nbt, "amount", 3);
            manager.setBoolean(nbt, "used", true);
        }
    }
});
```

You can view the NBT data on an item by using the [Forge NBTEdit In Game](https://www.curseforge.com/minecraft/mc-mods/forge-nbtedit-for-1-7-10) mod. Just put the items you need to view in a chest and then run `/nbtedit` while looking at it.