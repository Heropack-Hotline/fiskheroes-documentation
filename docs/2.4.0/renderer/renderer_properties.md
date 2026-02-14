+++
title = 'Renderer Properties'
linkTitle = 'Renderer Properties'
description = 'Written by Candy'
weight = 0
draft = false
+++

Renderer properties can really differentiate suits of similar abilities by giving those abilities unique appearances.

### Using renderer properties

Unlike renderer effects which are something you are creating, renderer properties configure how something should render. You can find everything you can configure with renderer properties and what you can configure in the mapping viewer `/hotline homepage`. These are most often used to change what beams and trails look like. Renderer properties go into your renderer file in the `initEffects` function, they do not need to be rendered in the `render` function.

```js
var utils = implement("fiskheroes:external/utils");

function initEffects(renderer) {
    // Forcefield
    var forcefield = renderer.bindProperty("fiskheroes:forcefield");
    forcefield.color.set(0xFFD3A8);
    forcefield.setShape(36, 18).setOffset(0.0, 6.0, 0.0).setScale(1.25);
    forcefield.setCondition(entity => {
        forcefield.opacity = entity.getInterpolatedData("fiskheroes:shield_blocking_timer") * 0.15;
        return true;
    });

    // Shadowform Cloud
    utils.bindCloud(renderer, "fiskheroes:particle_cloud", "fiskheroes:shadow_smoke").setCondition(entity => entity.getData("fiskheroes:shadowform"));

    // Antimatter Beam
    utils.bindBeam(renderer, "fiskheroes:energy_projection", "fiskheroes:energy_projection", "body", 0xFF1000, [
        { "firstPerson": [0.0, 6.0, 0.0], "offset": [0.0, 5.0, -4.0], "size": [4.0, 4.0] }
    ]).setParticles(renderer.createResource("PARTICLE_EMITTER", "fiskheroes:impact_energy_projection"));
}
```

Most if not all properties are made easy to configure with the help of the utils external the base mod provides. Above are many examples of properties being used in a suit. The forcefield shows how you would go about configuring a property without the help of the utils file and the rest use the file. You can see each function the utils file contains by looking at the basemod `/hotline homepage` and going to `\\assets\\fiskheroes\\renderers\\heroes\\external\\utils.js` and you can see what fields they take.