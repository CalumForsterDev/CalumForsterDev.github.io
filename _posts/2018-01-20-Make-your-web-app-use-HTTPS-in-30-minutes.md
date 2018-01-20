---
title: Make your web app use HTTPS in 30 minutes with Let's Encrypt and NGINX
---

# Make your web app use HTTPS in 30 minutes with Let's Encrypt and NGINX
<img src="https://letsencrypt.org/images/letsencrypt-logo-horizontal.svg" width="30%"/>

So you have an application which works over HTTP and you want to switch to HTTPS. You can do it for free with Let's Encrypt and NGINX. It should only take about 30 minutes...

  1. Register a free domain name (if you don't already have one) `10 minutes`
  2. Setup your NGINX proxy `10 minutes`
  3. Use certbot to generate certificates `10 minutes`

## Register a free domain name (if you don't already have one)
You need to have a domain name to use HTTPS. If you don't already have one, you can register one for free at [dot.tk](http://www.dot.tk/).

Once you have registered a domain, you need to set up your DNS records for it. If you used [dot.tk](http://www.dot.tk/) then you want to click through `Services -> My Domains -> Manage Domain -> Manage Freenom DNS` and then add a blank record with the `Target` set to be your server's IP address.

## Setup your NGINX proxy
You need to install NGINX onto your server and setup the configuration so that NGINX will forward any traffic onto your application.

<img src="https://avatars0.githubusercontent.com/u/1412239?s=200&v=4" width="20%"/>

_If you are having problems with NGINX, then take a look at their [beginner guide](http://nginx.org/en/docs/beginners_guide.html)_

### Install NGINX
The quickest way to install is to use a package manager. Find steps on how to install NGINX onto your operating system using the [NGINX install guide](https://www.nginx.com/resources/admin-guide/installing-nginx-open-source/#prebuilt).


If you are using Ubuntu, then it is as easy as

```sh
$ sudo apt-get update
$ sudo apt-get install nginx
$ sudo nginx -v
nginx version: nginx/1.6.2
```

or for CentOS/Red Hat

```sh
$ sudo yum install epel-release
$ sudo yum update
$ sudo nginx -v
nginx version: nginx/1.6.3
```

### Configure NGINX
You want to edit the NGINX configuration file. On Ubuntu this is found at `/etc/nginx/conf.d/virtual.conf`. You will need to edit the file as root.

```sh
$ sudo nano /etc/nginx/conf.d/virtual.conf
```

Then change the file to be the following config (swapping `yourdomain.cf` with your registered domain name)

```
server {
    listen       80;
    server_name  yourdomain.cf localhost;

    location / {
      proxy_pass http://localhost:8000;
      proxy_http_version 1.1;
    }
}
```

After changing the configuration file you need to restart NGINX. This if you are using Ubuntu, this is `$ sudo service nginx restart`. If you are having problems with NGINX, then take a look at their [beginner guide](http://nginx.org/en/docs/beginners_guide.html).

## Use certbot to generate certificates
Now for the fun part. You want to use [certbot](https://certbot.eff.org/) to setup your Let's Encrypt certificates. Certbot will also update your NGINX configuration file to use HTTPS instead of HTTP!

<img src="https://certbot.eff.org/images/certbot-logo-1A.svg" width="30%"/>

Go to [certbot's website](https://certbot.eff.org/) and select `I'm using Nginx on ...` and your operating system. If you are using amazon web services then you can select `Other UNIX`.

Certbot will then give you the commands to run. While you run the scripts, certbot will ask you questions to help you with your configuration. Make sure that when it asks about updating your NGINX config file for you that you select `yes` - it makes the process slightly easier.

And you're done! Test it out by going to `https://yourdomain.cf`. Your web application is now running encrypted! ![](/assets/Lock.svg)


[Home](/)
