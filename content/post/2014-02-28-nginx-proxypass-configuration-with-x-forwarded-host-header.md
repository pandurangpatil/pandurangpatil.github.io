+++
title = "nginx proxypass configuration with X-Forwarded-Host header"
slug = "2014-02-28-nginx-proxypass-configuration-with-x-forwarded-host-header"
published = 2014-02-28T11:00:00.002000-08:00
author = "Pandurang Patil"
tags = ["nginx", "ReverseProxy"]
+++
I have used and configured `apache` for `proxy pass` and `proxy pass reverse` multiple times with `X-Forwarded-Host`. I tried configuring same with `nginx` and it works out to be more customisable and easy one.

```
        server {
            listen       80;
            server_name  pandurangpatil.com;
            location /myapp {
                proxy_set_header X-Forwarded-Host $host;
                proxy_pass http://localhost:8080/myapp;
            }
            .
            .
            .
        }
```
