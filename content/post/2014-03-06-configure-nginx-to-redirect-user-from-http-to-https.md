+++
title = "configure nginx to redirect user from HTTP to HTTPS"
slug = "2014-03-06-configure-nginx-to-redirect-user-from-http-to-https"
published = 2014-03-06T04:22:00.002000-08:00
author = "Pandurang Patil"
tags = [ "nginx", "http", "https",]
+++
When you are going to sever all requests over `SSL` then in some cases you need to only serve requests over `SSL`. While doing that you may have to disable port 80 so that all the requests will be only served through `SSL`. But in that case if user hits your url with `http`, user will see `page not found` error. Instead you can enable your port 80 and redirect all requests to `https` url with following configuration.

```
         server {
            listen      80;
            server_name www.yourdomain.com;
            return 301 https://www.yourdomain.com$request_uri;
        }
```

Adding `$request_uri` will make sure it will keep requested url as is as per requested. Other wise even if you hit the url like `http://www.yourdomain.com/company/about.html` still it will be redirected to `https://www.yourdomain.com`
