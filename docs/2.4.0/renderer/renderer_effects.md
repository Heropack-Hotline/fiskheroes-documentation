+++
title = 'Renderer Effects'
linkTitle = 'Renderer Effects'
description = 'Written by Candy'
weight = 0
draft = false
+++

Using renderer effects can add a lot of extra detail to your suits and can range from boosters to custom models.

### Using renderer effects

You can find all the renderer effects and what functions they support from the mapping viewer `/hotline homepage`. Some common ones are `fiskheroes:chest` for female suits breasts, `fiskheroes:capes` for capes, scarfs, and sometimes hair, and `fiskheroes:model` for custom models from tabula. Renderer effects go into your renderer file and are created in the `initEffects` function.

```js
var utils = implement("fiskheroes:external/utils");
var afro;

function initEffects(renderer) {
    parent.initEffects(renderer);
    afro = renderer.createEffect("fiskheroes:model");
    afro.setModel(utils.createModel(renderer, "fiskheroes:deadpool_bob_ross_afro", "afro"));
    afro.setOffset(0, 0, -1);
    afro.anchor.set("head");
}

function render(entity, renderLayer, isFirstPersonArm) {
    parent.render(entity, renderLayer, isFirstPersonArm);

    if (!isFirstPersonArm && renderLayer == "HELMET") {
        afro.render();
    }
}
```

To use a renderer effect you need to first create it with a variable, for this model effect of an afro a variable named `afro` was made and then was defined in the `initEffects` function. After its definition you can use any functions on the effect that its compatible with, like `.setOffset()`. To display your effect you need to go into the `render` function and call `.render()` on the effect. You can also dynamically adjust values like offset, size, texture, and other functions in the `render` function but always call `.render()` last or your changes might not apply correctly.