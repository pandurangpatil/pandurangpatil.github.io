+++
title = "Set environment variable which is inherited inside eclipse workspace"
slug = "2014-02-12-set-environment-variable-which-is-inherited-inside-eclipse-workspace"
published = 2014-02-12T10:53:00.002000-08:00
author = "Pandurang Patil"
tags = ["ubuntu", "eclipse"]
+++
**Ubuntu :**
Set required environment variable inside `/etc/environment` and restart the machine. This will set environment variable which can be inherited inside eclipse workspace. Above method will set the environment variable for all the users. To set environment variable for individual user set the required variable inside `<user home>/.profile` file. While doing so please make sure you use `export` keyword before variable. Alterante option to use `.bashrc` to set those environment variable, here as well you need to prefix `export` keyword.

Note: here is some issue to set `D_LIBRARY_PATH` through `/etc/environment` [refer](http://www.pandurangpatil.com/2014/03/ubuntu-134-ldlibrarypath-is-not-set.html) for workaround. 

**MAC OSX :** (tested on `maverick`): Set required environment variable inside `/etc/launchd.conf` (`setenv PROJECT_HOME <Project home location>`) and restart the machine.
