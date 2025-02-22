+++
title = "Tomcat 7 onwards set additional JAVA_OPTS options"
slug = "2014-02-26-tomcat-7-onwards-set-additional-java-opts-options"
published = 2014-02-26T11:46:00-08:00
author = "Pandurang Patil"
tags = ["tomcat", "java"]
+++
To set `JAVA_OPTS` options which you want to set additionally while running the `tomcat` should be set inside `<tomcat home>/bin/setenv.sh` if this file is not present then create one and set variable `JAVA_OPTS="-Dsomething $JAVA_OPTS"`. If you have to set some variables while only starting the tomcat then you need to set those variables to `CATALINA_OPTS` rather than `JAVA_OPTS`.
