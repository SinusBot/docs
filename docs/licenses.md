# Licenses

!!! warning "Please note the following restrictions"
    Licenses are **only** available **for the Linux version** of the bot.<br/>
    Licenses are **only** available **for TeamSpeak** and not Discord.<br/>
    Private use only, see [Disclaimer](#disclaimer).

So you own a large server and two instances are not enough for you? For this case we're handing out free extended licenses which come with 4 more instances by default, so you've got a total of 6.

## How to get a free extended license?

We issue approx. one of those licenses per day (that's about 30 per month) but as this is a manual process, we do it in batches every couple of days. You can apply for such a license (if one is available) at our [License Page](https://forum.sinusbot.com/license). If you've successfully committed the request, your license will be issued with the next batch. Please make sure to input the correct information as you would have to request a new license otherwise.

## But all free licenses have been taken. Is there another way to obtain one?

We do have a "Donor" group on our forums that you will get automatically if you [donate](https://forum.sinusbot.com/account/upgrades). With this group, the [License Page](https://forum.sinusbot.com/license) will directly be open to you and you can request a license right away. However, please be aware that your license will not be issued directly but with the next batch (see above).

## How long does it take for the license to be approved?

As mentioned above, licenses are done in batches every couple of days. It usually takes between two days and one week.

## How long is such a license valid?

A license will also be valid for at least a major release (e.g. 2.0 could require a new license compared to 1.0). We currently don't have plans to invalidate any license given out before 1.0 with the release of 1.0.

Licenses are **not** bound to the TeamSpeak-Server UID nor the IP address anymore; the license is still valid even if they change.

## How do I install the license?

Once you've received a license you just have to download the `private.dat` file from the [License Page](https://forum.sinusbot.com/license) and save/copy it into the same folder the bot is installed in (normally that should be in `/opt/sinusbot/`).
After restarting the SinusBot the new instances will appear automatically.

If no instances appear afterwards then you did something wrong.
Make sure that...

- `private.dat` is in the directory where the SinusBot is installed (typically `/opt/sinusbot/` if you followed our guide or used the installer)
- `private.dat` is owned and readable by the SinusBot user (`chown sinusbot:sinusbot /opt/sinusbot/private.dat`)
- `private.dat` was uploaded correctly

## Disclaimer

Every request will be checked manually and we reserve the right to deny requests without further notice (e.g. in case of abuse). We also reserve the right to discontinue this service or change the terms at any time.

Whether you use a SinusBot license or not, the license agreement applies in any case (see `Settings -> Info -> About` in your SinusBot web-interface).

!!! warning "You may NOT redistribute this software or use this software commercially without prior written permission from the author. See [FAQ](https://sinusbot.github.io/docs/faq/general/#commercial-use) for more information."
