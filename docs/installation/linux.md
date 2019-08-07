**If you are new to Linux and/or wish to have everything installed for you in a more convenient way, we encourage you to use the [Installer Script](https://forum.sinusbot.com/resources/sinusbot-installer-script.58/).**

### Compatible Versions

SinusBot Version | TS3 Version  | Linux Kernel Version
-----------------|--------------|-------------------------
1.0.0-beta4      | 3.3          | 3.17+
1.0.0-beta3      | 3.3          | 3.17+
1.0.0-beta2      | 3.2.5        | 2.6+
1.0.0-beta1      | 3.2.5        | 2.6+

### Manual installation

Let's start by installing several dependencies:

TS3.3+ requires at least a Linux Kernel of version 3.17 or higher!

```bash
apt-get update
apt-get install -y x11vnc xvfb libxcursor1 ca-certificates bzip2 libnss3 libegl1-mesa x11-xkb-utils libasound2 libpci3 libxslt1.1 libxkbcommon0 curl
update-ca-certificates
```

On Debian and some Ubuntu versions you might as well have to install, so at least try

```bash
apt-get install libglib2.0-0
```

**In case of Ubuntu 18.04**: Depending on the Ubuntu installation the `universe` repository of Ubuntu is not activated, resulting in missing packages for required dependencies *x11vnc* and *xvfb*. When said problem ocurrs, enable the `universe` repository by using following command:

```bash
add-apt-repository universe
apt-get update
```

After all required dependencies are installed, let's assume that you're going to install the bot to `/opt/sinusbot` and are using the user `sinusbot` with the group `sinusbot`. We will install the bot with root then switch to this user account when running the bot.

You will need to create an new user `sinusbot` on your server, so to do so type the following command.

```bash
adduser --disabled-login sinusbot
```

This created user is used to start the bot with usual user privileges (which is highly recommended!), as the bot should **not** run as root for security-reasons.

Next we will create and prepare the folder where Sinusbot will be installed to, by issuing following commands as the root user:

```bash
mkdir -p /opt/sinusbot # create folder
chown -R sinusbot:sinusbot /opt/sinusbot # grant sinusbot user permissions on specified folder
```

(If you're using another user/group than "sinusbot", replace sinusbot:sinusbot with **yourusername:yourusergroup**)

Then we will switch over to the recently created user dedicated for the sinusbot, change the working directory and to download the latest Sinusbot release:

```bash
su sinusbot
cd /opt/sinusbot
wget https://www.sinusbot.com/dl/sinusbot.current.tar.bz2
```

If that command results in SSL-Errors, you can **alternatively** try

```bash
curl -O https://www.sinusbot.com/dl/sinusbot.current.tar.bz2
```

Next, extract the bot:

```bash
tar -xjf sinusbot.current.tar.bz2
```

Copy the configuration (if you haven't started the bot before)

```bash
cp config.ini.dist config.ini
```

Now you need to download the TeamSpeak 3 Client and **install it**.

```bash
wget https://files.teamspeak-services.com/releases/client/3.3.0/TeamSpeak3-Client-linux_amd64-3.3.0.run
chmod 0755 TeamSpeak3-Client-linux_amd64-3.3.0.run
./TeamSpeak3-Client-linux_amd64-3.3.0.run
```

You will need to accept the terms.
You do this by pressing enter to scroll through the text or press q to simply go to the end.

Now you need to configure the ini-File of the bot to match your directories.

```bash
nano config.ini
```

Make sure that the TS3Path is correct (if you followed this tutorial step by step, it should already match):

```toml
TS3Path = "/opt/sinusbot/TeamSpeak3-Client-linux_amd64/ts3client_linux_amd64"
```

Close the editor (++ctrl+o++, ++enter++, ++ctrl+x++).

Remove the file 'libqxcb-glx-integration.so' from the clients 'xcbglintegrations' directory:

```bash
rm TeamSpeak3-Client-linux_amd64/xcbglintegrations/libqxcb-glx-integration.so
```

Create the plugins folder in the ts3client directory:

```bash
mkdir TeamSpeak3-Client-linux_amd64/plugins
```

And finally copy the plugin to the plugins-directory of the TeamSpeak-Installation

```bash
cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/
```

Just to make sure that the bot is executable, enter

```bash
chmod 755 sinusbot
```

### Update

(This instructions needs to be done using the sinusbot user.)

Make sure you're using the latest version:

```bash
cd /opt/sinusbot
wget https://www.sinusbot.com/dl/sinusbot.current.tar.bz2
tar -xjvf sinusbot.current.tar.bz2
cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/
```

If you are updating from `3.X` to `3.1.X` then you need to remove the `data/ts3` directory and the `libqxcb-glx-integration.so` file as well:

```bash
rm -rf data/ts3
rm TeamSpeak3-Client-linux_amd64/xcbglintegrations/libqxcb-glx-integration.so
```

### Usage

As [the bot won't run as root](https://sinusbot.github.io/docs/faq/installation/#why-cant-i-run-the-bot-as-root) you will need to switch to the user that you have installed the bot on, if you followed the tutorial, this will be 'sinusbot". To do this use the following command:

```bash
su sinusbot
```

Starting the bot

```bash
./sinusbot
```

Stopping the bot with ++ctrl+c++

**If you want to keep the bot running when you exit out of the terminal follow the instruction on how to [install a startscript](#using_a_startscript).**

Now login at `http://<your ip>:8087/` with user **admin** and the password provided on first run. (see [FAQ](https://sinusbot.github.io/docs/faq/installation/#what-is-the-default-username-and-password) on how to reset)

## Troubleshooting

Look for any errors in the sinusbot/instance log and try to look-up solutions on our forum or your favourite search engine.

If you ask us or our community for help then please provide all of the information mentioned in [READ ME BEFORE YOU POST](https://forum.sinusbot.com/threads/read-me-before-you-post.115/) and also the output of the [diag script](https://forum.sinusbot.com/threads/diagsinusbot-sh-sinusbot-diagnostic-script.831/).

If you used the startscript you can check the status with `systemctl status sinusbot.service`.
Logs can be viewed using `journalctl -u sinusbot.service -f --since "1 hour ago"`.

## Using a startscript

*These instructions need to be done as the `root` user.*

Download the startscript:

```bash
curl -o /lib/systemd/system/sinusbot.service https://raw.githubusercontent.com/SinusBot/linux-startscript/master/sinusbot.service
```

Then edit the file:

```bash
nano /lib/systemd/system/sinusbot.service
```

And replace the following placeholders to match your installation:

| placeholder                    | description                                 | example                |
| ------------------------------ | ------------------------------------------- | ---------------------- |
| YOUR\_USER                     | Your user who starts the bot                | sinusbot               |
| YOURPATH\_TO\_THE\_BOT\_BINARY | Your path to the SinusBot binary            | /opt/sinusbot/sinusbot |
| YOURPATH\_TO\_THE\_BOT         | Your path to the SinusBot install directory | /opt/sinusbot          |

Reload systemd: `systemctl daemon-reload`

Enable autostart (optional): `systemctl enable sinusbot`

Start the sinusbot: `systemctl start sinusbot`

----

Startscript: [github.com/SinusBot/linux-startscript](https://github.com/SinusBot/linux-startscript)
Linux-Installer: [github.com/SinusBot/installer-linux](https://github.com/SinusBot/installer-linux)
