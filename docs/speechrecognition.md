# Speech Recognition

!!! warning "Speech Recognition is not very reliable and currently only works on TeamSpeak."

This is a little tutorial on how to use speech recognition. The feature is still **highly experimental** and will cause increased CPU & RAM usage. I've tried to make it so it only activates if it is really necessary.

[Discuss this feature on the forums.](https://forum.sinusbot.com/threads/using-speech-recognition.1693/)

## Requirements

* you need at least SinusBot version 0.13.37
* you will need to provide the commands that should be recognized beforehand for now
* there is no continuous recognition
* only 3 speakers will be recognized simultaneously, additional speakers will be ignored until one of the initial 3 speakers will stop speaking; in most cases that is more than enough
* speech recognition will only work on licensed instances for now
* TS3 only

## Preparation

* set `Enable = true` in section `[SpeechRecognition]` of the config.ini
* Download [https://www.sinusbot.com/pre/speech.tar.bz2](https://www.sinusbot.com/pre/speech.tar.bz2)
* Extract that file to the same directory as your SinusBot (so you will have a new folder speech inside the SinusBot directory)
* Create a script that uses the speech recognition engine
* Restart the bot

## Code Example

```javascript
registerPlugin({
    name: 'Speech Recognition Demo',
    version: '1.0',
    description: 'This is a simple script that will stop playback when you say "stop"',
    author: 'Michael Friese <michael@sinusbot.com>',
    vars: [],
    voiceCommands: ['stop']
}, function(sinusbot, config) {
    var event = require('event');
    var engine = require('engine');
    var audio = require('audio');
    var media = require('media');

    audio.setAudioReturnChannel(2);

    event.on('speech', function(ev) {
        if (ev.text == 'stop') {
            engine.log('Stopping playback on behalf of client ' + ev.client.nick());
            media.stop();
        } else {
            engine.log(ev.client.nick() + ' just said ' + ev.text);
        }
    });
});
```

So it's pretty simple: you register some voiceCommands in the plugins' manifest. Once one of the registered commands is recognized, the speech event gets triggered with an object containing the clientId and the recognized command (a full client object will be added later on).

> Important: Only words that are inside the ./speech/dict file will be recognized. It already contains many english words and their phonetic "translation". If you need words that are not in there, you have to add them (and the translation) manually before you can use them.

In most simple cases it works well enough, so don't try to recognize full sentences but focus on simple commands. Also, you might want to let the commands start with a word like "bot", so that you don't trigger things by accident ;)
