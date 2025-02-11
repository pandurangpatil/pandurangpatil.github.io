+++
title = "Install ZeroMQ on ubuntu with Java Binding "
slug = "2014-03-27-install-zeromq-on-ubuntu-with-java-binding"
published = 2014-03-27T23:38:00.001000-07:00
author = "Pandurang Patil"
tags = ["ubuntu", "zeromq", "java"]
+++
<span
style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">First
install all required tools to build zeromq library</span>  

    sudo apt-get install libtool autoconf automake uuid-dev build-essential pkg-config

<span
style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">  
</span> <span
style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">Once
you have required tools install download zeromq source code and make a
build</span>  
<span
style="font-family: &quot;helvetica neue&quot; , &quot;arial&quot; , &quot;helvetica&quot; , sans-serif;">  
</span>  

     #Download latest zermoq source code http://zeromq.org/area:download   
     #I tried it with zeromq-3.2.4.tar.gz (http://download.zeromq.org/zeromq-3.2.4.tar.gz)   
     $ zeromq-3.2.4.tar.gz  
     $ tar -zxvf zeromq-3.2.4.tar.gz  
     $ cd zeromq-3.2.4  
     $ ./configure  
     $ make  
     $ sudo make install  
     $ cd ../  


This will install zeromq libraries at location `/usr/local/lib` you may like
to set this path with `LD_LIBRARY_PATH` so that the libraries will be
used at the time of execution. If you are setting `LD_LIBRARY_PATH` from
`.profile`, or `/etc/environment` then you will it is not getting set
[refer](http://www.pandurangpatil.com/2014/03/ubuntu-134-ldlibrarypath-is-not-set.html)
GenerateJava binding refer official [documentation](http://zeromq.org/bindings:java ) for more details. 


```
     $ git clone https://github.com/zeromq/jzmq.git  
     $ cd jzmq  
     $ ./autogen.sh  
     $ ./configure  
     $ make  
     $ sudo make install
```
  
At the end you will find zmq.jar generated at location `/usr/local/share/java/zmq.jar`

**Updated Note :**

With latest version, you may get following error</span>  
  
```
    checking for sodium... no
    configure: error: Package requirements (libsodium) were not met:
    No package 'libsodium' found
```

You may not require this package, so install it with it to do that run configuration with following option


    ./configure --without-libsodium

