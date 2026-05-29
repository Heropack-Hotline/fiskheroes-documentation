+++
title = 'Alts'
linkTitle = 'Alts'
description = 'Alts are alternate versions of suits that you can access via the Suit Iterator, they have the same powers and functions as the suit they are an iteration of.'
weight = 0
draft = false
+++

Alts are alternate versions of suits that you can access via the Suit Iterator, they have the same powers and functions as the suit they are an iteration of.

### Adding alts to a suit

Alts are added through the `heropack.json` in a field called `\"alts\":`

```json
{
"alts": {
    "fiskheroes:falcon": {
      "civil_war": "Civil War"
    },
    "fiskheroes:august_heart_comics": {
      "$DEFAULT": {
        "name": "Future Godspeed",
        "maskToggleTicks": 15,
        "soundProfile": "COMICS"
      }
    },
    "fiskheroes:captain_america": {
      "aou": "Age of Ultron",
      "canada": {
        "name": "Captain Canada",
        "vanity": "achievement.fiskheroes.language"
      },
      "nomad": {
        "name": "Nomad",
        "armor": {
          "HELMET": "Beard"
        }
      }
    }
  }
}
```

In this example `fiskheroes:falcon` is being given an alt based on his appearance in civil war. The first part under the suit is what the alt's identifier will be, you will need to make a new renderer file for each alt to render its new appearance, name the alt's renderer the same as the base suit with the identifier at the end separated by an underscore Ex. `falcon_civil_war`. The second part is what the name of the alt will be in game. The `fiskheroes:august_heart_comics` suit is being given `$DEFAULT` properties. There aren't any new alts being added to this suit and instead it is modifying the default suit, you can give a default suit a alt style identifier when hovering over it's item by using the `\"name\":` field. You can change the speed in ticks at which mask toggle is used using `\"maskToggleTicks\":` and you can customize the sound profile the suit uses using `\"soundProfile\":`. `fiskheroes:captain_america` has a lot going on here. He has some normal alts but also some special ones. Vanity alts are alts that can only be obtained after the user has completed the corresponding achievement attached to them, If someone attempts to wear a vanity alt they have not unlocked it will appear to be the default suit. Cap also has an `\"armor\":` field so you can rename the armor items of an alt if they happen to wear different types of clothing. Here it's used to rename Cap's helmet into a beard. You can rename any and all parts of the suit here.