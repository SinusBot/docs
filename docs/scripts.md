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

```javascript
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

Using this, you can define which restricted modules the script wants to use. If it's not allowed via the config, the script will not load at all but instead return an error on startup. This field is mandatory if you use any restricted module from version 1.0 onwards.

##### vars (array)

## Variables

This is probably the most complex parameter as this defines the configuration interface that will be shown on the web interface of the bot.

Current available variable types:

| Type      | Input |
| --- | --- |
| string    | Show a regular input element where the user can enter some text |
| password  | like string but doesn't display the text you've entered |
| strings   | set multiple strings |
| multiline | this will display a text area where the user can enter several lines of text |
| number    | Show a regular input element, but only accept numeric input from the user |
| track     | %%Show an input where the user can search and specify a track that has been uploaded to the bot - the config variable will later on contain an object like this: { "url": "track://uuid", "title": "A short title of the track" } %%|
| tracks    | select multiple tracks |
| channel   | If the bot is connected, this displays a channel selector. The config variable will later on hold the channel-id of the selected channel |
| select    | this will display a select box. All options need to specified in an array called options and the config value will later on hold the index to the selected option. |
| checkbox  | this will display a checkbox |
| array     | this allows the user to add an unspecified amount of items |

Example of the string type usage:
```
{
    name: 'ExampleName',
    title: 'message type',
    type: 'string',
    placeholder: 'Some example placeholder'
}
```

Example of the select type usage:

```
{
    name: 'fooType',
    title: 'Variations of foobar',
    type: 'select',
    options: ['Foo', 'Bar', 'Foobar', 'Barfoo']
}
```

Example of the condition type with the above options example:

```
{
    name: 'fooSwitch',
    title: 'Selected fooType',
    type: 'select',
    conditions: [{        //make a field visible or invisible in the config with conditions
        field: 'fooType', //this will tell to use the config field with the name "fooType"
        value: 2,         //this will tell to use the 3rd index of the options of the selected type in this case "Foobar"
    }]
}
```

You can print these values in the log by using:

```
engine.log(config.ExampleName);
engine.log(config.fooType);
```

##### voiceCommands ([]string)

This parameter is only used for the speech recognition feature and may contain one or more strings that are to be detected for the given script.
Note that the speech recognition only works with licensed instances.
You can find more details on how to use it [here](speechrecognition).

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
