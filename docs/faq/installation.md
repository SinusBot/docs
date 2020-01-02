### When will feature X be implemented?

!!! success ""
    There will be **no ETA** (estimated time of arrival) on any feature. It’s done when it’s done, please don’t ask.

### What is the default username and password?

The default username is `admin`.

???+ info "Windows"
    Double click the SinusBot logo in the tray (next to your clock at the bottom right of the screen) to login. If you need credentials to login from another system, edit the user account or create a new one and set a new password.

???+ info "Linux"
    The bot will initially have a **randomly generated password** which is **displayed on first run** in the console. The sinusbot installer will also print the password at the end of the installation.

    Unexperienced users should use the sinusbot-installer script to reset the password.

    More experienced users can temprorarily override the password and change it by folling these steps:

    1. Stop the sinusbot (ie. `systemctl stop sinusbot`)
    2. Start the sinusbot with the `--override-password=newpassword` flag as the sinusbot user:
        - login as the sinusbot user: `su sinusbot`
        - go to the sinusbot directory: `cd /opt/sinusbot`
        - start the sinusbot: `./sinusbot --override-password=newpassword` (**don't** do this as root!)
    3. Login as `admin` with the specified password (ie. `newpassword`) and change your password to a new one.
    4. Stop the sinusbot: ++ctrl+c++
    5. Afterwards restart the sinusbot *without* the `--override-password` parameter. (ie. `systemctl start sinusbot`)

    If the sinusbot doesn't start afterwards and you get something like

        Job for sinusbot.service failed because the control process exited with error code.
        See "systemctl status sinusbot.service" and "journalctl -xe" for details.

    then you did something wrong, such as: starting the bot as root or not stopping the bot, ...

    Look at the sinusbot log (as it says) with `journalctl -xe` and search for a solution on this FAQ page or in the forum.

### Is there a version for 32bit Windows / Linux? { #32bit data-toc-label='Is there a 32bit version?' }

!!! success ""
    No, there isn’t and there probably won't be one as that would mean much more maintenance work for not that many users.

### I get some message like "ELF: not found" on Linux when trying to start the bot. WTF? { #elf-not-found data-toc-label='Error: ELF: not found' }

!!! success ""
    You are trying to run the bot on a 32bit OS. Upgrade your system to 64bit to make the bot work (see above: there’s no 32bit version).

### Do you support CentOS, Fedora, (name your distro)…? { #distro-support data-toc-label='Supported Distros' }

!!! success ""
    Probably. I’ve heard of people running the bot on ArchLinux, CentOS, Fedora and others. Rule of thumb is: if the TS3 Client can run there, the bot usually can as well. However, these distributions have not been officially tested and there’s no documentation available.

    We provide documentation and support for the latest LTS releases of Debian and Ubuntu.

### When trying to download the bot, I get errors about SSL. Why and how to fix that? { #ssl-errors-on-download data-toc-label='SSL errors on download' }

!!! success ""
    The whole website now runs on SSL which is far more secure when it comes to software you want to install on your server. However, some linux distributions only have outdated root certificates and those of cloudflare are missing. You can try to upate them via `sudo update-ca-certificates` on debian/ubuntu.

    Otherwise, you can try to use `curl -O https://...`

### When I start the bot from the webinterface, it doesn’t work. It says something about “TSClient quit.” in the log { #ts-client-quit data-toc-label='Error: TSClient quit.' }

!!! success ""
    This can have many reasons. It means that the TeamSpeak client is unable to run or connect to the destination server. You either have not enough free memory, dependencies for the client are missing, or or or. Please search the forum and post your problem along with the log if you cannot find an issue similar to yours.

    Here's a quick checklist:

    - does your server have enough RAM? (at least 300 MB are recommended)
    - did you follow the installation guide thoroughly and installed all required dependencies?
    - do you run the bot on an officially supported OS? Windows, Debian, Ubuntu are officially supported.
    - did you try setting the locale manually like it says in the "Troubleshooting" section of the installation guide?
    - did you copy the plugin like it says in the documentation?
    - make sure the server ip/adress is correct
    - make sure your client is up to date since older versions might be blocked
    - make sure the security level is lower or equal to the clients identity level

### My bot stutters / lags a lot on Windows. What can I do? { #lags-on-windows data-toc-label='Lags on Windows' }

!!! success ""
    Increase the bots’ priority and also that of the client instances it uses. You can do that within the task manager.
    You can also try to decrease the setting SampleInterval, adjusting it to `SampleInterval = 40` in your config.ini.

### Someone told me to fix the file permissions. How do I do that? { #fix-file-permissions data-toc-label='Fix File Permissions' }

!!! success ""
    Given your bot has been installed in `/opt/sinusbot` and you've added a user sinusbot with the group sinusbot as well, run the following command with root permissions:

        chown -R sinusbot:sinusbot /opt/sinusbot

### I get an error like "what(): locale::facet::_S_create_c_locale name not valid". What do I do? { #missing-locales data-toc-label='Error: c locale name not valid' }

!!! success ""
    Example Error:

        terminate called after throwing an instance of 'std::runtime_error'
        what(): locale::facet::_S_create_c_locale name not valid

    On some minimal installs of Debian or other distributions, the locales are not completely installed / built.
    This error can be corrected as follow (**run as root**):

    Debian:

        apt-get install locales
        dpkg-reconfigure locales

    Ubuntu:

        apt-get install locales
        locale-gen en_US.UTF-8
        update-locale LANG=en_US.UTF-8
        reboot

### I get an error when starting: Updating database to v7... 6 / Error on database operations: there is already another table or index with this name: { #database-errors data-toc-label='Error on database operations' }

!!! success ""
    This is a bug in the database upgrade process which happens when you upgrade from <= 0.9.9 to a newer version, go back to <= 0.9.9 and then try to upgrade again (or more likely: when starting the bot via ./ts3bot, even when the newer version ./sinusbot is installed).

    To get around this, please carefully do the following:

    - stop the bot process completely
    - edit your config.ini and add `Pragma = 7` at the top
    - start the bot and wait 2-3 minutes
    - shut down the bot again
    - remove that Pragma entry (this is really important)
    - start the bot normally

    That should fix it.

### On Windows I get the following error: Error spawning instancefork/exec... WTF? { #error-spawning-instancefork-exec data-toc-label='Error spawning instancefork/exec' }

!!! success ""
    Most people who see this error have the compatibility mode enabled for either the bot or the TS3 client. Please disable the compatibility mode and try again.

### Could not open /tmp/.sinusbot.lock. Is SinusBot already running?

!!! success ""
    Remove the file with `rm /tmp/.sinusbot.lock` and make sure **not** to run the bot as root.

### Why can't I run the bot as root?

!!! success ""
    Unnecessarily running software with the root user is a potential security risk and is generally considered bad practice.

    You should always run any program with the least amount of permissions required.

    **So how can I run the bot then?**

    Start the bot with another user or [use a startscipt](../../installation/linux/#using-a-startscript) to run the bot.
    You'll have to [change the ownership](#fix-file-permissions) of the entire folder to the new user.

### What does "a manual update is required" mean?

!!! success ""
    This error message appears when the time of your server is not accurate.
    To fix this issue set the correct time and configure ntp to keep it synced properly.


### What does "could not contact update server" mean?

!!! success ""
    This error message appears when the SinusBot is unable to contact our update servers.

    Possible causes:

    - no internet connection / invalid network configuration
    - cloudflare is showing a captcha page because your IP is marked as shady
    - your IP is blacklisted due to suspected non-private use
        - you are only allowed to run **one** SinusBot and **commercial/non-private use is not allowed** without prior, written consent by the author. If you need more instances then [get a license](https://sinusbot.github.io/docs/licenses/).
        - if you decide to contact us: please be polite, explain the situation in detail and provide your IP address
        - there is no point in lying, if you are not honest then we are not interested in talking to you

    Please check `curl -v --no-keepalive --http1.1 https://update01.sinusbot.com`.<br>
    If it returns a 404 (`< HTTP/1.1 404 Not Found`) then cloudflare should not be the issue.<br>
    If it returns a 403 (`< HTTP/1.1 403`) and HTML code with a captcha then cloudflare requires you to solve the captcha because your IP address is not trusted. Before you ask: No, we can't whitelist your IP from cloudflare.
