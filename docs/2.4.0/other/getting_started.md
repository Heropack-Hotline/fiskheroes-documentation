+++
title = 'Getting Started'
linkTitle = 'Getting Started'
description = 'Coding seems hard but that is very much a myth, heropacking is an amazing way to learn how and many heropackers have gone on to study in game development fields.'
weight = 0
draft = false
+++

Coding seems hard but that is very much a myth, heropacking is an amazing way to learn how and many heropackers have gone on to study in game development fields.

### There was an idea

All you need to get started is an idea and a skin. You can make your own skin using resources in the textures section of Heropack Hotline to help or ask someone for permission to use theirs. Your suit doesn't even need to be a superhero. Plenty of various characters have been made by the community, from LEGO Ninjago to Five Nights at Freddy's. Once you have an idea of who you want to make I recommend using the Heropack Hotline's heropack template feature by joining the community [Discord](https://discord.gg/MA7DuKm) and running `/heropack-template` in any channel.

### heropack.json file

All heropacks start in the same place... the `heropack,json` If you use the discord bot's template generator you can have one made for you otherwise you can look in the [base mod's](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) `heropack.json` file to see how to make one. This file essentially sets up your heropack and will be where you will define sounds, alts, and damage types. For now the important things to include are the name, description, and domain. Your description and name can be just about anything, but the domain needs to be simple, lowercase, and unique to your pack, it can also not contain any special symbols.

### Data files

Next up are data files, every suit needs one and they define how the suit functions. In your heropack you need a folder named the same as your chosen domain defined in your `heropack.json` and in that folder you need a data folder. In the `data` folder you need a `power` folder and a `heroes` folder. In your `heroes` folder you need to make a `.js` file named after the hero you want to make (Ex. `spider_man.js`). This is where you name the hero, set its tier, define its powers, and control its abilities. Looking at [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) data files can help you with what to put in here as well as looking in the data section of Heropack Hotline. Power files aren't necessary for a suit but if you want to customize the hero's powers more than the base mod's abilities can offer you will want to make one of these. You can define modifiers here and customize their values.

### Renderer files

Renderer files control how a suit and its abilities look. This is where you will define textures, and renderer effects and properties. Looking at [base mod](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) renderer files can help you with what to put in here as well as looking in the renderer section of Heropack Hotline.

### Textures

Arguably the most important part of the suit you can find out how to give your suit its textures by looking in the texture section of Heropack Hotline.