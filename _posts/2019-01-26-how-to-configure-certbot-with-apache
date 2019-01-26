---
classes: wide
tags: [solid certbot ssl certificate]
---

This one was a long time coming, but I finally got around to checking out [Certbot](https://certbot.eff.org/lets-encrypt/ubuntuxenial-apache) via [LetsEncrypt](https://letsencrypt.org/). This guide will demonstrate how to quickly and easily setups signed SSL certificates for multiple web services that use reverse proxy behind an Apache server, running on Ubuntu 16.04.

## The setup
The first step if to create the Apache virtual host entries for both web services. Setting up the virtual hosts is necessary so that CertBot can pick them up later on.

### Webservice 1
```bash
<VirtualHost *:*>
    ServerName localhost
    ProxyPreserveHost On
    ProxyPass / http://0.0.0.0:8000/
    ProxyPassReverse / http://0.0.0.0:8000/

    RewriteEngine on
    RewriteCond %{SERVER_NAME} =localhost [OR]
    RewriteCond %{SERVER_NAME} =webservice1.co.uk
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```

### Webservice 2
```bash
<VirtualHost *:*>
    ServerName webservice2.com
    ProxyPreserveHost On
    ProxyPass / http://0.0.0.0:8802/
    ProxyPassReverse / http://0.0.0.0:8802/

    RewriteEngine on
    RewriteCond %{SERVER_NAME} =webservice1.co.uk
    RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>
```
Remember to enable the virtual hosts using the command `sudo a2ensite webservice1.com.conf` and `sudo service apache2 reload`.

## Install Certbot

Simply run the following commands in the terminal:

```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install python-certbot-apache 
```

## Configure a certificate for one of the webservices
Run `sudo certbot --apache` in the terminal and follow the prompts. 

You can now navigate to the webservice using the the `https` protocol. So simple!

## Automatic renewal
Automatic renewly, of the 90 certificates, is active be default but you can test this mechanism using `sudo certbot renew --dry-run`.
