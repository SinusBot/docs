It's recommend to modify the sinusbot config in two ways:

  - Set the `ListenHost` to `localhost` or `127.0.0.1` as the Sinusbot is now only meant to be accessed via the reverse proxy.
  - Set `IsProxied` to `true` so that the Sinusbot knows that the Webinterface is reverse proxied and will handle the IPs correctly.