+++
title = 'Troubleshooting'
linkTitle = 'Troubleshooting'
description = 'You will run into a lot of problems as you learn how to heropack. Hopefully this page can help you solve them. If you were looking for something that isnt here make sure to use the feedback button.'
weight = 0
draft = false
+++

You will run into a lot of problems as you learn how to heropack. Hopefully this page can help you solve them. If you were looking for something that isnt here make sure to use the feedback button.

### Error types

There are three types of errors; syntax, runtime, and logic. syntax errors are the most common and you will run into them often, they happen when you forget to include a character or misspell something. This will be caught when you try to run the pack and will either cause your suit to be gold or not run the pack at all. Runtime errors are why we need to test suits before we release them, the game will let the pack run and load and won't have an issue until the specific line of code is ran. If something doesn't exist, or is unavailable when you try to access it, it may end up causing a runtime error and crash the game. Logic errors are the hardest to find as they don't cause the game to break or not run but instead just give you an unwanted result. This can be caused by doing math wrong or comparing variables incorrectly.

### Common issues

**Textures are black and purple**
Most likely the texture you are calling does not exist, check it for spelling errors or incorrect file paths. This can also happen if you turned shaders on in which case run `/fiskheroes reload --resources` inside of Minecraft."

**Suit is gold**
There is most likely something wrong with your renderer file, check it for syntax errors or check the log for `[Client thread/WARN]: Using fallback Hero model` to find out what went wrong. This could also be caused by a missing resource - like models, trails, animations, and so on.

**Pack failed to read**
This can only be caused by a problem with your data files, this includes the suit's data file but also power files, nodes, and the `heropack,json`. Use `/fiskheroes reload --debug` and check the log for `Reloading HeroPacks failed` to find out what is causing this.

**My pack is taking forever to reload**
Fiskheroes suffers from memory leaks every time you reload the pack, this is minor at first but every time you reload it takes longer and longer. Restart the game when this happens and it should fix the problem. If it doesn't, make sure your heropack.png is at the recommended size of 256x256.

### Accessing logs

You can find the log at `.minecraft/logs/latest.log` and use it to find information on what is going wrong with your pack. Newer information is at the bottom and show you why the game crashed, or is using fallback models. Look through it carefully as it's easy to miss information. Try using `Ctrl + F` to search for specific suits or keywords.

### Solving errors

If your pack is not functioning as intended and you can't figure out why from either the log or your code, you can try printing debugging messages to find the issue. Using `PackLoader.print()` you can print variables or messages by putting it inside the parenthesis and it will appear in your log. You can also send the same messages directly to your in-game chat using `PackLoader.printChat()` or `entity.as("PLAYER").addChatMessage()`. Keeping your code clean is important to be able to find errors or find code when you need it later. This means using proper indentation and separation between lines. Many IDEs will format code for you with a push of a button, but you can also use online beautifiers to help as you learn.

### Resources

* [JS Syntax](https://www.w3schools.com/js/js_syntax.asp)
* [JS Validator](https://codebeautify.org/jsvalidate)
* [JS Beautifier](https://codebeautify.org/jsviewer)