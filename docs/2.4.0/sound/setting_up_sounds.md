+++
title = 'Setting up Sounds'
linkTitle = 'Setting up Sounds'
description = 'Written by Candy'
weight = 0
draft = false
+++

Custom sounds can add a lot to a suit and be what makes an ability satisfying to use.

### Setting up your repository and sound files

Make a new **public** [GitHub repository](https://github.com/new). Create a sounds directory/folder on your desktop named `sounds`. Within this folder, there should be another `sounds` folder as well as a `sounds.json` file. In this second `sounds` folder put any of your sound files. They must be `.ogg` and can be organized further into whatever folders you want. Go back and open the `sounds.json` file. For every sound you have you will want to have something like this:

```json
{
    "sound.name": {
      "sounds": [
        "folder_path/sound_file"
      ],
      "category": "player"
    }
}
```

Compress the inner `sounds` folder and `sounds.json` into a zip file called `0.zip`. The number is the version number and you can make it whatever you want, if you have a file named `1.zip` and a file named `2.zip` then you can have two different versions of your heropack or even two different heropacks with different sounds depending on what sound version you put in the `heropack.json` Upload the first `sounds` folder with the `0.zip` inside it to your GitHub repository.

### Adding sounds to your pack

Going into your `heropack.json` add a sounds portion under `\"packFormat\" : 1,`

```json
{
"packFormat": 1,
   "sounds": {
    "download": {
      "repository": "Put your GitHub username followed by your repository seperated by a forward slash here, Ex: Joespeph/Sounds",
      "version": 0
    },
    "range": {
      "sound_name": { "distance": 32.0, "sendToAll": true }
    }
  }
}
```

Now in your assets\\domain folder create a new folder named `events` in this folder create another named `sounds`, then in this folder create a .JSON file for each sound file you have. Ex: `sound_name.json`. Inside this .JSON you will define the sound further. Its recommended you look at the base mods events folder for more information. Now the last thing to do is to add the sound to the suit, there are two ways to do this the first is in the data file and the second is in the power file. Use the base mod to figure out which you are supposed to do but most of the time its the power file. If you are doing it in the data file, under ` function init(hero) {` put something like `hero.addSoundEvent(\"SOUND_EVENT\", \"domain:sound_name\");` For the power file under each power should be a `\"soundEvents\"` section, its as simple as changing the name of the sound here.

```json
{
"soundEvents": {
    "ENABLE": "domain:sound_name"
  }
}
```

### Resources

* [List of sound events](https://docs.google.com/document/d/1VZaH6tF9KBfW9Ucizv_evalHi8zxgnQ-9eevxtaenRs/edit?usp=sharing)
* [Video game sound library](https://www.sounds-resource.com/)
* [Video Tutorial by Robin_Cosmic](https://www.youtube.com/watch?v=hXOkPwrCn_g)