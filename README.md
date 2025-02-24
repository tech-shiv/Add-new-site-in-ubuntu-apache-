﻿# Add new site in ubuntu (apache)

## Prerequisites
> In order to complete this tutorial, you will need access to the following on an Ubuntu 20.04 server:
- A sudo user on your server
- An Apache2 web server, which you can install with"
```
sudo apt install apache2
```
### Step 1 — Create the Directory Structure
```
sudo mkdir -p /var/www/example.com/public_html
```
### Step 2 — Grant Permissions
```
sudo chown -R $USER:$USER /var/www/example.com/public_html
```
### Step 3 — Create the Virtual Host File
```
sudo nano /etc/apache2/sites-available/example.com.conf
```
```
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/example.com/public_html
    ServerName example.com
    ServerAlias www.example.com
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
### Step 4 — Enable the Virtual Host
```
sudo a2ensite example.com.conf
```
### Step 5 — Reload Apache
```
sudo systemctl reload apache2
```
### Step 6 — Test the Virtual Host
```
example.com.conf
```
### Step 7 — Create the Document Root
```
sudo mkdir -p /var/www/example.com/public_html
```
### Step 8 — Create the Index File
```
sudo nano /var/www/example.com/public_html/index.html
```
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```
### Step 9 — Set Up Local Hosts File (Optional)
```
sudo nano /etc/hosts
```
```
127.0.0.1   localhost
127.0.1.1   guest-desktop
your_server_IP example.com
your_server_IP test.com
```
### Step 10 — Test your Results
```
http://example.com
```
# Install SSl on ubuntu

## Install Certbot in Ubuntu with PIP

> First, install PIP:
``` 
sudo apt install python3 python3-venv libaugeas0
```
> Set up a virtual environment:
```
sudo python3 -m venv /opt/certbot/

sudo /opt/certbot/bin/pip install --upgrade pip
```
> Install Certbot on Apache:
```
sudo /opt/certbot/bin/pip install certbot certbot-apache
```
> Install Certbot on NGINX:
```
sudo /opt/certbot/bin/pip install certbot certbot-nginx
```

> Create a symlink to ensure Certbot runs:
```
sudo ln -s /opt/certbot/bin/certbot /usr/bin/certbot
```
## Install Certbot in Ubuntu with snapd

> Install snapd:
```
sudo apt install snapd
```
> Ensure you have the latest snapd version installed:
```
sudo snap install core; sudo snap refresh core
```

> Install Certbot with snapd:
```
sudo snap install --classic certbot
```
> Create a symlink to ensure Certbot runs:
```
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

## Create an SSL Certificate with Certbot

### Choose the best option for your needs.

> Create SSL certs for all domains and configure redirects in the web server:
```
sudo certbot --apache

sudo certbot --nginx
```

> Create SSL certs for a specified domain (recommended if you’re using your system hostname):
```
sudo certbot --apache -d [domain] -d www.[domain]

sudo certbot --nginx -d [domain] -d www.[domain]
```

### If prompted, choose whether to redirect HTTP traffic to HTTPS – 1 (no redirect, no further changes to the server) or 2 (redirect all HTTP requests to HTTPS).

