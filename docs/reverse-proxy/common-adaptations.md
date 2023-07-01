It's recommend to modify the sinusbot's `config.ini`:

- Set the `ListenHost` to `localhost` or `127.0.0.1` as the SinusBot is now only meant to be accessed via the reverse proxy.
- Set `IsProxied` to `true` so that the SinusBot knows that the web-interface is behind a reverse proxy and will handle the IPs correctly.
- Set the `Hostname` to your public domain you've set up.