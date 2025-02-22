+++
title = "Install nginx on OS-X"
slug = "2014-02-18-install-nginx-on-os-x"
published = 2014-02-18T23:40:00-08:00
author = "Pandurang Patil"
tags = ["nginx", "osx"]
+++
One need to have `gcc` installed for that you need to install `xcode` along with command line tools. To install the same one can [refer](http://stackoverflow.com/questions/9329243/xcode-4-4-and-later-install-command-line-tools) to this link for xcode 5.0.1.

`Nginx` requires `PCRE` – `Perl` Compatible Regular Expressions to build, I used `PCRE` version `8.33`

Install `PCRE`

    $ mkdir source
    $ cd source
    $ curl -OL ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.33.tar.gz
    $ tar -zxvf pcre-8.33.tar.gz 
    $ cd pcre-8.33/
    $ ./configure
    $ make
    $ sudo make install


Install `nginx`

Here I am considering stable version for installation.

    $ cd ..
    $ curl -OL http://nginx.org/download/nginx-1.4.4.tar.gz
    $ tar -zxvf nginx-1.4.4.tar.gz
    $ cd nginx-1.4.4
    $ ./configure --with-http_ssl_module --with-pcre=../pcre-8.33
    # When you are done with ./configure command you will see below output at the end you might want to keep this information copied some where for future reference.
    $ make
    $ sudo make install

Output-- 

    nginx path prefix: "/usr/local/nginx"
    nginx binary file: "/usr/local/nginx/sbin/nginx"
    nginx configuration prefix: "/usr/local/nginx/conf"
    nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
    nginx pid file: "/usr/local/nginx/logs/nginx.pid"
    nginx error log file: "/usr/local/nginx/logs/error.log"
    nginx http access log file: "/usr/local/nginx/logs/access.log"
    nginx http client request body temporary files: "client_body_temp"
    nginx http proxy temporary files: "proxy_temp"
    nginx http fastcgi temporary files: "fastcgi_temp"
    nginx http uwsgi temporary files: "uwsgi_temp"
    nginx http scgi temporary files: "scgi_temp"

  
`Start`/`Stop` `nginx`</span>  
  
    # Start
    $ sudo /usr/local/nginx/sbin/nginx 

    # Stop
    $ sudo /usr/local/nginx/sbin/nginx -s stop

For more details on command line help [refer](http://wiki.nginx.org/CommandLine) you
can make your life easier to access `ngnix` from anywhere by adding `nginx` path `/usr/local/nginx/sbin` into `PATH` environment variable inside `~/.profile` file.
