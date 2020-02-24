## Requirements

!!! Warning "The TeamSpeak Client 3.3+ requires at least a Linux Kernel of version 3.17 or higher!"
    You can check your Linux Kernel version with `uname -a`.

Make sure that your OS (Operating System) is up-to-date.
We recommend recent LTS releases such as **Ubuntu 18.04** or **Debian 10** (buster), minimal required versions:

- Debian 8+
- Ubuntu 16.10+
- CentOS 7+

When choosing a VPS (virtual private server), make sure that it is **not** based on OpenVZ, because the Linux kernel will be too old. Instead choose a **KVM** or **LCX** based VPS with a recent OS.

The server should have *at least* 512MB or 1GB of free RAM.
Although the SinusBot itself doesn't require much RAM, the TeamSpeak Client(s) often take up the most memory.

Make sure that the server has enough free disk space to fit your needs.

#### Compatible Versions

SinusBot Version         | TS3 Client Version  | Linux Kernel Version
-------------------------|---------------------|---------------------
1.0.0-beta3 and later    | 3.3+                | 3.17+
1.0.0-beta2, 1.0.0-beta1 | 3.2.5               | 2.6+

Please note that we do not support old beta releases. See [Support Policy / Support Grundregeln](https://sinusbot.github.io/docs/faq/general/#support-policy).

## Installer Script

If you are new to Linux and/or wish to have everything installed for you in a more convenient way, we encourage you to use the [Installer Script](https://sinusbot.github.io/installer/).

## Manual installation

!!! Warning "The TeamSpeak Client 3.3+ requires at least a Linux Kernel of version 3.17 or higher!"
    You can check your Linux Kernel version with `uname -a`.

Let's start by installing several dependencies:

```bash
apt-get update
apt-get install -y x11vnc xvfb libxcursor1 ca-certificates curl bzip2 libnss3 libegl1-mesa x11-xkb-utils libasound2 libpci3 libxslt1.1 libxkbcommon0 libxss1 libxcomposite1
update-ca-certificates
```

On Debian and some Ubuntu versions you might as well have to install, so at least try:

```bash
apt-get install libglib2.0-0
```

**In case of Ubuntu 18.04**: Depending on the Ubuntu installation the `universe` repository of Ubuntu is not activated, resulting in missing packages for required dependencies *x11vnc* and *xvfb*. When said problem occurs, enable the `universe` repository by using following command:

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
# create folder
mkdir -p /opt/sinusbot
# grant sinusbot user permissions on specified folder
chown -R sinusbot:sinusbot /opt/sinusbot
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
# set the current/supported TS3 version here
VERSION="3.3.2"
wget https://files.teamspeak-services.com/releases/client/$VERSION/TeamSpeak3-Client-linux_amd64-$VERSION.run
chmod 0755 TeamSpeak3-Client-linux_amd64-$VERSION.run
./TeamSpeak3-Client-linux_amd64-$VERSION.run
```

You will need to accept the terms by pressing: ++enter++, ++q++, ++y++, ++enter++.

Afterwards you can delete the file: `rm TeamSpeak3-Client-linux_amd64-$VERSION.run`

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

!!! Info "If you want to keep the bot running when you exit out of the terminal follow the instruction on how to [install a startscript](#using_a_startscript)."

Now login at `http://<your ip>:8087/` with user **admin** and the password provided on first run. (see [FAQ](https://sinusbot.github.io/docs/faq/installation/#what-is-the-default-username-and-password) on how to reset)

### Using a startscript

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


### Update

#### Update the SinusBot

*Note: The following instructions assume that you've followed this guide - otherwise you might need to slightly adapt the commands to fit your installation.*

Before continuing you should install the dependencies mentioned at the beginning of the "Manual installation" section.

The update process is the same as the installation, we simply download and unpack the new SinusBot version over the old one.

First stop your sinusbot (e.g. `systemctl stop sinusbot` if you use the systemd-startscript) and then run the following commands:

```bash
# go into the sinusbot directory
cd /opt/sinusbot
# download the current release
wget https://www.sinusbot.com/dl/sinusbot.current.tar.bz2
# unpack it
tar -xjvf sinusbot.current.tar.bz2
# copy the plugin
cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/
# fix the file permissions if you're doing this as root
chown -R sinusbot:sinusbot /opt/sinusbot
```

#### Update the TeamSpeak Client

Before continuing you should install the dependencies mentioned at the beginning of the "Manual installation" section.

The update process is the same as the installation, we simply download and unpack the new TeamSpeak Client over the old one.

```bash
# set the current/supported TS3 version here
VERSION="3.3.2"
wget https://files.teamspeak-services.com/releases/client/$VERSION/TeamSpeak3-Client-linux_amd64-$VERSION.run
chmod 0755 TeamSpeak3-Client-linux_amd64-$VERSION.run
./TeamSpeak3-Client-linux_amd64-$VERSION.run
```

You will need to accept the terms by pressing: ++enter++, ++q++, ++y++, ++enter++.

Afterwards you can delete the file: `rm TeamSpeak3-Client-linux_amd64-$VERSION.run`

Now remove the `data/ts3` directory and the `libqxcb-glx-integration.so` file as well:

```bash
rm -rf data/ts3
rm TeamSpeak3-Client-linux_amd64/xcbglintegrations/libqxcb-glx-integration.so
```

And finally copy the plugin to the plugins-directory of the TeamSpeak-Installation

```bash
cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/
# fix the file permissions if you're doing this as root
chown -R sinusbot:sinusbot /opt/sinusbot
```

### Migrating to another System

First, install the SinusBot on the new system according to our guides.
Afterwards, copy over the `data`-folder, `scripts`-folder, `config.ini` and `private.dat` from your old SinusBot installation folder (typically `/opt/sinusbot/` on Linux).

Depending on how you copied the files, you might need to [fix your file permissions](https://sinusbot.github.io/docs/faq/installation/#fix-file-permissions) afterwards.

When finished, stop the SinusBot on the old system (e.g.`systemctl stop sinusbot`) and (re)start the SinusBot on the new system (e.g.`systemctl restart sinusbot`).

## Troubleshooting

Look for any errors in the sinusbot/instance log and try to look-up solutions on our [forum](https://forum.sinusbot.com/) or your favorite search engine.

If you ask us or our community for help then please provide the output of the [diag script](https://forum.sinusbot.com/threads/diagsinusbot-sh-sinusbot-diagnostic-script.831/) and follow everything that is mentioned in [READ ME BEFORE YOU POST](https://forum.sinusbot.com/threads/read-me-before-you-post.115/).

If you use the systemd-startscript you can check the status with `systemctl status sinusbot`.
Logs can be viewed using `journalctl -u sinusbot -f --since "2 hours ago"`.

----

The SinusBot itself is closed-source, but some of the resources are open-source and available in the [SinusBot GitHub Organization](https://github.com/SinusBot) - contributions welcome.

- [Documentation](https://github.com/SinusBot/docs)
- [Linux-Installer](https://github.com/SinusBot/installer-linux)
- [Startscript](https://github.com/SinusBot/linux-startscript)
- and more!
