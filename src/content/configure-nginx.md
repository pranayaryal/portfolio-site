---
layout: post
title: How to Configure Nginx to Run websites
image: 
author: Pranay Aryal
date: 2019-07-10T10:00:00.000Z
tags:
  - nginx
---

I will show you how to configure nginx to serve a website

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

If you get <strong>404 not found</strong> error then please ensure and check doubly that your path next to 'root' is correct. I ran into problems because of incorrect path

I hope this helps