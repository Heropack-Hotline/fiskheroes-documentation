+++
title = 'Augments'
linkTitle = 'Augments'
description = 'Augments are used at the Suit Augmentor to upgrade suits to have stronger attributes.'
weight = 0
draft = false
+++

Augments are used at the Suit Augmentor to upgrade suits to have stronger attributes.

### Adding augments to a suit

Either go to or create the folder chain `../assets/domain/data/augments/` in your heropack and create a `.json` file with the same name as your suits data file. Here you can add attributes to be augmented.

```json
{
    "attributes": {
      "DAMAGE_REDUCTION": [0, 4],
      "PUNCH_DAMAGE": [1, 3],
      "WEAPON_DAMAGE": [2, 4],
      "JUMP_HEIGHT": [0, 3],
      "FALL_RESISTANCE": [0, 4],
      "SPRINT_SPEED": [1, 3]
    }
  }
```

here you have an attribute followed by its minimum (default value) and the maximum that it can be upgraded to you cant set anything higher than 5 or lower than 0 for these values. You can have up to 6 attributes to be augmented on a single suit, they can be of any attribute in the mod. Which include... `ARROW_DAMAGE, BASE_SPEED, BASE_SPEED_LEVELS, BOW_DRAWBACK, DAMAGE_REDUCTION, FALL_RESISTANCE, FISKTAG_ARMOR, FISKTAG_HEALTH, IMPACT_DAMAGE, JUMP_HEIGHT, KNOCKBACK, MAX_HEALTH, PUNCH_DAMAGE, REACH_DISTANCE, SPRINT_SPEED, STEP_HEIGHT, WEAPON_DAMAGE`. You probably will not be using either of the fisktag related attributes. As always look at the [base mod's](https://github.com/Heropack-Hotline/heropack-hotline-storage/blob/main/Fiskheroes%202.4.0%20Extracted.zip) suits for a general idea of what values these should be set at to keep them balanced. A lot of people forget to add augments to suits but its important for survival compatibility so try to keep track of what suits you've given augments and which you've yet to do so for.