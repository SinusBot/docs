# Installing youtube-dl

The bot can use [youtube-dl](https://rg3.github.io/youtube-dl/) to download media files from several [supported websites](https://rg3.github.io/youtube-dl/supportedsites.html).

## Windows

- Install the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) if it isn't installed already
- Download [youtube-dl.exe](https://yt-dl.org/downloads/latest/youtube-dl.exe)
- Save it in the bot directory (same folder the sinusbot.exe is in, for example in `C:\SinusBot\` - depending on where you installed it)
- Restart the bot

The bot should detect it automatically and commands like `!yt`, `!ytdl`, etc. should be available.

### Troubleshooting

If you face an issue, make sure you have the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) installed.

You should also try updating youtube-dl by redownloading it as described above.

## Linux

Run the following commands but make sure to adjust the path to match your SinusBot installation:

```bash
sudo apt-get update && sudo apt-get install python
cd /opt/sinusbot/
curl -L -O https://yt-dl.org/downloads/latest/youtube-dl
chmod a+rx youtube-dl
```

The bot should detect it automatically and commands like `!yt`, `!ytdl`, etc. should be available.

### Automatic updates

If you want youtube-dl to be updated automatically you can add a cronjob that does this by executing:

```bash
echo "0 0 * * * sinusbot /opt/sinusbot/youtube-dl -U --restrict-filename >/dev/null" > /etc/cron.d/ytdl
```

### Troubleshooting

Always make sure that you are using the latest version of youtube-dl. You can upgrade it by running `/opt/sinusbot/youtube-dl -U` (adjust to your own path) - assuming the user you run this with has write permissions.

You should also try manually downloading something with youtube-dl via the command line before reporting a bug. You can do that with `/opt/sinusbot/youtube-dl <mediaurl>`.

#### HTTP error 429: Too many requests

- Create/modify the file `/etc/youtube-dl.conf`
- Paste this inside the file: `--force-ipv4`
- Save and try again, the error should be fixed.

#### Signature extraction failed

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`

#### Download Failed

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`

#### invalid character 'W' looking for beginning of value

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`
