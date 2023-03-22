If you want to serve the web interface of the SinusBot encrypted or with the rest of your website, you usually want to setup a reverse proxy. Most of the time, you already have a web server (like apache2 or nginx) in place, which you can use to forward the incoming traffic to the SinusBot.

First you need to add a DNS record (A) which is pointing from your subdomain (e.g. sinusbot.example.com) to the IP of your server. After that, create a file at `/etc/apache2/sites-available/sinusbot.conf` with the following content.

Adjust the value of the following variables in the configuration examples below:

- `YOUR_DOMAIN` (domain of your sinusbot)
- `ProxyPass` and `ProxyPassReverse` (port of your sinusbot)
- `SSLCertificate*` (SSL only!)

<!-- TODO: check if websockets work -->

If you are using no SSL (http):

```apache
<VirtualHost *:80>
    ServerName YOUR_DOMAIN
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    ProxyPreserveHost On

    ProxyPass / http://127.0.0.1:8087/
    ProxyPassReverse / http://127.0.0.1:8087/
</VirtualHost>
```

If you are using SSL (https) with http->https redirect:

```apache
<VirtualHost *:80>
    ServerName YOUR_DOMAIN
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    RewriteEngine on
    RewriteCond %{SERVER_NAME}=YOUR_DOMAIN
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

<VirtualHost *:443>
    ServerName YOUR_DOMAIN
    
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    
    SSLEngine On
    SSLCertificateFile    /etc/letsencrypt/live/YOUR_DOMAIN/cert.pem
    SSLCertificateKeyFile /etc/letsencrypt/live/YOUR_DOMAIN/privkey.pem
    SSLCertificateChainFile /etc/letsencrypt/live/your_domain/fullchain.pem
    
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:8087/
    ProxyPassReverse / http://127.0.0.1:8087/

    Include /etc/letsencrypt/options-ssl-apache.conf
</VirtualHost>
```
> This example uses [Let's Encrypt](https://letsencrypt.org/) to generate the SSL certificate. If you are using a different certificate, you need to adjust the `SSLCertificate*` variables and remove the `Include` line.

Afterwards you need to enable the configuration file:

`a2ensite sinusbot`

Enable the proxy-module:

`a2enmod proxy`

Enable the http-proxy-module:

`a2enmod proxy_http`

Enable the SSL-module

`a2enmod ssl`

Enable the rewrite-module:

`a2enmod rewrite`

Restart apache2:

`systemctl restart apache2`

Now just follow the [common adaptations](common-adaptations.md) for reverse proxies.
