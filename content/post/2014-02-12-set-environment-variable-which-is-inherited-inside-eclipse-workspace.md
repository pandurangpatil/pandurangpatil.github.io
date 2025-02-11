+++
title = "Set environment variable which is inherited inside eclipse workspace"
slug = "2014-02-12-set-environment-variable-which-is-inherited-inside-eclipse-workspace"
published = 2014-02-12T10:53:00.002000-08:00
author = "Pandurang Patil"
tags = ["ubuntu", "eclipse"]
+++
**Ubuntu**
: Set required environment variable inside /etc/environment and restart
the machine. This will set environment variable which can be inherited
inside eclipse workspace.  Above method will set the environment
variable for all the users.  To set environment variable for individual
user set the required variable inside &lt;user home&gt;/.profile file.
While doing so please make sure you use "export" keyword before variable
which is required if those variables are expected to be passed on to
subprocess. You need to make use of "export" keyword while setting those
variables from inside ".bashrc". </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Note:
There is some issue to set LD\_LIBRARY\_PATH through /etc/environment
[refer](http://www.pandurangpatil.com/2014/03/ubuntu-134-ldlibrarypath-is-not-set.html)
<span id="goog_1670417350"></span><span id="goog_1670417351"></span>for
workaround.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">**MAC
OSX** (tested on maverick): Set required environment variable
inside /etc/launchd.conf (setenv PROJECT\_HOME &lt;Project home
location) and restart the machine. </span>
