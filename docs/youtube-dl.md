# youtube-dl

The bot can use [youtube-dl](https://github.com/ytdl-org/youtube-dl/) to download media files from several [supported websites](https://rg3.github.io/youtube-dl/supportedsites.html).

## Usage

Once you have installed youtube-dl (as described below for Windows and Linux) you can use chat commands like `!yt <url>`, `!ytdl <url>` to play content from any of the [supported websites](https://rg3.github.io/youtube-dl/supportedsites.html), like YouTube for example.

Alternatively you can also download something in your SinusBot web-interface in the "Upload" Page, under "Download Files". You can also [import public playlists from YouTube](https://sinusbot.github.io/docs/faq/features/#download-youtube-playlists).

## Windows

- Install the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) if it isn't installed already
- Download [youtube-dl.exe](https://yt-dl.org/downloads/latest/youtube-dl.exe)
- Save it in the SinusBot directory (same folder the sinusbot.exe is in, for example in `C:\SinusBot\` - depending on where you installed it)
- Restart the SinusBot (in taskbar right-click => close, then start again)

The SinusBot should detect it automatically and commands like `!yt`, `!ytdl`, etc. should be available.

### Manual Update { #windows-update }

Delete the old file and download it again, as described above.

### Troubleshooting { #windows-troubleshooting }

If you face an issue, make sure you have the [Microsoft Visual C++ 2010 Redistributable Package (x86)](https://www.microsoft.com/en-US/download/details.aspx?id=5555) installed.

You should also **try updating youtube-dl** by re-downloading it as described above.

Try downloading something in your SinusBot web-interface on the "Upload" page and check what it shows in the list. "youtube-dl unavailable" indicates that youtube-dl is not installed correctly; In that case reinstall it as shown above.

For further troubleshooting see the [youtube-dl Troubleshooting section for Linux](#linux-troubleshooting).

## Linux

Run the following commands but make sure to adjust the paths to match your SinusBot installation:

```bash
sudo apt-get update
sudo apt-get install python
cd /opt/sinusbot/
curl -L -O https://yt-dl.org/downloads/latest/youtube-dl
chmod a+rx youtube-dl
chown sinusbot:sinusbot youtube-dl
```

Afterwards set `YoutubeDLPath = "/opt/sinusbot/youtube-dl"` in your `config.ini` and restart the SinusBot.

### Automatic updates

If you want youtube-dl to be updated automatically you can add a cronjob that does this by executing:

```bash
echo "0 0 * * * sinusbot /opt/sinusbot/youtube-dl -U --restrict-filenames >/dev/null" > /etc/cron.d/ytdl
```

### Manual Update { #linux-update }

Either install it again, as described above, or use `youtube-dl -U`.

```bash
su sinusbot
youtube-dl -U
```

Note: Replace `youtube-dl` with the correct path to your `youtube-dl` file (i.e. `/opt/sinusbot/youtube-dl` or `/usr/local/bin/youtube-dl`).

### Troubleshooting { #linux-troubleshooting }

Note: Adjust the paths mentioned here to fit your installation. Replace `youtube-dl` with the correct path to your `youtube-dl` file (i.e. `/opt/sinusbot/youtube-dl` or `/usr/local/bin/youtube-dl`).

1. Always make sure that you are using the latest version of youtube-dl (`youtube-dl --version`). You can upgrade it by running `youtube-dl -U` (adjust to your own path) - assuming the user you run this with has write permissions.

2. Try downloading something in your SinusBot web-interface on the "Upload" page and check what it shows in the list.

3. Try manually downloading something with youtube-dl via the command line. You can do that with `youtube-dl -v -i --no-playlist --no-call-home -x <Media URL>`<br/> The sinusbot usually passes the following flags: `-i --no-playlist --no-call-home -J -x`.

#### youtube-dl unavailable

The message "youtube-dl unavailable" indicates that youtube-dl is not installed correctly; In that case reinstall it as shown above.

Make sure that the `YoutubeDLPath` in your `config.ini` is set to the correct path as described above.

#### Common issues with outdated youtube-dl { #outdated data-toc-label='Common outdated issues' }

If your error message includes one of the following:

- Signature extraction failed
- Download Failed
- invalid character 'W' looking for beginning of value

Try updating youtube-dl: `youtube-dl -U`

#### HTTP Error 403: Forbidden { #error-403 }

Remove the signature cache:

```bash
su sinusbot
youtube-dl --rm-cache-dir
```

and then try again.

#### HTTP Error 429: Too Many Requests or 402: Payment Required { #error-429 }

These two error codes indicate that the service (for example YouTube) is blocking your IP address because of overuse. Usually this is a soft block, meaning that you can gain access again after solving a CAPTCHA. Please [read the youtube-dl FAQ section](https://github.com/ytdl-org/youtube-dl#http-error-429-too-many-requests-or-402-payment-required) for more details.

While **this is not a bug**, you could at least try the following if you use an IPv6 address:

Create the file `/etc/youtube-dl.conf` with the content `--force-ipv4` and then try again. </br>
You can do this easily with the following command: `echo "--force-ipv4" >> /etc/youtube-dl.conf`

If you still receive this error afterwards:

This is neither a bug in youtube-dl nor the SinusBot. This error means that YouTube is limiting your IP-address.
Unfortunately there is nothing else that you could do other than trying to use a different IP-address.

*Note: youtube-dl has [network options](https://github.com/ytdl-org/youtube-dl/blob/master/README.md#network-options) such as `--source-address <ip>` to select the correct ip-address in case your server has more than one and `--proxy <url>` that you can use to route requests over another server with a http(s)/socks proxy, however we will **not** help you with configuring this as it has nothing to do with the SinusBot itself.*

#### Assuming --restrict-filenames since file system encoding cannot encode all characters. Set the LC_ALL environment variable to fix this. { #assuming-restrict-filenames data-toc-label='Assuming --restrict-filenames since file system encoding cannot encode all characters' }

This is only a warning, not an error, however you can you can solve it by setting your system locale to something ending in `UTF-8`.

On Debian/Ubuntu you can set your locale with: `dpkg-reconfigure locales`<br>
Select something (use the arrow keys to navigate and ++space++ to select/deselect items) that ends in `UTF-8`, e.g. `en_US.UTF-8` and confirm your selection (++tab++ switches the highlighted button/field and ++enter++ activates it).

Afterwards restart your system or your SinusBot to make sure that the changes are applied.
