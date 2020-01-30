# What is new?

## Version 1.0

> This entry might change until the 1.0 version has become stable.

### Scripting: Introducing v8

The scripting engine has been changed to v8 - that's the engine that also powers the Chrome browser and node.js. The change will bring many advantages such as ES6 compatibility and an increased control over the resources used by it.

This comes with a couple of changes that script authors need to adapt their scripts to. More info can be found in the [changelog of Alpha 1](https://forum.sinusbot.com/resources/internal-beta.1/updates#resource-update-1119).

For users of scripts, it has been made easier to grant a script permission to use restricted modules. When previously you had to edit your config.ini to specifically allow a script to access a database or the filesystem, you can now view the required privileges of a script and accept them automatically when you activate it - just like you do with apps on your phone. Please be careful when installing scripts, especially when they want to use the restricted modules.

### External File Support

With version 1.0 you can store files outside of the bot itself and have the bot "import" and use them on-the-fly. This means that if you already have your music collection on the server, you don't need to manually import it into the bot anymore. Or if you want to use (S)FTP to manage your files, you can use that as well. Just add or modify the `ExternalFileBase` in your config.ini to point to your music directory.

### Integrated Text-to-Speech environment

We've integrated the Native Client functionality from the Chromium project into the bot - that means that you can use the same offline TTS engine you probably know from the Chrome browser or your Android phone. More info on that can be found [here](tts.md).

### Better support for Discord

The Discord backend has also seen several of additions - you can for example now bind server roles to SinusBot accounts just like you can bind them to server groups on TeamSpeak.
