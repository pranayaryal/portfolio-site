---
layout: post
title: How to Configure Nginx to Run websites
image: 
author: Pranay Aryal
date: 2019-07-10T10:00:00.000Z
tags:
  - nginx
---

![](/img/feeling-proud.svg)
This is how to configure nginx to serve a website in Ubuntu 18.04

Create a .conf file in `/etc/nginx/sites-available`. For instance, you can run `touch blog.app.conf` in the `sites-available` directory.

Copy this code to the newly created .conf file. Make sure the root points to the public directory. 

The server_name should also be the same name as the .conf file

```shell
server {
      listen 80;
  
      root /home/oem/Code/sar-upgrade/public;
      index index.html index.htm index.php;
  
      server_name blog.app;
  
      location @rewrite {
          rewrite ^/(.*)$ /index.php?_url=/$1;
      }
  
      location / {
          try_files $uri $uri/ @rewrite;
      }
  
      location ~ \.php$ {
          try_files $uri =404;
          fastcgi_split_path_info ^(.+\.php)(/.+)$;
          fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
          fastcgi_index index.php;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          include fastcgi_params;
      }
  
      location /doc/ {
          alias /usr/share/doc/;
          autoindex on;
          allow 127.0.0.1;
          deny all;
      }
  
      location ~/\.ht {
          deny all;
      }
  }
```

Then type
```shell
sudo ln -s /etc/nginx/sites-available/blog.app.conf /etc/nginx/sites-enabled/
```

Be sure to write out the full path
Check if there are any errors inside sites-enabled/ folder. If there are errors remove the conf file and try again.

Then type
```shell
sudo service nginx restart
```

You also have to go to `/etc/hosts` file and add your app name there. Mine looks like this

```shell
  127.0.0.1       localhost
  127.0.1.1       pranay-Z170GT7
  127.0.0.1       blog.app
  # The following lines are desirable for IPv6 capable hosts
  ::1     ip6-localhost ip6-loopback
  fe00::0 ip6-localnet
  ff00::0 ip6-mcastprefix
  ff02::1 ip6-allnodes
  ff02::2 ip6-allrouters
```

You can see that `blog.app` is pointing to 127.0.0.1.

If you get <strong>404 not found</strong> error then please ensure and check doubly that your path next to 'root' is correct. I ran into problems because of incorrect path

If you get 502-Bad gateway error:
Check the version of php you have by typing

```shell
php --version
```
Depending on the php version you have, change the above conf file. For example I have php7.3
So my nginx conf file looks like this. Note the php7.3-fpm in the third line end.
```shell
    try_files $uri =404;
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass unix:/var/run/php/php7.3-fpm.sock; ## Note php7.3-fpm here
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
```

After this make sure you have `php7.3-fpm` installed.  If not installed, type this to install it

```shell
sudo apt-get update
sudo apt-get install php7.3-fpm
```

After this do
```shell
sudo systemctl reload nginx
```
Your site should be running

I hope this helps