# Installing youtube-dl

The bot can use [youtube-dl](https://github.com/ytdl-org/youtube-dl/) to download media files from several [supported websites](https://rg3.github.io/youtube-dl/supportedsites.html).

## Windows

- Install the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) if it isn't installed already
- Download [youtube-dl.exe](https://yt-dl.org/downloads/latest/youtube-dl.exe)
- Save it in the bot directory (same folder the sinusbot.exe is in, for example in `C:\SinusBot\` - depending on where you installed it)
- Restart the bot

The bot should detect it automatically and commands like `!yt`, `!ytdl`, etc. should be available.

### Troubleshooting

If you face an issue, make sure you have the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) installed.

You should also **try updating youtube-dl** by redownloading it as described above.

## Linux

Run the following commands but make sure to adjust the path to match your SinusBot installation:

```bash
sudo apt-get update && sudo apt-get install python
cd /opt/sinusbot/
curl -L -O https://yt-dl.org/downloads/latest/youtube-dl
chmod a+rx youtube-dl
chown sinusbot:sinusbot youtube-dl
```

Afterwards set `YoutubeDLPath = "/opt/sinusbot/youtube-dl"` in your `config.ini` and restart the SinusBot.

### Automatic updates

If you want youtube-dl to be updated automatically you can add a cronjob that does this by executing:

```bash
echo "0 0 * * * sinusbot /opt/sinusbot/youtube-dl -U --restrict-filename >/dev/null" > /etc/cron.d/ytdl
```

### Troubleshooting

Always make sure that you are using the latest version of youtube-dl. You can upgrade it by running `/opt/sinusbot/youtube-dl -U` (adjust to your own path) - assuming the user you run this with has write permissions.

You should also try manually downloading something with youtube-dl via the command line before reporting a bug. You can do that with `/opt/sinusbot/youtube-dl <mediaurl>` (the sinusbot usually passes the following flags: `-i --no-playlist --no-call-home -J -x <mediaurl>`).

Make sure that the `YoutubeDLPath` in your `config.ini` is set to the correct path as described above.

Try downloading something in your SinusBot webinterface on the "Upload" page and check what it shows in the list. "youtube-dl unavailable" indicates that youtube-dl is not installed correctly; In that case reinstall it as shown above.

#### Signature extraction failed

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`

#### Download Failed

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`

#### invalid character 'W' looking for beginning of value

- Try updating youtube-dl: `/opt/sinusbot/youtube-dl -U`

#### HTTP error 429: Too many requests

Create the file `/etc/youtube-dl.conf` with the content `--force-ipv4` and then try again. </br>
You can do this easily with the following command: `echo "--force-ipv4" >> /etc/youtube-dl.conf`

If you still receive this error afterwards:

This is neither a bug in youtube-dl nor the SinusBot. This error means that **YouTube** is limiting your IP-address. </br>
Unfortunately there is nothing else that you could do other than trying to force ipv4 (as described above) or trying to use a different IP-adress.

*Note: youtube-dl has [network options](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#network-options) such as `--source-address <ip>` to select the correct ip-address in case your server has more than one and `--proxy <url>` that you can use to route requests over another server with a http(s)/socks proxy, however we will **not** help you with configuring this as it has nothing to do with the SinusBot itself.*
