# Using & creating Scripts

Your bot can be extended by installing scripts from other users or by writing and activating your own scripts. Such scripts can react on several events and control how the bot should react to them.

This can be a simple 'Hello' response when someone writes 'hello' to the bot or a pretty detailed leveling/xp system where the bot tracks the online time of each user. You can find many scripts from other users [here](https://forum.sinusbot.com/resources/categories/scripts.2/).

The language the scripts have to be in is JavaScript (ECMAScript Version 5). Since version 1.0 you can now also use newer ES6 features.

The full API documentation of the API that is available to you can be found [here](https://sinusbot.github.io/scripting-docs/).


## How to install a script?

When you download scripts manually, you should get files that end with .js. Copy those files into the scripts folder within the installation directory.

> A bot restart is required whenever you add or remove a script manually.

Should you have downloaded a zip/rar or whatever file, make sure to unpack it first.

> Some scripts also come with more files than just the main script file. In such cases make sure you copy them exactly in the same structure as you've downloaded them (keeping all folders that came with the script). This is usually true for scripts that come with their own web interface.


## Writing a script

So you've searched for a script and found nothing that fully suits you, right? The best way to get started with writing a script is usually to have a look at other scripts first and try to understand how they work. If you for example want to have a custom welcome script, have a look at how the existing ones work and make slight adjustments instead of directly writing it from scratch.

> The source code of scripts should usually be readable so you can extend / modify them. Should you plan to publish changes to another script however, make sure you contact the original author and ask for permission.


## Writing a script from scratch

### Basic structure and manifest

Every script must register itself using the `registerPlugin` function. This function takes two arguments:

* the manifest as an object
* the setup function of your script

First, let's see what a manifest consists of. The manifest will determine which features are available to the script and also contain metadata and variables that will be shown in the web interface. It's also used to make sure the script works with the current version of the bot.

```
registerPlugin({
    name: 'Demo Script',
    version: '1.0',
    description: 'This example actually does nothing',
    author: 'Sinus Bot <bot@sinusbot.com>',
    vars: [],
    autorun: true
}, function(sinusbot, config) {
    ...
});
```

#### Mandatory fields

##### name (string)

The name field should contain a short name of your script.

##### author (string)

Put your name and your email address in here in the form of "your name 
<your-email@example.com\>"

##### description (string)

This should contain a longer description - tell the user what exactly your script does.

##### version (string)

Start with something like 1.0 and increase it with every release.

#### Optional fields

##### autorun (bool)

Set to true, if you want the script to be run on every instance, without the option to disable it.

##### backends ([]string)

Per default, scripts will only be available on TS3 instances. If your script supports Discord (or in the future maybe other backends) as well, you have to specify this explicitly by setting this variable to an array containing all backends like so: `backends: ["ts3", "discord"]`

##### enableWeb (bool)

If your script required own web content, you can set enableWeb to true and put files into the ./scripts/scriptname/html directory. After restart, the script title will be clickable and lead to an index.html inside that html-directory you just created.

From there you have access to the localStorage variables containing the login and may communicate with the bot api from your own pages.

##### engine (string)

Sets the required engine version (bot version). This uses [Semantic Versioning](http://semver.org). Example: `>= 0.9.16`

##### hidden (bool)

Hides the script from the settings page. Should be used together with `autorun`.

> Hidden scripts can not have variables (vars), since they'd never be shown and thus not configurable.


##### requiredModules ([]string)

Using this, you can define which restricted modules the script wants to use. If it's not allowed via the config, the script will not load at all but instead return an error on startup. If you only optionally use features from restricted modules, don't use this but provide a fallback in your script.

##### vars (array)

More information about the usage of variables can be found [[en:guides:features:scripts:variables|here]].

##### voiceCommands ([]string)

This parameter is only used for the speech recognition feature and may contain one or more strings that are to be detected for the given script.
Note that the speech recognition only works with licensed instances.
You can find more details on how to use it here:
[[en:guides:features:speechrecognition]]

### The Setup-Function

Following the manifest, you hand over a function to registerPlugin that will be called upon activation with two or more parameters. The first one, `sinusbot`, can be ignored if you use the new scripting engine. The second one will hold the configuration of the plugin that the user set from within the web interface (given you have added anything to the `vars` field of your script manifest).

Use this function to setup event listeners and do stuff on initialization.

Example

```
registerPlugin({
	...
}, function(sinusbot, config) {
	var event = require('event');
	event.on('chat', function(chatEvent) {
		// Do something...
	});
});
```
	
As said, the function will get called once the script gets activated either by enabling it in the web interface or when autorun is enabled.
In this example an event handler is installed that will be called whenever a chat message has been sent.
