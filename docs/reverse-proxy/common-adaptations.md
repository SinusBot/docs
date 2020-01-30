It's recommend to modify the sinusbot's `config.ini` in two ways:

- Set the `ListenHost` to `localhost` or `127.0.0.1` as the Sinusbot is now only meant to be accessed via the reverse proxy.
- Set `IsProxied` to `true` so that the Sinusbot knows that the web-interface is behind a reverse proxy and will handle the IPs correctly.