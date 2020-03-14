---
layout: post
title: How to set up Laravel and Nginx in Ubuntu 18.04
image: img/green.jpg
author: Pranay Aryal
date: 2020-03-13T10:00:00.000Z
tags:
  - Laravel 
---

Follow the instructions in the [Laravel](https://laravel.com) website to install Laravel.

After you have installed, delete the file `.env.example`

Then make the directories `/storage` and `/bootstrap/cache` writable by typing this:
```shell
sudo chown -R 777 storage/
sudo chown -R 777 bootstrap/cache 
```

Create a file in `/etc/nginx/sites-available` directory.  In my case I created on called larblog.  Then copy this in that file:
```bash
server {
      listen 80;
      server_name blog.app;
      root <path to the public folder>;
  
      add_header X-Frame-Options "SAMEORIGIN";
      add_header X-XSS-Protection "1; mode=block";
      add_header X-Content-Type-Options "nosniff";
  
      index index.html index.htm index.php;
  
      charset utf-8;
  
      location / {
          try_files $uri $uri/ /index.php?$query_string;
      }
  
      location = /favicon.ico { access_log off; log_not_found off; }
      location = /robots.txt  { access_log off; log_not_found off; }
  
      error_page 404 /index.php;
  
      location ~ \.php$ {
          fastcgi_pass unix:/var/run/php/php7.3-fpm.sock;
          fastcgi_index index.php;
          fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
          include fastcgi_params;
      }
  
      location ~ /\.(?!well-known).* {
          deny all;
      }

```
Put the path to the public folder of your Laravel project in root above.  Put the url or ip address of the app in server_name.

**Note** that for the above you need to have **php7.3-fpm** installed.  If you have php7.2 in your machine, then you need to install php7.2-fpm and replace the line in the above file like this

```bash
    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock; ##Note the php7.2 here
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
```


```bash
## If it is Ubuntu 18.04
sudo apt-get update
sudo apt-get install php7.3-fpm
```

Type `sudo nginx -t` to check syntax of above nginx files you created and you should see this output if ok:
```bash
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

Then go to `/etc/hosts` and add the name of your app there next to 127.0.0.1. In my case it is blog.app
```bash
  127.0.0.1       localhost
  127.0.0.1       blog.app
  
  # The following lines are desirable for IPv6 capable hosts
  ::1     ip6-localhost ip6-loopback
  fe00::0 ip6-localnet
  ff00::0 ip6-mcastprefix
  ff02::1 ip6-allnodes
  ff02::2 ip6-allrouters
```

Then make a sym-link in `/etc/nginx/sites-enabled/` like this:
```bash
sudo ln -s /etc/nginx/sites-available/larblog /etc/nginx/sites-enabled/
```
Replace 'larblog' with the name of your laravel project

Then do
```bash
sudo systemctl reload nginx
```

Go to Chrome and type your url there. In this case it is blog.app.  You should see your site.

If you see '502 Bad Gateway', check nginx logs like this:
```bash
sudo tail -30 /var/log/nginx/error.log
```

I had this log in `/var/log/nginx/error.log` when I wrongly had php7.2 in the nginx file above
```bash
2020/03/13 23:21:11 [crit] 7111#7111: *10 connect() to unix:/var/run/php/php7.2-fpm.sock failed (2: No such file or directory) while connecting to upstream, client: 127.0.0.1, server: blog.app, request: "GET / HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php7.2-fpm.sock:", host: "blog.app"
2020/03/13 23:21:12 [crit] 7111#7111: *10 connect() to unix:/var/run/php/php7.2-fpm.sock failed (2: No such file or directory) while connecting to upstream, client: 127.0.0.1, server: blog.app, request: "GET / HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php7.2-fpm.sock:", host: "blog.app"
2020/03/13 23:21:13 [crit] 7111#7111: *10 connect() to unix:/var/run/php/php7.2-fpm.sock failed (2: No such file or directory) while connecting to upstream, client: 127.0.0.1, server: blog.app, request: "GET / HTTP/1.1", upstream: "fastcgi://unix:/var/run/php/php7.2-fpm.sock:", host: "blog.app"
```

I installed php7.3-fpm as mentioned above and replaced the nginx file with php7.3 as mentioned above and the 'Bad Gateway' error went away.

Happy Coding.


