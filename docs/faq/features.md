### How can I playback audio from 3rd party sites? { data-toc-label='Playback from 3rd party sites' }

!!! success ""
    You can [install youtube-dl](../../youtube-dl/) to playback URLs from every source youtube-dl supports. However, there will be no support for youtube-dl related issues.

    Some websites don't allow downloading, so make sure you don't use the bot for those sites.

### How does Text-to-Speech (TTS) work? I need an URL for that! { #tts data-toc-label='Text-to-Speech (TTS)' }

!!! success ""
    Search the forums for some URLs you can use with the bot. Also, see [this page](../tts.md) for more information.

### Can I download whole playlists from YouTube? { #download-youtube-playlists data-toc-label='Download YouTube Playlists' }

!!! success ""
    Yes, you can. This requires [installing youtube-dl](../../youtube-dl/). When creating a new playlist click "Show advanced options", then you have the option to enter a URL from which the playlist will be fetched.

### I want to integrate the bot into my website / remote control the bot via script. How can I do that? { #sinusbot-api-integration data-toc-label='SinusBot API Integration' }

!!! success ""
    The API documentation of the Bot can be found [here](https://www.sinusbot.com/api). Samples and libraries can be found in the [3rd party forums](https://forum.sinusbot.com/resources/categories/3rd-party-tools-libraries.11/).

### How can guests control the bot?

!!! success ""
    Create a bot user account in your web-interface, edit it afterwards and bind it to the server group ID `-1` (this will match everyone). Then set the privileges you want the guests to have. The web-interface will however always require a login.
