+++
title = 'Giving Your Suit a Texture'
linkTitle = 'Giving Your Suit a Texture'
description = 'Getting started with the Plume theme.'
weight = 0
draft = false
+++

Arguably the most important part of making a suit is giving it a skin.

### Recommended Tools

* [Blockbench](https://www.blockbench.net/downloads)
* [PMCSkin3D](https://www.planetminecraft.com/skin-editor/)
* [Paint.NET](https://getpaint.net)
* [Coolors](https://coolors.co)

I also recommend looking through Blockbench's plugins if you decide to use that for skinning.

### Skinning Tips

* [Minecraft Style Guide](https://www.blockbench.net/wiki/guides/minecraft-style-guide/)

When making your skin remember ambient occlusion. Ambient occlusion is a the lighting conditions should naturally occur when indirect or ambient lighting is cast out (99% of the time the light source comes from above your head, keep that in mind when skinning). Places like under the head or chest will be darker as they are more obscured by light compared to places like the top of the head or shoulders. Another way to know if you should make certain places lighter or darker is based on depth.

The closer something should be to you the lighter it should be, this helps make flat planes appear to have more shape. Don't forget to account for the material you are skinning and how light interacts with it. And remember to take anatomy into account, using an anatomy reference image like a drawing or even a photo can help. A lot of people forget about the anatomy of a human and just shade the cubes, the cubes are supposed to be something other than just cubes. If you want to try to stick to the style of the mod you can try studying the base mods skins for inspiration, another thing you can do is apply a minor blur to certain colors or noise to the skin (I usually use 10 or less noise).

### Item Textures

You can make your item textures using templates found in the base mods texture files `/hotline homepage` and using other item textures as reference. To give your texture the outline, put the template on a layer above your texture and set it to multiply. Then you can adjust as needed. You can put all your textures in `...\\textures\\items\\heroes` and name them `suit_name_0.png` for the helmet, `suit_name_1.png` for the chestplate and so on.

### Layering

Layering your skin can be pretty tricky depending on the skin. The simplest and luckily most common way is to separate the head, chestplate, and boots onto layer 1, and the leggings on to layer 2. Usually the leggings go farther down than how the appear when the full suit is worn, so its smart to make your skin with this in mind. The leggings also often contain the bottom few pixels of texture on the body. If you have a more complicated skin you may need more layers. As always looking at the base mods files `/hotline homepage` can help you with this. Often boots or jackets will need to be separated as the jacket may extend to the legs or even cover the boots. You can place all these files in your `...\\textures\\heroes` folder and even put them in a subfolder to help organize them.

### loadTextures

Now moving on to the renderer file you to need to call the textures and give them simpler names to be able to apply them to your suit.

```js
loadTextures({
    "layer1": "fiskheroes:batman_dceu_layer1",
    "layer2": "fiskheroes:batman_dceu_layer2",
    "cape": "fiskheroes:batman_dceu_cape"
});
```

the first part is the shorter name and you can name it anything, after that is the domain and the texture file, if you used a subfolder you would do `\"domain:subfolder/texture\"` instead. If you have even more subfolders you would just do the same thing  `\"domain:subfolder/subfolder/texture\"`

### init(renderer)

still in the renderer this is where you actually set the textures.

```js
function init(renderer) {
    renderer.setTexture((entity, renderLayer) => renderLayer == "LEGGINGS" ? "layer2" : "layer1");

    renderer.setItemIcons("%s_0", "%s_1", "%s_2", "%s_3");
    renderer.showModel("HELMET", "head", "headwear");
    renderer.showModel("CHESTPLATE", "body", "rightArm", "leftArm");
    renderer.showModel("LEGGINGS", "body", "rightLeg", "leftLeg");
    renderer.showModel("BOOTS", "rightLeg", "leftLeg");
    renderer.fixHatLayer("HELMET");

    initEffects(renderer);
    initAnimations(renderer);
}
```

Most of these you wont need to worry about as most suits have the same structure and thus are default. Starting with `.setTexture` this is the main part of setting your skin, in this case `renderLayer == \"LEGGINGS\" ?` is a condition and `\"layer2\"` is what it calls if that condition is true, with `\"layer1\"` being what's called if its false, with `:` separating them. You can also do this with if statements. For example...

```js
renderer.setTexture((entity, renderLayer) => {
    if (renderLayer == "LEGGINGS") {
        return entity.getWornChestplate().suitType() == $SUIT_NAME ? "pants_trenchcoat" : "layer2";
    }
    else if (renderLayer == "BOOTS") {
        return entity.getWornChestplate().suitType() == $SUIT_NAME ? "boots_trenchcoat" : "boots";
    }
    return "layer1";
});
```

It can be a bit of a logic puzzle but using these if statements in combination with the separated textures you made earlier you can make sure the correct textures show up when you have a specific suit part equipped. ```js\nrenderer.setItemIcons(\"%s_0\", \"%s_1\", \"%s_2\", \"%s_3\");``` `.setItemIcons` is used to set the item textures for the suit `%s` just means its going to use whatever the suits name is then the number which corrolates to a specific suit part, with 0 being the helmet, 1 being the chestplate, and so on. If you wanted a different suits texture show up or have multiple suits with the same boots or somthing you could just write the suit name instead of the `%s`. ```js\nrenderer.showModel(\"HELMET\", \"head\", \"headwear\");``` `.showModel` is pretty straight foward and is just for letting the game know what armor pieces modify what parts of the player. So if you had a trenchcoat that has the texture extend down to the legs, you would add both legs to the `.showModel`. ```js\ninitEffects(renderer);\n    initAnimations(renderer);``` `initEffects` and `initAnimations` are just setting up functions for later, you probably wont need to do this as long as you have `hero_basic` as the suit's parent. 

### Troubleshooting

If you are having issues with your suit texture make sure to make sure your syntax `/hotline troubleshooting` is correct. If your suit is black and purple it means your texture doesn't exist, you may want to double check your names or check the log.

### Resources

* [Minecraft assets](https://mcasset.cloud)