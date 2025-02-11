+++
title = "Quick enable simple password protected Remote JMX with tomcat "
slug = "2014-01-10-quick-enable-simple-password-protected-remote-jmx-with-tomcat"
published = 2014-01-10T04:39:00.004000-08:00
author = "Pandurang Patil"
tags = [ "JMX",]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
need to do following configuration to enable Remote JMX monitoring on
tomcat server.</span>

1.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Copy</span><span
    style="font-family: Courier New, Courier, monospace;"> <span
    style="color: #444444;"><span
    style="font-size: x-small;">jmxremote.password.template</span></span></span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    located at </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">JRE\_HOME/lib/management</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;"> inside
    the same folder with the name </span><span
    style="color: #444444;"><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">jmxremote.password</span></span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">.
      </span>
2.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Edit
    this </span><span style="color: #444444;"><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">jmxremote.password</span></span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    file and uncomment last two lines starts with </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">monitorRole</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    and </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">controleRole</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    and instead of QED and R&D set some good password for both of
    them.</span>
3.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Change
    directory to </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">CATALINA\_HOME/bin</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    from where you start the tomcat. </span>
4.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
    will find </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">setenv.sh</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    (if you don't find it create one) and add following line inside file
    </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">CATALINA\_OPTS="$CATALINA\_OPTS
    -Dcom.sun.management.jmxremote.port=9000
    -Djava.rmi.server.hostname=127.0.0.1
    -Dcom.sun.management.jmxremote.ssl=false"</span>
5.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Here
    in above line you need to set proper ip address which is accessible
    from remote machine to </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">-Djava.rmi.server.hostname</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    and set available port number to </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">-Dcom.sun.management.jmxremote.port 
    </span>
6.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Once
    all this settings are done restart / start tomcat.</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Above
steps will enable remote JMX on this JVM. To monitor it using jconsole
from remote machine follow below steps from remote machine.</span>

1.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Start
    jconsole </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">$
    jconsole</span>
2.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Select
    Remote Process option and enter </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">"&lt;remote
    ip address&gt;:&lt;port&gt;"</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">,
    specify username as </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">monitorRole</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    or </span><span
    style="font-family: Courier New, Courier, monospace; font-size: x-small;">controleRole</span><span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">
    and password that you set inside jmxremote.password file for
    corresponding user. </span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">This
should start remote monitoring of remote JVM tomcat.</span>
