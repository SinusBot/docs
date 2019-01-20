### Can I have more than 2 instances?

Yes you can! Check out [this page](https://forum.sinusbot.com/license). (You need to be logged on to the forums, though.)

### My bot eats a lot of RAM. Why?

The bot itself doesn’t use lots of memory but reserves a fair amount. However, this doesn’t count as used, so you don’t need to worry about it. The actual client instances require more RAM, from which a big part is shared between multiple instances - so again: you probably don’t need to worry about it. Google for more information on how to read memory usage on linux.

### Can I control the bot via TS chat commands?

Yes, that's possible. The bot knows about several privileges that a user must have to do several kinds of actions. To make the bot recognize a TS user as a bot user, you can bind a TS account to a bot account on the Edit user page.

All available commands are listed at Settings -> Info -> Commands - including the required privileges to run them.

### What's the maximum length/size of music files?

Uploaded files can be limited through the UploadLimit-option in your config.ini.

### Where and how to get the hosting version? I want to sell the bot! 

The hosting version is not publicly available and won't be before version 1.0. If you are interested in hosting a huge amount of bots (I'm talking 200+ here), feel free to contact @flyth on the forums. The hosting version will not become generally available to everyone anytime soon.

Please refrain from messages like "I'm thinking of starting a business...", "I want to sell the bot, but my website is not yet ready" or such and come back, if you seriously want to apply as a hosting partner and have the proper audience for that. :)

There are no licenses for sponsored hosting, yet.

However, here are some basic facts of that version:
It's capable of running *many* customer-separated instances on one host (I've seen around 180 on a mediocre server - ~2.x GHz Xeon / 8 Cores, 32G RAM - without any load-saving features enabled - with those features enabled, many more instances would be supported). A provisioning API is available for creating & managing customer instances. There are also some protective features in place that prevent misuse of several client-features (banner spamming and such).
Automatic logins can be created from other webinterfaces and the whole frontend API is open, well documented and accessible for further customization / integration.
If you're a serious hosting company and want to do some stress testing, please contact me to get a demo-license that will help you do so.

### What about sponsoring?

Sponsoring the SinusBot is currently not allowed without prior written permission of the author.

### Does the bot run on Raspberry PI / PI 2 or similar ARM based systems?

No - there's no ARM based TS client available, so it makes little sense to port the bot.

### How can I add scripts?

Download the script you want and copy it to the scripts-folder of the bot. Restart the bot and see the settings -> scripts page to activate it.

### Where are my music files stored? Can I upload files via FTP?

When you upload files to the bot, they will be analyzed, indexed and stored in the data-directory of the bot. This ensures consistency, fast access and independent metadata as well as some other features like deduplication.

If you want to use FTP to manage your files, you can use the `ExternalFileBase` setting in your config.ini to point to a directory where the files are stored. The bot will pick them up automatically.

### Will there be a Mac (OSX) Version?

Probably not, sorry.

### How do I get a license?

#### PRIVATE USE

Extended private licenses aren't for sale, yet. It is planned to make them available with version 1.0 or shortly after. If you host a large community, feel free to send a mod a short introduction about your community and explain why you would need a license and with what quantity of instances and we'll look into it. No promises, though. :) 

#### COMMERCIAL USE

Commercial licenses / hosting licenses require special agreements and are only available to selected hosting companies. However, without such a license, hosting / reselling the SinusBot in any commercial way is not allowed.

### Why are you guys so rude?

It sounds like you got an answer you didn't like or think we haven't treated you the way you expect us to.
Usually the staff and the community is really nice. We usually answer to whatever questions you have and we are very patient - even if you're a newbie.

Still, people answer in their spare time and get asked some questions over and over again, even if they have been answered well in the FAQ or on the forums in general. That really gets annoying fast. And because you just didn't search the FAQ or forums before asking on the chat or in a new thread, or posted a thread in caps only (and maybe with the words "FAST!", "ASAP!" or such), you're basically saying that you think your time is worth more than the time of the people you ask. And that is way more rude than just a short unfriendly answer. So please keep that in mind.

If you are such a user: next time, use the search functionality before you ask something. Read the "READ ME BEFORE YOU POST" threads (yes, they're in caps for that reason!) as well.

If you did some research before asking, please tell people that / what you did. If people are still being rude, there have probably been other users just before you asked your question, who didn't do research before. So please be a little patient in such cases and ask kindly again.

Last but not least: the users of this forum speak many different languages, many of them are not native English or German speakers. Politeness can get lost in translation really fast as can messages be interpreted as "rude" even if they're not meant to be. Calm down and try to do your best in understanding each other in such cases :)

### Support Policy / Support Grundregeln

#### English: 

In the past we got tons of support requests in case of the user is using an old and no longer supported version (How to check my Bot Version?) of our software. We don't want this any more... So of course we need some rules!

* Make sure you use an up to date version of:
  * Linux (Ubuntu 14.04, Debian 8, CentOS 7 or better) (*1)
  * Windows (7, 8, 10, Server 2008, 2012 or better).
* with all latest Updates / Service Packs
* Make sure you have the latest Sinusbot version
* Make sure you use a valid license for Teamspeak / a valid hoster with legal licenses. (*2)

1. We want to support more operating systems, but we can't test everything so if you wan't to try the bot on an not-listed platform you can try it. But you should have the knowledge of the platform!
2. We respect Teamspeak, so we will not support invalid or illegal servers no matter what areas.

**Every topic and private message which is violating this rule will be ignored an deleted.**

#### Deutsch:

In der Vergangenheit haben wir massenhaft Support-Anfragen erhalten, wenn der Benutzer eine alte oder nicht mehr unterstützte Version unserer Software verwendet (Wie kann ich meine Bot Version prüfen?). Wir wollen das nicht mehr ... Daher brauchen wir Regeln!

* Stelle sicher, dass du eine aktuelle Betriebssystem Version verwendest:
  * Linux (Ubuntu 14.04, Debian 8, CentOS 7 oder besser) (*1)
  * Windows (7, 8, 10, Server 2008, 2012 oder besser)
* Mit allen Updates / Service Packs
* Stelle sicher, dass du die aktuellste Sinusbot Version hast
* Stelle sicher das du eine gültige Teamspeak Lizenz verwendest, bzw dein Teamspeak Hoster sich an die Teamspeak Richtlinien hält. (*2)

1. Wir wollen mehr Betriebssysteme unterstützen, aber wir können nicht alles testen, wenn man den bot auf einer nicht- gelisteten Plattform ausprobieren möchte kann man das tun. Doch du solltest das Wissen über die Plattform haben!
2. Wir Respektieren Teamspeak, daher werden wir ungültige oder Illegale Server nicht Supporten egal in welchen bereichen.

**Jedes Thema und jede private Nachricht, die gegen diese Regel verstößt, wird ignoriert und gelöscht.**

### Does SinusBot support Discord?

Yes, it does!

### What are outdated Resources?

Resources with the prefix OUTDATED will be removed in the future and might not work currently due script api changes. They are not designed to use in production usage because of e.g. broken script engine compatibility.