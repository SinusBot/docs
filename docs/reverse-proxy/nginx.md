If you want to serve the web interface of the SinusBot encrypted or with the rest of your website, you usually want to setup a reverse proxy. Most of the time, you already have a web server (like Apache2 or nginx) in place, which you can use to forward the incoming traffic to the SinusBot.

First you need to add a DNS record (for example an A-record) that points from your subdomain (e.g. sinusbot) to the IP of your server.

After that, create a file at `/etc/nginx/sites-available/sinusbot.conf` with the following content.

You need to adjust the value of the following variables in the configuration examples below:

- `server_name` (domain/subdomain)
- `proxy_pass` (local address of your sinusbot)
- `ssl_certificate` (SSL only)
- `ssl_certificate_key` (SSL only)

If you are using no SSL (http):

<!-- TODO: check if websockets work -->

```nginx
server {
    listen 80;
    listen [::]:80;
    
    # Set your domain here:
    server_name sinusbot.example.com;

    client_max_body_size 200M;
    
    access_log  /var/log/nginx/sinusbot.access.log;
    error_log   /var/log/nginx/sinusbot.error.log;
    
    location / {
        proxy_pass http://127.0.0.1:8087;
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $remote_addr;

        # pass upgrade/connection headers for websockets
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
    }
}
```

If you are using SSL (https) with http->https redirect:

```nginx
server {
    listen 80;
    listen [::]:80;
    
    # Set your domain here:
    server_name sinusbot.example.com;
    
    access_log /var/log/nginx/sinusbot.access.log;
    error_log  /var/log/nginx/sinusbot.error.log;
    
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    
    # Set your domain here:
    server_name sinusbot.example.com;
    
    client_max_body_size 200M;
    
    access_log /var/log/nginx/sinusbot.access.log;
    error_log  /var/log/nginx/sinusbot.error.log;
    
    # Set the path to your ssl cert here:
    ssl on;
    ssl_certificate     /opt/ssl/fullchain.pem;
    ssl_certificate_key /opt/ssl/privkey.pem;
    
    location / {
        proxy_pass http://127.0.0.1:8087;
        proxy_http_version 1.1;
        proxy_set_header X-Forwarded-For $remote_addr;

        # pass upgrade/connection headers for websockets
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
    }
}
```

Afterwards you need to link the file to the `sites-enabled` directory:

`ln -sf /etc/nginx/sites-available/sinusbot.conf /etc/nginx/sites-enabled`

Check for errors:

`nginx -t`

Reload nginx:

`nginx -s reload`

Now just follow the [common adaptations](common-adaptations.md) for reverse proxies.
