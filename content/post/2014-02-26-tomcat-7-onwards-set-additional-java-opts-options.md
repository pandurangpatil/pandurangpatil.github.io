+++
title = "Tomcat 7 onwards set additional JAVA_OPTS options"
slug = "2014-02-26-tomcat-7-onwards-set-additional-java-opts-options"
published = 2014-02-26T11:46:00-08:00
author = "Pandurang Patil"
tags = ["tomcat", "java"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">To
set JAVA\_OPTS options which you want to set additionally while running
the tomcat should be set inside set &lt;tomcat home&gt;/bin$setenv.sh if
this file is not present then create one and set variable
JAVA\_OPTS="-Dsomething $JAVA\_OPTS". If you have to set some variables
while only starting the tomcat then you need to set those variables
to </span>CATALINA\_OPTS<span
style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;"> rather
than JAVA\_OPTS. </span>
