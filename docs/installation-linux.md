## Installation Linux (Ubuntu / Debian)

**If you are new to Linux and/or wish to have everything installed for you in a more convenient way, we encourage you to use the [Install Script](https://forum.sinusbot.com/resources/sinusbot-installer-script.58/).**

Let's start by installing several dependencies:

	apt-get update
	apt-get install -y x11vnc xvfb libxcursor1 ca-certificates bzip2 libnss3 libegl1-mesa x11-xkb-utils libasound2
	update-ca-certificates

On Debian and some Ubuntu versions you might as well have to install, so at least try

	apt-get install libglib2.0-0

**In case of Ubuntu 18.04**: Depending on the Ubuntu installation the `universe` repository of Ubuntu is not activated, resulting in missing packages for required dependencies *x11vnc* and *xvfb*. When said problem ocurrs, enable the `universe` repository by using following command:

	add-apt-repository universe
	apt-get update

After all required dependencies are installed, let's assume that you're going to install the bot to `/opt/sinusbot` and are using the user `sinusbot` with the group `sinusbot`. We will install the bot with root then switch to this user account when running the bot.

You will need to create an new user `sinusbot` on your server, so to do so type the following command.

	adduser --disabled-login sinusbot

This created user is used to start the bot with usual user privileges (which is highly recommended!), as the bot should **not** run as root for security-reasons.

Next we will create and prepare the folder where Sinusbot will be installed to, by issuing following commands as the root user:

	mkdir -p /opt/sinusbot # create folder
	chown -R sinusbot:sinusbot /opt/sinusbot # grant sinusbot user permissions on specified folder

(If you're using another user/group than "sinusbot", replace sinusbot:sinusbot with **yourusername:yourusergroup**)

Then we will switch over to the recently created user dedicated for the sinusbot, change the working directory and to download the latest Sinusbot release:

	su sinusbot
	cd /opt/sinusbot
	wget https://www.sinusbot.com/dl/sinusbot.current.tar.bz2

If that command results in SSL-Errors, you can **alternatively** try

	curl -O https://www.sinusbot.com/dl/sinusbot.current.tar.bz2

Next, extract the bot:

	tar -xjf sinusbot.current.tar.bz2

Copy the configuration (if you haven't started the bot before)

	cp config.ini.dist config.ini

Now you need to download the TeamSpeak 3 Client and **install it**.

	wget http://dl.4players.de/ts/releases/3.2.3/TeamSpeak3-Client-linux_amd64-3.2.3.run
	chmod 0755 TeamSpeak3-Client-linux_amd64-3.2.3.run
	./TeamSpeak3-Client-linux_amd64-3.2.3.run

You will need to accept the terms.
You do this by pressing enter to scroll through the text or press q to simply go to the end.

Now you need to configure the ini-File of the bot to match your directories.

	nano config.ini

Make sure that the TS3Path is correct (if you followed this tutorial step by step, it should already match):

	TS3Path = "/opt/sinusbot/TeamSpeak3-Client-linux_amd64/ts3client_linux_amd64"

Close the editor (Ctrl+O, Enter, Ctrl+X).

Remove the file 'libqxcb-glx-integration.so' from the clients 'xcbglintegrations' directory:

	rm TeamSpeak3-Client-linux_amd64/xcbglintegrations/libqxcb-glx-integration.so

Create the plugins folder in the ts3client directory:

	mkdir TeamSpeak3-Client-linux_amd64/plugins

And finally copy the plugin to the plugins-directory of the TeamSpeak-Installation

	cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/

Just to make sure that the bot is executable, enter

	chmod 755 sinusbot

### Update

(This instructions needs to be done using the sinusbot user.)

Make sure you're using the latest version:

	cd /opt/sinusbot
	wget https://www.sinusbot.com/dl/sinusbot.current.tar.bz2
	tar -xjvf sinusbot.current.tar.bz2
	cp plugin/libsoundbot_plugin.so TeamSpeak3-Client-linux_amd64/plugins/

If you are updating from `3.X` to `3.1.X` then you need to remove the `data/ts3` directory and the `libqxcb-glx-integration.so` file as well:

	rm -rf data/ts3
	rm TeamSpeak3-Client-linux_amd64/xcbglintegrations/libqxcb-glx-integration.so

### Usage

As [the bot won't run as root](https://forum.sinusbot.com/kb/why-cant-i-run-the-bot-as-root.201) you will need to switch to the user that you have installed the bot on, if you followed the tutorial, this will be 'sinusbot". To do this use the following command:


	su sinusbot

Starting the bot

	./sinusbot

Stopping the bot

	Ctrl + C

**If you want to keep the bot running when you exit out of the terminal follow the instruction on how to [install a startscript](#using_a_startscript).**

Now login at `http://<your ip>:8087/` with user **admin** and the password provided on first run. (see [FAQ](https://forum.sinusbot.com/faq/what-is-the-default-username-and-password.2/) on how to reset)

## Troubleshooting

If the bot doesn't connect and you only see a "INFO TSClient quit" every time you try to start the bot **via the webinterface**, you might need to set your locale info manually when starting up the bot. Try to start it with

	LC_ALL="en_US.UTF-8" ./sinusbot

Exchange **en_US.UTF-8** to whatever locale you're using.

If that still doesn't help, try to manually start a TS client instance and see if that reports something useful:

	xinit /opt/sinusbot/TeamSpeak3-Client-linux_amd64/ts3client_linux_amd64 -- /usr/bin/Xvfb :1 -screen 0 800x600x16 -ac

If you used the startscript check the status by `systemctl status sinusbot.service`. Other logs from the stdout you can see by using ` journalctl -u sinusbot.service --since "1 hour ago"`.

## Using a startscript

(This instructions needs to be done using the `root` user.)  
Either download it directly with `curl -o /lib/systemd/system/sinusbot.service https://raw.githubusercontent.com/SinusBot/linux-startscript/master/sinusbot.service`
or create a file at `/lib/systemd/system/sinusbot.service` with the following content:

```ini
[Unit]
Description=Sinusbot, the Teamspeak 3 and Discord music bot.
Wants=network-online.target
After=syslog.target network.target network-online.target

[Service]
User=YOUR_USER
ExecStartPre=/bin/rm -f /tmp/.sinusbot.lock
ExecStopPost=/bin/rm -f /tmp/.sinusbot.lock
ExecStart=YOUR_PATH_TO_THE_BOT_BINARY
WorkingDirectory=YOUR_PATH_TO_THE_BOT
Type=simple
KillSignal=2
SendSIGKILL=yes
Environment=QT_XCB_GL_INTEGRATION=none
LimitNOFILE=512000
LimitNPROC=512000

[Install]
WantedBy=multi-user.target
```

Adjust the following placeholders to your installation:

| placeholder                      | description                                 | example                |
| --- | --- | --- |
| YOUR\_USER                       | Your user who starts the bot                | sinusbot               |
| YOUR\_PATH\_TO\_THE\_BOT\_BINARY | Your path to the SinusBot binary            | /opt/sinusbot/sinusbot |
| YOUR\_PATH\_TO\_THE\_BOT          | Your path to the SinusBot install directory | /opt/sinusbot          |

Reload systemd: `systemctl daemon-reload`

Enable autostart (optional): `systemctl enable sinusbot`

Start the sinusbot: `systemctl start sinusbot`

----

[github.com/SinusBot/linux-startscript](https://github.com/SinusBot/linux-startscript)