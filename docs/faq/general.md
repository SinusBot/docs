### Can I have more than 2 instances? How do I get a license? { #more-instances data-toc-label='More Instances?' }

!!! success ""
    Yes you can! Check out the page about [Licenses](../../licenses/) for more.
    For the Linux version you don't need a license anymore. The licensing system was removed in v1.0.1.

### Where and how to get the hosting version? I want to sell the bot! { #commercial-use data-toc-label='Commercial Use?' }

!!! success ""
    The SinusBot software is free for personal use only. If you want to use it commercially, please contact the author.

    The hosting version is **not publicly available**. If you are interested in hosting a huge amount of bots (I'm talking 200+ here), feel free to contact [@flyth](https://forum.sinusbot.com/members/flyth.2/) on the forums. The hosting version will not become generally available to everyone anytime soon.

    Please refrain from messages like "I'm thinking of starting a business...", "I want to sell the bot, but my website is not yet ready" or such and come back, if you seriously want to apply as a hosting partner and have the proper audience for that. :)

    There are no licenses for sponsored hosting, yet.

    However, here are some basic facts of that version:
    It's capable of running *many* customer-separated instances on one host (I've seen around 180 on a mediocre server - ~2.x GHz Xeon / 8 Cores, 32G RAM - without any load-saving features enabled - with those features enabled, many more instances would be supported). A provisioning API is available for creating & managing customer instances. There are also some protective features in place that prevent misuse of several client-features (banner spamming and such).
    Automatic logins can be created from other webinterfaces and the whole frontend API is open, well documented and accessible for further customization / integration.
    If you're a serious hosting company and want to do some stress testing, please contact me to get a demo-license that will help you do so.

### Is sponsoring allowed? { #sponsoring}

!!! success ""
    Sponsoring the SinusBot is currently not allowed without prior written permission of the author.

    Private use (non-commercial and neither profiting directly nor indirectly in any way) such as sharing with your friends is fine of course.

### Where can I find the version of my SinusBot?  { #what-is-my-version}

!!! success ""
    If the bot is already running, open up the web interface and go to **Settings** > **Info** > **About**.
    
    If the bot is not running, you can start it with `./sinusbot -v` on your command line and it will display the version information there.

### My bot eats a lot of RAM. Why? { #high-ram-usage data-toc-label='High RAM Usage?' }

!!! success ""
    The sinusbot itself doesn't use lots of memory but reserves a fair amount. However, this doesn't count as used, so you don't need to worry about it. More details about memory usage on Linux can be found [here](https://www.linuxatemyram.com/).

    The actual TeamSpeak Client instances require more RAM, from which a big part is shared between multiple instances - so again: you probably don't need to worry about it.

    If you TeamSpeak Server has an big/animated server banner than that will significantly increase RAM usage.

### Can I control the bot via chat commands? { #chat-commands data-toc-label='Chat Commands?' }

!!! success ""
    Yes, that's possible. The bot knows about several privileges that a user must have to do several kinds of actions. To make the bot recognize a user as a bot user, you can bind an account to a bot account on the Edit user page.

    All available commands are listed at Settings -> Info -> Commands - including the required privileges to run them. Recent SinusBot versions also have a `!help` command.

### My Bot doesn't respond to chat commands on Discord. Why? { #no-chat-commands-response data-toc-label='Discord Chat Commands broken?' }

