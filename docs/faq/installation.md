### When will feature X be implemented?

There will be **no ETAs** (estimated time of arrival) on any feature. It’s done when it’s done, please don’t ask.

### What is the default username and password?

#### Windows

Double click the SinusBot logo in the tray (next to your clock at the bottom right of the screen) to login. If you need credentials to login from another system, edit the user account or create a new one and set a new password.

#### Linux

Newer releases (0.9.12+) will have **a randomly generated password** which will be displayed on first run. Those versions can have their password overridden by running the bot via

```
./sinusbot --override-password=newpassword
```

(make sure to run as the correct system user). Login as admin with the specified password (newpassword in the example above) and change your password to a new one. Afterwards restart the bot without the pwreset parameter.

For older versions there is no option to reset the password; the only options are to either upgrade or to delete the data-folder which will fully reset the bot.

### Is there a version for 32bit Windows / Linux?

No, there isn’t and there probably won't be one as that would mean much more maintenance work for not that many users.

### I get some message like "ELF: not found" on Linux when trying to start the bot. WTF?

You are trying to run the bot on a 32bit OS. Upgrade your system to 64bit to make the bot work (see above: there’s no 32bit version).
Forums.

### Do you support CentOS, Fedora, (name your distro)…?

Probably. I’ve heard of people running the bot on ArchLinux, CentOS, Fedora and others. Rule of thumb is: if the TS3 Client can run there, the bot usually can as well. However, these distributions have not been officially tested and there’s no documentation available.

### When trying to download the bot, I get errors about SSL. Why and how to fix that?

The whole website now runs on SSL which is far more secure when it comes to software you want to install on your server. However, some linux distributions only have outdated root certificates and those of cloudflare are missing. You can try to upate them via sudo update-ca-certificates on debian/ubuntu.

Otherwise, you can try to use `curl -O https://......`

### When I start the bot from the webinterface, it doesn’t work. It says something about “TS quit” in the log

This can have many reasons. It means that the TeamSpeak client is unable to run or connect to the destination server. You either have not enough free memory, dependencies for the client are missing, or or or. Please search the forum and post your problem along with the log if you cannot find an issue similar to yours.

Here's a quick checklist:

- does your server have enough RAM? At least 200 MB are recommended?
- did you follow the installation guide thoroughly and installed all required dependencies?
- do you run the bot on an officially supported OS? Windows, Debian, Ubuntu are officially supported.
- did you try setting the locale manually like it says in the "Troubleshooting" section of the installation guide?
- did you copy the plugin like it says in the documentation?
- make sure the server exists at the given location
- make sure your client is up to date since older versions might be blocked
- make sure the security level is lower or equal to the clients identity level


### My bot is starting up but playback is not possible / I hear strange things / …! Why?

Make sure you copied the plugin like said in the documentation.

### My bot stutters / lags a lot on Windows. What can I do?

Increase the bots’ priority and also that of the client instances it uses. You can do that within the task manager.
You can also try to decrease the setting SampleInterval, adjusting it to
SampleInterval = 40
in your config.ini.

### Someone told me to fix the file permissions. How do I do that?

Given your bot has been installed in `/opt/sinusbot` and you've added a user sinusbot with the group sinusbot as well, run the following command with root permissions:

```
chown -R sinusbot:sinusbot /opt/sinusbot
```

### I get an error like "what(): locale::facet::_S_create_c_locale name not valid". What do I do?

Example Error:

```
terminate called after throwing an instance of 'std::runtime_error'
what(): locale::facet::_S_create_c_locale name not valid
```

On some minimal installs of Debian or other distributions, the locales are not completely installed / built.
This error can be corrected as follow (**run as root**):

Debian:

```bash
apt-get install locales && dpkg-reconfigure locales
```

Ubuntu:

```bash
apt-get install locales
locale-gen en_US.UTF-8
update-locale LANG=en_US.UTF-8
reboot
```

### What are the requirements for youtube-dl on Linux?

In order to use Youtube-DL on Linux you need Python (Version 2.6, 2.7, 3.3 or later) and optionally the libav-tools.

On Ubuntu / Debian, these packages can be installed as root via:

```
apt-get install python libav-tools
```

### I get an error when starting: Updating database to v7... 6 / Error on database operations: there is already another table or index with this name:

This is a bug in the database upgrade process which happens when you upgrade from <= 0.9.9 to a newer version, go back to <= 0.9.9 and then try to upgrade again (or more likely: when starting the bot via ./ts3bot, even when the newer version ./sinusbot is installed).

To get around this, please carefully do the following:

- stop the bot process completely
- edit your config.ini and add `Pragma = 7` at the top
- start the bot and wait 2-3 minutes
- shut down the bot again
- remove that Pragma entry (this is really important)
- start the bot normally

That should fix it.

### On Windows I get the following error: Error spawning instancefork/exec... WTF?

Most people who see this error have the compatibility mode enabled for either the bot or the TS3 client. Please disable the compatibility mode and try again.

### Could not open /tmp/.sinusbot.lock. Is SinusBot already running?

Remove the file with rm /tmp/.sinusbot.lock and make sure not to run the bot as root.

### Why can't I run the bot as root?

The parameter `-RunningAsRootIsEvilAndIKnowThat` has been disabled as running the bot with the root user is a potential security risk and is generally considered bad practice.
You should always run any program with the least amount of permissions required.

**So how can I run the bot then?**
Start the bot with another user or use a startscipt to run the bot.
You'll have to change the ownership of the entire folder to the new user.

### What does "a manual update is required" mean?

This error message appears when the time of your server is not accurate.
To fix this issue set the correct time and configure ntp to keep it synced properly.