+++
title = "Run eclipse on remote ubuntu 13.10 server using x11"
slug = "2014-03-29-run-eclipse-on-remote-ubuntu-13-10-server-using-x11"
published = 2014-03-29T13:20:00.001000-07:00
author = "Pandurang Patil"
tags = ["eclipse", "ubuntu", "remote"]
+++

To run eclipse from on remote ubuntu 13.10 server using x11 on local machine.

*Prerequisites:*  I am assuming `JDK` and `Eclipse` is already installed.

In addition to that you need to install few libraries on remote server. Run the following command to install those libraries on remote server.

```
      $ sudo apt-get install libgtk2.0-0:i386 libxxf86vm1:i386 libsm6:i386 lib32stdc++6 libxtst6
```

Once above libraries are install open another terminal and connect remote server through `ssh` with `-X` option

```
    #From local machine
    $ ssh <username>@<remote machine ip> -X
```

Now you can start the eclipse from this ssh session

```
    #From local machine
    $ cd <to location where eclipse is installed>
    $ ./eclipse
```
