+++
title = 'Renderer Inheritance'
linkTitle = 'Renderer Inheritance'
description = 'Written by Candy'
weight = 0
draft = false
+++

Inheriting renderer files can cut down on repeat code and optimize your pack.

### Why inherit renderers?

Like stated above renderer inheritance can reduce repeat code, it also makes it easier to add similar suits and change all those suits at once instead of individually. Say you have three Iron Man suits and all of them look exactly the same except for their texture. You could copy and paste the renderer and have the same code repeated three times, but then not only does it increase the file size of the pack but if you decide to change something you need to change it in all three files. Alternatively you could have two of them extend the parent and only define the textures in the child files. This way when you change something in the parent it is changed in the children.

### Using renderer inheritance

Inheritance is most commonly used for alts but can be used for any renderer.

```js
extend("fiskheroes:captain_america");
loadTextures({
    "layer1": "fiskheroes:captain_america_stealth_layer1",
    "layer2": "fiskheroes:captain_america_stealth_layer2",
    "shield": "fiskheroes:captain_america_stealth_shield"
});

var utils = implement("fiskheroes:external/utils");

function initEffects(renderer) {
    parent.initEffects(renderer);
    utils.addLivery(renderer, "SHIELD", "shield");
}
```

Here you can see an alt renderer for Captain America. Since this alt has a different shield texture the `initEffects` function is overwritten but it calls the parent's `initEffects` using `parent.initEffects(renderer);`. You cannot parent a function that does not exist in the parent. For example, say you want to have the alt file shown above as a parent for another alt. You cannot parent the `init` function since it is not defined in the parent even though its defined in the parent of the parent. To fix this you would define the `init` function and just add `parent.init(renderer);` so it parents it's own parent. Any functions you don't define in the child file will just default to whatever it's parent uses, same with textures. However, variables do not get inherited. You can also inherit a renderer that isn't used as a suit. Killer Frost is a good example of this as she and her alts inherit `fiskheroes:killer_frost_base`.