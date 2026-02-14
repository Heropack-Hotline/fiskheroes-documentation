+++
title = 'Tick Handlers'
linkTitle = 'Tick Handlers'
description = 'Written by Candy'
weight = 0
draft = false
+++

Tick handlers allow you to run code that runs constantly depending on conditions of your choosing.

### Creating a tick handler

Within your suit's data files, ensure that you are within the init function. Once in that function, type out the following:

```js
hero.setTickHandler((entity, manager) => {
    
});
```

Within the brackets you now have access to create code that is runs every tick unless specified by code. You should try to keep your code inside an if statement to ensure its not always running. Otherwise it may impact performance. All code within the tick handler is run every tick (20 times per second).

### Uses for tick handlers

Using Doctor Strange from the base mod as an example. Doctor Strange uses a tick handler to keep him from dying to fall damage if the conditions are met (falling at a certain velocity).

```js
hero.setTickHandler((entity, manager) => {
    // Here is the if statement, we are checking if the player is not sneaking, is in the air and their motion velocity on the Y AXIS is less than -0.8
    if (!entity.isSneaking() && !entity.isOnGround() && entity.motionY() < -0.8) {
        manager.setData(entity, "fiskheroes:flying", true);
    }
});
```

The condition within the if statement ensures the code isn't run until it is met. Once the condition is met the code inside will run, saving the player from certain death. You can set any data to any value that is allowed within its variable type `/hotline variables`. You can find what variables there are using the mapping viewer `/hotline homepage`. You can also set NBT data `/hotline nbt data` or even print to chat.

```js
if (entity.is("PLAYER") && !entity.is("DISPLAY")) {
    entity.as("PLAYER").addChatMessage("Hello World!")
}
```