+++
title = "Mysql 5.5 is not accessible remotely."
slug = "2014-04-13-mysql-5-5-is-not-accessible-remotely"
published = 2014-04-13T01:34:00-07:00
author = "Pandurang Patil"
tags = ["mysql"]
+++
I recently installed MySql 5.5 and tried to access it from remote machine. But it was not accessible. I had added remote user for the remote machine from which I was trying to access the DB. But it was failing to connect, I even tried to connect it through telnet. Then I found that by default mysql is only bound to serve localhost requests only. If you need to access it remotely you need to make changes in my.cnf file to bind mysql service to actual network ip address through which you will access it remotely.

Follow below steps to make those changes

1. First locate your my.cnf file. For me it was located at `/etc/mysql/my.cnf` on ubuntu server machine.
2. Look for the `[mysqld]` section, and in there look for the bind-address keyword. This usually is set to `127.0.0.1` -- change that to match your "normal" IP-address. 
3. Save file, close it and restart mysql service

Now when try with telnet, you should be able to connect to the service. If you still facing this issue then probably you need to also check if you are running any firewall, which is blocking this connection. In that case you need to allow user to connect to mysql port through firewall.

Note: You need to add remote user to access mysql from remote machine.
