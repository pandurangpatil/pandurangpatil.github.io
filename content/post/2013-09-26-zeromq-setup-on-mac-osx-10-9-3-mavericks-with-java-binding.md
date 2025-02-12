+++
title = "Zeromq setup on MAC OSX 10.9.3 (mavericks) with Java binding"
slug = "2013-09-26-zeromq-setup-on-mac-osx-10-9-3-mavericks-with-java-binding"
published = 2013-09-26T08:39:00.002000-07:00
author = "Pandurang Patil"
tags = [ "zeromq", "OSX", "Mac"]
+++

Steps: With reference to following blogs written by Vivek [blog](http://technicalvvkydv.blogspot.in/2011/06/making-zeromq-jar-for-mac.html) to install zeromq and by
Jean [blog](http://jsdelfino.blogspot.in/2012/08/autoconf-and-automake-on-mac-os-x.html) to
install `auto tools`. I faced few issues ( one of them is following error `./configure: line 15284: 'PKG_CHECK_MODULES'`) which I tried to address with following steps:  
  

1.  Install `gcc` ( to install `gcc` you need to install `xcode` 5 download it from `https://developer.apple.com/xcode/ and install.)
2.  Make sure you have `java` installed. If you want to install `JDK 7` refer this http://docs.oracle.com/javase/7/docs/webnotes/install/mac/mac-jdk.html

3.  Make sure you have `git` installed to checkout `zeromq` java binding source code.

4.  Make sure `libtool`, `autoconf`, `automake` are installed. [refer](http://jsdelfino.blogspot.in/2012/08/autoconf-and-automake-on-mac-os-x.html). I preferred installing binaries in system directory directly. If you have already installed it then you can skip this step.
```
    # create a temporary folder to checkout / download source code and build the same  
    $ mkdir build  
    $ cd build  
    $ curl -OL http://ftpmirror.gnu.org/autoconf/autoconf-2.69.tar.gz  
    $ tar -xzf autoconf-2.69.tar.gz  
    $ cd autoconf-2.69  
    $ ./configure  
    $ make  
    $ sudo make install  
    $ cd ../  
    $ curl -OL http://ftpmirror.gnu.org/automake/automake-1.14.tar.gz  
    $ tar -xzf automake-1.14.tar.gz  
    $ cd automake-1.14  
    $ ./configure  
    $ make  
    $ sudo make install  
    $ cd ../  
    $ curl -OL http://ftpmirror.gnu.org/libtool/libtool-2.4.2.tar.gz  
    $ tar xzf libtool-2.4.2.tar.gz  
    $ cd libtool-2.4.2  
    $ ./configure  
    $ make  
    $ sudo make install  
    $ cd ../  
```
5.  Install core `ZeroMQ` library.

```
    #Download latest zermoq source code http://zeromq.org/area:download   
    #I tried it with zeromq-3.2.4.tar.gz (http://download.zeromq.org/zeromq-4.0.4.tar.gz)   
    $ curl -OL http://download.zeromq.org/zeromq-4.0.4.tar.gz  
    $ tar -zxvf zeromq-4.0.4.tar.gz  
    $ cd zeromq-4.0.4  
    $ ./configure  
    $ make  
    $ sudo make install  
    $ cd ../  
```

6.  Install `pkg-config`. If you already have it installed then you can skip this step.
```
    $ curl -OL http://pkgconfig.freedesktop.org/releases/pkg-config-0.28.tar.gz  
    $ tar -zxvf pkg-config-0.28.tar.gz  
    $ cd pkg-config-0.28   
    $ ./configure --with-internal-glib 
    $ make  
    $ sudo make install  
    $ cd ../  
```

7.  Install/generate `ZeroMQ` `JAVA` binding for more details [refer](http://zeromq.org/bindings:java)
```
    $ git clone https://github.com/zeromq/jzmq.git  
    $ cd jzmq  
    # if you already have JAVA_HOME set you can skip this  
    $ export JAVA_HOME=`/usr/libexec/java_home`  
    $ ./autogen.sh  
    $ ./configure  
    $ make  
    $ sudo make install  
```
At the end you will find `zmq.jar` generated at location `/usr/local/share/java/`
