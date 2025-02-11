+++
title = "Setup virtualbox on Ubuntu Server 64 Bit "
slug = "2014-07-12-setup-virtualbox-on-ubuntu-server-64-bit"
published = 2014-07-12T02:47:00.004000-07:00
author = "Pandurang Patil"
tags = [ "virtualbox", "ubuntu"]
+++
Setup virtual box on ubuntu server `64bit` and use `phpvirtualbox` to access webui of VirtualBox to manage the instances on virtualbox.

1. Ubuntu Server 64bit
2. VirtualBox4.3.
3. phpvirtualbox

Running `VirtualBox` and `phpvirtualbox` on the same machine.

I mostly followed followed this blog http://santi-bassett.blogspot.in/2013/01/installing-virtualbox-on-ubuntu-server.html.

Except few changes. 

1. When I installed virtual box I installed latest version 4.3.*
2. location of `phpvirtualbox` has been changed to sourceforge.net http://sourceforge.net/projects/phpvirtualbox/files/ and used phpvirtualbox 4.3.1 version.

However even after following all the steps right I got following error

I click on details and get the following:

    Exception Object
    (
        [message:protected] => Could not connect to host (http://127.0.0.1:18083/

I started `vboxwebsrv` server in foreground and tried to telnet `18083`, everything was fine. Then I tried to do wget with url http://127.0.0.1:18083 and responded connection refused. Then I tried to `wget` with url `http://localhost:18083` and it responded with 403 error. So url was the problem. Update `config.php` with `http://localhost:18083` in place of `http://127.0.0.1:18083`.

This solved my problem.