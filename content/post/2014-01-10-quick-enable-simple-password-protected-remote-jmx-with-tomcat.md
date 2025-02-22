+++
title = "Quick enable simple password protected Remote JMX with tomcat "
slug = "2014-01-10-quick-enable-simple-password-protected-remote-jmx-with-tomcat"
published = 2014-01-10T04:39:00.004000-08:00
author = "Pandurang Patil"
tags = [ "JMX",]
+++
You need to do following configuration to enable `Remote JMX` monitoring on `tomcat` server.

1. Copy `jmxremote.password.template` located at `JRE_HOME/lib/management` inside the same folder with the name `jmxremote.password`.
2. Edit this `jmxremote.password` file, uncomment last two lines starts with `monitorRole` and `controleRole`, instead of QED and R&D set some good password for both of them.
3. Change directory to `CATALINA_HOME/bin` from where you start the tomcat. 
4. You will find `setenv.sh` (if you don't find it create one) and add following line inside file 

```
CATALINA_OPTS="$CATALINA_OPTS -Dcom.sun.management.jmxremote.port=9000 -Djava.rmi.server.hostname=127.0.0.1 -Dcom.sun.management.jmxremote.ssl=false"
```
5. Here in above line you need to set proper ip address which is accessible from remote machine to `-Djava.rmi.server.hostname` and set available port number to `-Dcom.sun.management.jmxremote.port`
6. Once all this settings are done `restart`/`start` tomcat.

Above steps will enable `remote JMX` on this `JVM`. To monitor it using `jconsole` from remote machine follow below steps from remote machine.

1. Start `jconsole` 

```
    $ jconsole
```

2. Select Remote Process option and enter `<remote ip address>:<port>` , specify username as `monitorRole` or `controleRole`  and password that you set inside `jmxremote.password` file for corresponding user. 

This should start remote monitoring of remote JVM tomcat.
