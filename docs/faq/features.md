### How can I playback audio from streaming sites?

You can install youtube-dl and configure the bot to use it. Afterwards you are able to playback URLs from every source youtube-dl supports. However, there will be no support for youtube-dl related issues.
Download youtube-dl from the website (the version of your linux distribution is probably outdated)
edit the config.ini and change YoutubeDLPath = "" to YoutubeDLPath = "/your/path/to/youtube-dl"
On launch, the bot will tell you if it found youtube-dl and if it’s compatible.

Some websites don't allow downloading, so make sure you don't use the bot for those sites.

### How does Text-to-Speech (TTS) work? I need an URL for that!

Search the forums for some URLs you can use with the bot. Also, see [this page](../tts.md) for more information.

### Can I download whole playlists from YouTube?

Yes, you can. When creating a new playlist, you have the option to enter a URL from which the playlist will be fetched then.

### I want to integrate the bot into my website / remote control the bot via script. How can I do that?

The API documentation of the Bot can be found [here](https://www.sinusbot.com/api). Samples and libraries can be found in the [3rd party forums](https://forum.sinusbot.com/resources/categories/3rd-party-tools-libraries.11/).

### How can guests control the bot?

You can bind a bot user to a server group for that (for example: your default guest group) and set the privileges you want the guests to have. The webinterface will however always require a login.
