# Configuration

Usually you don't need to edit too much in the config file as most of the important stuff can be managed via the web interface. Some functionality however can be enabled or tweaked in here. Please be careful with the settings and should you encounter problems, always make sure that you tell us what you changed in here!

### General

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| EnableDebugConsole | (internal use only)                                                            | true                       |
| EnableLocalFS      | (internal use only)                                                            | false                      |
| EnableProfiler     | (internal use only; deprecated)                                                | false                      |
| EnableWebStream    | allow the bot to export the audiostream via http or icecast                    | false                      |
| ExternalFileBase   | a path where an external music library is stored                               |                            |
| DataDir            | This can be used to specify the data directory the bot should use.             | ./data inside the bot root |
| Hostname           | Hostname to use for the certificate when UseSSL is enabled                     |                            |
| InstanceActionLimit| number of http requests / actions (per instance and second) before a limit will prevent further actions | 6 |
| IsProxied          | if enabled, the bot will trust proxied headers and use the ips from there      | false                      |
| License            | one or more valid licenses                                                     |                            |
| LicenseKey         | hostspecific license key; used for license-requests. Don't change it!          |                            |
| ListenHost         | IP-address the bot should listen on                  | 0.0.0.0 (will listen on all interfaces/IP-addresses) |
| ListenPort         | Port the bot should listen on                        | 8087  |
| LocalPlayback      | (internal use only)                                  | false |
| LogFile            | if specified, output will be logged to this file instead of stdout | |
| MaxBulkOperations  | number of entries that can be moved with one operation (add to playlist, move to folder and such) | 300 |
| LogLevel           | verbosity of the log                                      | 3 (errors and warnings) |
| Pragma             | (caution!) used to override database version; DO NOT SET! | |
| RunAsGroup         | gid to use for privilege drop          | 0 |
| RunAsUser          | uid to use for privilege drop          | 0 |
| SampleInterval     | `DON'T TOUCH, WILL BREAK THINGS!`      | |
| SSLCertFile        | certificate to use for SSL connections | |
| SSLKeyFile         | private key to use for SSL connections | |
| Token              | random security token, generated on first start; to change, remove it | |
| TS3Path            | Path to the TeamSpeak 3 Client executable | |
| UploadLimit        | maximum number of bytes a file is allowed to have when uploading | 83886080 (80M) |
| UseSSL             | if set to true, the bot will only accept https-connections; Hostname MUST be specified | false |
| YoutubeDLPath      | Path the the youtube-dl executable | youtube-dl |

### TS3

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| AvatarMaxWidth     | if set, all uploaded avatars will be limited (resized) to this value | 0 (no limit) | 
| AvatarMaxHeight    | if set, all uploaded avatars will be limited (resized) to this value | 0 (no limit) |
| AllowGIF           | allows avatar to be a GIF                                            |              |

### YoutubeDL

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| BufferSize                    | number of bytes to use for buffering (useful to tune on slow connections)   |            |
| CacheStreamed                 | if streaming via ytdl, enabling this will cause the streams to get stored inside the cache directory; please be aware that you have to delete the cache files manually (that's safe to do) |            |
| ChunkSize                     | Size in bytes that will determine count of simultaneous download streams (limited by MaxSimultaneousChunkDownloads) | 3 MB        |
| MaxDownloadSize               | maximum size of files to download via ytdl                                  |            |
| MaxDownloadRate               | if you want to slow down ytdl to prevent traffic spikes, use this           |            |
| MaxSimultaneousChunkDownloads | overall limit of simultaneous download streams per job                      | 10         |
| TimeoutMultiDownloader        | timeout (in seconds) for chunks of a multi stream download                  | 5 Minutes  |
| TimeoutSingleDownloader       | time (in seconds) before a downloader cancels                               | 30 Minutes |

### Plugins

This section will hold configuration values for used plugins. Please see the manual of the plugin to use for what settings are required.

### Scripts

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| AllowReload        | Enables a script function that allows hot script reloading (added scripts will still need a restart of the bot) |
| DevMode            | If set to true (default is false), all scripts will be reloaded once a script file gets changed. |

### SpeechRecognition

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| Enable             | Enable speech recognition; requires additional files to work |

### XServer

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| Delay              | Throttle XServer events to save CPU cycles (DON'T CHANGE) | 0       |
| Debug              | (internal only)                                           | false   |

### DAV (deprecated)

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| Enable             | Enables serving the music files via DAV backend; experimental; deprecated | false   |

### FFmpeg

| Field              | Value                                                                          | Default                    |
| ------------------ | ------------------------------------------------------------------------------ | -------------------------- |
| UserAgent          | Can be used to replace the default user-agent header FFmpeg uses |
