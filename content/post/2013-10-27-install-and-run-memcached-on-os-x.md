+++
title = "Install and run memcached on OS-X"
slug = "2013-10-27-install-and-run-memcached-on-os-x"
published = 2013-10-27T10:42:00-07:00
author = "Pandurang Patil"
tags = [ "memcached", "mac", "OSX"]
+++
<span
style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">One
need to have gcc installed for that you need to install xcode along with
command line tools. To install the same one can
[refer](http://stackoverflow.com/questions/9329243/xcode-4-4-and-later-install-command-line-tools)
to this link for xcode 5.0.1.  Libevent is required to be installed for
memcached so you need to first install libevent, if it is already
installed on your machine you can skip this step.</span>  
  
<span
style="font-family: &quot;Helvetica Neue&quot;, Arial, Helvetica, sans-serif;">Create
temp directory and change directory to that location and execute
following commands.</span>  
  
  

     $ curl -O http://www.monkey.org/~provos/libevent-1.4.14-stable.tar.gz  
     $ tar xzvf libevent-1.4.14-stable.tar.gz  
     $ cd libevent-1.4.14-stable  
     $ ./configure   
     $ make  
     $ sudo make install   

<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">  
</span> <span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">now
install memcached</span> <span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">  
</span>  

     $ curl -O http://memcached.googlecode.com/files/memcached-1.4.15.tar.gz  
     $ tar -zxvf memcached-1.4.15.tar.gz  
     $ cd memcached-1.4.15  
     $ ./configure  
     $ make  
     $ sudo make install  

<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">  
</span> <span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">Above
steps will install the memcached on your OS-X. Once it is done you can
start it</span>  
<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"></span>  

     $ memcached -d -p 11211  

<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"></span>  
<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"></span>
