If you want to serve the web interface of the SinusBot encrypted or with the rest of your website, you usually want to setup a reverse proxy. Most of the time, you already have a webserver (like Apache2 or nginx) in place, which you can use to forward the incoming traffic to the SinusBot.

## Using nginx as a reverse proxy

First you need to add a DNS record (for example an A-record) that points from your subdomain (e.g. sinusbot) to the IP of your server.

After that, create a file at `/etc/nginx/sites-available/sinusbot.conf` with the following content.

In the config files below you need to adjust the value of the following variables:

- `server_name` (domain/subdomain)
- `proxy_pass` (local address of your sinusbot)
- `ssl_certificate` (SSL only)
- `ssl_certificate_key` (SSL only)

If you are using no SSL (http):

```
server {
    listen 80;
    listen [::]:80;
    
    # Set your domain here:
    server_name sinusbot.example.com;
    client_max_body_size 200M;
    
    access_log  /var/log/nginx/sinusbot.access.log;
    error_log   /var/log/nginx/sinusbot.error.log;
    
    location / {
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_pass http://127.0.0.1:8087;
    }
}
```
If you are using SSL (https) with http->https redirect:
```
server {
    listen 80;
    listen [::]:80;
    
    # Set your domain here:
    server_name sinusbot.example.com;
    
    access_log  /var/log/nginx/sinusbot.access.log;
    error_log   /var/log/nginx/sinusbot.error.log;
    
    return 301 https://$host$request_uri;
}
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    
    # Set your domain here:
    server_name sinusbot.example.com;
    client_max_body_size 200M;
    
    access_log  /var/log/nginx/sinusbot.access.log;
    error_log   /var/log/nginx/sinusbot.error.log;
    
    # Set the path to your ssl cert here:
    ssl on;
    ssl_certificate /opt/ssl/fullchain.pem;
    ssl_certificate_key /opt/ssl/privkey.pem;
    
    location / {
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_pass http://127.0.0.1:8087;
    }
}

```
Afterwards you need to link the file to the `sites-enabled` directory:

`ln -sf /etc/nginx/sites-available/sinusbot.conf /etc/nginx/sites-enabled`

Check for errors:

`nginx -t`

Reload nginx:

`nginx -s reload`

Now just follow [[en:guides:installation:reverse-proxy:common-adaptations|this]].

## Using Apache 2 as a reverse proxy

First you need to add a DNS record (A) which is pointing from your subdomain (e.g. bot) to the IP of your server. After that, create a file at `/etc/apache2/sites-available/sinusbot.conf` with the following content.

In the config files in the buttom you need to adjust the value of the following variables:

- `ServerName`
- `ProxyPass` and `ProxyPassReverse` (port of your sinusbot)
- `SSLCertificate*` (SSL only!)

If you are using no SSL (http):
```
<VirtualHost *:80>
    ServerName bot.example.tld
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    ProxyPreserveHost On

    ProxyPass / http://127.0.0.1:8087/
    ProxyPassReverse / http://127.0.0.1:8087/

</VirtualHost>
```
If you are using SSL (https) with http->https redirect:
```
<VirtualHost *:80>
    ServerName bot.example.tld
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    RewriteEngine on
    RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]

</VirtualHost>

<VirtualHost *:443>
    ServerName bot.example.tld
    
    SSLEngine On
    SSLCertificateFile    /opt/ssl/cert.pem
    SSLCertificateKeyFile /opt/ssl/privkey.pem
    SSLCertificateChainFile /opt/ssl/fullchain.pem
    
    ProxyPass / http://127.0.0.1:8087/
    ProxyPassReverse / http://127.0.0.1:8087/
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

```
Afterwards you need to link the file to the `sites-enabled` directory:

`ln -sf /etc/apache2/sites-available/sinusbot.conf /etc/apache2/sites-enabled`

Enable the proxy-module:

`a2enmod proxy`

Enable the http-proxy-module:

`a2enmod proxy_http`

Enable the ssl-module

`a2enmod ssl`

Enable the rewrite-module:

`a2enmod rewrite`

Restart apache2:

`systemctl restart apache2`

Now just follow [[en:guides:installation:reverse-proxy:common-adaptations|this]].
