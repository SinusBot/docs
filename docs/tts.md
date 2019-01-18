# Text-to-Speech

Since version 1.0, SinusBot has two options for you to use Text-to-Speech. You can either

* have the bot use an online service to do the speech synthesis or
* install some libraries from the Chromium project to generate speech on your computer/server

Both come with advantages and disadvantages - using an online service will most likely generate some cost, while using your server to generate voice will consume quite some CPU power.

## Using an online service

To let your bot speak via an online service, you need to register with such a service and get a valid URL (link) that the bot can use to do the actual conversion.

`Settings -> Instance Settings` has got a field called `TTS-Url` where you can enter such a URL.

To make this actually work, you have to replace the parameter that contains the text to `__TEXT` and the locale (if that can be configured via the service) to `__LOCALE`.

If you are using the locale feature, please also provide the default locale in the appropriate field.

Afterwards click `Save changes`.

Hit `Alt+S` in the bot interface to run a test. If everything was successful, you should hear the bot saying what you entered after a short delay.

Given you have a tts provider that handed you an URL in the form of

	http://a-great-tts-provider.com/doTTS?text=Test&locale=en

you will have to replace the "Test" in the URL with `__TEXT` and that "en" with `__LOCALE`, so that it looks like

	http://a-great-tts-provider.com/doTTS?text=__TEXT&locale=__LOCALE

See the [[https://forum.sinusbot.com/threads/text-to-speech-apis-for-sinusbot.500|forums]] for a list of providers known to support this kind of URLs.

## Installing libraries from the Chromium project

> These are basic instructions for Linux. You need at least SinusBot 1.0 for this to work.

* Download and install the library and the voices

```bash
cd /opt/sinusbot/tts
wget https://chromium.googlesource.com/chromiumos/platform/assets/+archive/master/speech_synthesis/patts.tar.gz
tar -xzf patts.tar.gz
rm patts.tar.gz
unzip tts_service_x86_64.nexe.zip
```

If the last command fails, you probably need to install unzip first. On Debian/Ubuntu this can be done with `apt install unzip`.

Afterwards, edit your config.ini ato contain the following:

```ini
[TTS]
Enabled = true

[[TTS.Modules]]
Locale = "en-US"
Filename = "voice_lstm_en-US.zvoice"
PipelineFile = "voice_lstm_en-US/sfg/pipeline"
Prefix = "voice_lstm_en-US/sfg/"
Instances = 2

[[TTS.Modules]]
Locale = "de-DE"
Filename = "voice_lstm_de-DE.zvoice"
PipelineFile = "voice_lstm_de-DE/nfh/pipeline"
Prefix = "voice_lstm_de-DE/nfh/"
Instances = 2
```

You can get the proper settings for the PipelineFile and Prefix parameters from the corresponding .js files. Some voices (those that have files beginning with remote_) need to be downloaded separately first.

The `Instances` parameter limits the number of concurrent synthesis processes - each of those consumes about 40-100 MB RAM and some CPU cycles. `Locale` is the locale parameter that is actually used by the bot.