!!! success ""
    Check in the [Discord Developer Portal](https://discord.dev) whether the Message Content Intent is enabled for your bot. It is required for bots to see the actual message content.
    Read [this](https://support-dev.discord.com/hc/en-us/articles/4404772028055-Message-Content-Privileged-Intent-FAQ) for information about the intent.

### What's the maximum length/size of music files? { #max-file-size data-toc-label='Max. file size?' }

!!! success ""
    Uploaded files can be limited through the UploadLimit-option in your config.ini (see [Configuration](../../configuration/)).
    Also note that reverse-proxies can limit the file size too.

### Does the bot run on Raspberry PI / PI 2 or similar ARM based systems? { #arm data-toc-label='Raspberry PI/ARM Support?' }

!!! success ""
    No - there's no ARM based TS client available, so it makes little sense to port the bot.

### How can I add scripts?

!!! success ""
    Download the script you want and copy it to the scripts-folder of the bot. Restart the bot and see the settings -> scripts page to activate it.

### Where are my music files stored? Can I upload files via FTP? { #where-are-music-files-stored data-toc-label='Where are music files stored?' }

!!! success ""
    When you upload files to the bot, they will be analyzed, indexed and stored in the data-directory of the bot. This ensures consistency, fast access and independent metadata as well as some other features like deduplication.

    If you want to use FTP to manage your files, you can use the `ExternalFileBase` setting in your config.ini to point to a directory where the files are stored. The bot will pick them up automatically.

### Will there be a macOS Version? { #macos data-toc-label='macOS Support?' }

!!! success ""
    Probably not directly, sorry.

    As a workaround you can currently use the [Docker image](https://hub.docker.com/r/sinusbot/docker), but that requires knowledge of Docker and the command line.

### Why are you guys so rude?

!!! success ""
    It sounds like you got an answer you didn't like or think we haven't treated you the way you expect us to.
    Usually the staff and the community is really nice. We usually answer to whatever questions you have and we are very patient - even if you're a newbie.

    Still, people answer in their spare time and get asked some questions over and over again, even if they have been answered well in the FAQ or on the forums in general. That really gets annoying fast. And because you just didn't search the FAQ or forums before asking on the chat or in a new thread, or posted a thread in caps only (and maybe with the words "FAST!", "ASAP!" or such), you're basically saying that you think your time is worth more than the time of the people you ask. And that is way more rude than just a short unfriendly answer. So please keep that in mind.

    If you are such a user: next time, use the search functionality before you ask something. Read the "READ ME BEFORE YOU POST" threads (yes, they're in caps for that reason!) as well.

    If you did some research before asking, please tell people that / what you did. If people are still being rude, there have probably been other users just before you asked your question, who didn't do research before. So please be a little patient in such cases and ask kindly again.

    Last but not least: the users of this forum speak many different languages, many of them are not native English or German speakers. Politeness can get lost in translation really fast as can messages be interpreted as "rude" even if they're not meant to be. Calm down and try to do your best in understanding each other in such cases :)

### Support Policy / Support Grundregeln { #support-policy data-toc-label='Support Policy' }

???+ info "English"
    In the past we got tons of support requests in case of the user is using an old and no longer supported version ([How to check my Bot Version?](https://sinusbot.github.io/docs/faq/general/#what-is-my-version)) of our software. We don't want this any more... So of course we need some rules!

    * Make sure you use an up to date version of:
        * Linux (Ubuntu 18.04+, Debian 9+, CentOS 7+ or better)
        * Windows (10, Server 2012 or better), with all latest Updates / Service Packs
    * Make sure you have the latest SinusBot version
    * Make sure you use a valid license for Teamspeak / a valid hosting provider with legal licenses.

    1. We want to support more operating systems, but we can't test everything so if you wan't to try the bot on an not-listed platform you can try it. But you should have the knowledge of the platform!
    2. We respect Teamspeak, so we will not support invalid or illegal servers no matter what areas.

    **Before posting: [READ THIS FIRST](https://forum.sinusbot.com/threads/read-me-before-you-post.342/).** Thanks!

    **Every topic and private message which is violating this rule will be ignored/deleted.**

???+ info "Deutsch"
    In der Vergangenheit haben wir massenhaft Support-Anfragen erhalten, wenn der Benutzer eine alte oder nicht mehr unterstützte Version unserer Software verwendet ([Wie kann ich meine Bot Version prüfen?](https://sinusbot.github.io/docs/faq/general/#what-is-my-version)). Wir wollen das nicht mehr ... Daher brauchen wir Regeln!

    * Stelle sicher, dass du eine aktuelle Betriebssystem Version verwendest:
        * Linux (Ubuntu 18.04+, Debian 9+, CentOS 7+ oder besser)
        * Windows (10, Server 2012 oder besser), mit allen Updates / Service Packs
    * Stelle sicher, dass du die aktuellste SinusBot Version hast
    * Stelle sicher das du eine gültige Teamspeak Lizenz verwendest, bzw dein Teamspeak Hoster sich an die Teamspeak Richtlinien hält.

    1. Wir wollen mehr Betriebssysteme unterstützen, aber wir können nicht alles testen, wenn man den bot auf einer nicht- gelisteten Plattform ausprobieren möchte kann man das tun. Doch du solltest das Wissen über die Plattform haben!
    2. Wir Respektieren Teamspeak, daher werden wir ungültige oder Illegale Server nicht Supporten egal in welchen bereichen.

    **Befor du etwas postest: [LIES MICH](https://forum.sinusbot.com/threads/lies-mich-bevor-du-schreibst.146/).** Danke!

    **Jedes Thema und jede private Nachricht, die gegen diese Regel verstößt, wird ignoriert/gelöscht.**
