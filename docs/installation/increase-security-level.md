# How to increase TeamSpeak security level

Open your SinusBot web-interface and go to: Settings ⇒ Instance Settings

![Instance Settings](incr01_instance_settings.png)

Click in the text filed labeled "Identity", Select All ++ctrl+a++, Copy ++ctrl+c++

![Identity text field](incr02_identity.png)

Open a text editor such as notepad and insert the following:

```ini
[Identity]
id=SinusBot Identity 
identity="<IDENTITY_STRING>"
nickname=SinusBot
phonetic_nickname=
```

Replace `<IDENTITY_STRING>` with the identity string you copied (ends with an `=`).

Save the file as `sinusbot_identity.ini` ++ctrl+s++ (select "All Files") on your desktop and close the editor.

![Notepad Save Dialog](incr03_notepad.png)

Start your TeamSpeak client and open the "Identities" menu ++ctrl+i++

![TS3 Client Identities Menu](incr04_ts3.png)

Right-click in the "Local Identities" field and select "Import".

![Context-menu: Import](incr05_identities.png)

Select the previously created file `sinusbot_identity.ini`.

![Import: Open File Dialog](incr06_import.png)

Click on "Go Advanced" if you are still in the "Basic" mode.

![Go Advanced](incr07_advanced.png)

Click on "Improve", then enter your "Requested Security Level" and click on "Start".

![Improve](incr08_improve.png)

When finished click "Close" and then right-click in the SinusBot Identity and select "Export".

![Export](incr09_export.png)

![Warning](incr10_warning.png)

Overwrite the previously created file `sinusbot_identity.ini`.

![Save Dialog](incr11_save.png)

Open the file again and copy the new identity string (ends with an `=`).

![Copy identity string](incr12_copy.png)

Stop your SinusBot instance (the button at the top should be orange/red).

![Stop Button](incr13_stop.png)

Delete the old identity string ++ctrl+a++ ++del++ and insert the new one ++ctrl+v++.

![Identity String](incr14_insert.png)

Now click on "Save changes" to apply your changes. If you followed these steps correctly the new security level will appear.

![Save](incr15_save.png)

Now you can start your SinusBot instance again.
