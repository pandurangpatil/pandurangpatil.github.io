+++
title = "Setup firewall with UFW on ubuntu"
slug = "2014-03-09-setup-firewall-with-ufw-on-ubuntu"
published = 2014-03-09T12:48:00-07:00
author = "Pandurang Patil"
tags = ["ubuntu", "firewall", "ufw", "linux"]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">It is
very easy to setup firewall using UFW on ubuntu server </span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">First
you need to check if you have UFW installed on your machine. If it is
installed you can check the status of the same using </span>  

    $ sudo ufw status
    Status: inactive

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">In
case it is installed but not enabled. If it is not installed then it
will throw command not found error. If it is active then it will show
out put similar like below output.</span>  

    Status: active

    To                         Action      From
    --                         ------      ----
    22                         ALLOW       Anywhere

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">If it
is not installed then you can install it </span>  

    $ sudo apt-get install ufw

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">This
will install ufw. Now when you will check the status it will be
inactive. Before you activate the same you need to set the rules.
 Depending on your requirement, you can set default policy for incoming
as well as outgoing connections. If default policy for incoming is
"deny" then all incoming connections are by default denied the access.
Except on those ports which are made open. If you set default policy to
be "allow" then all incoming connections will be allowed except on those
ports for which rule has been added to deny the connections. Same is
true for outgoing connections. Ideally we should set default policy to
be "deny" for all incoming connections and default policy to be "allow"
for all out going connections.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Set
default policy for incoming connections</span>  

    $ sudo ufw default deny incoming
    Default incoming policy changed to 'deny'
    (be sure to update your rules accordingly)

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Set
default policy for outgoing connections</span>  

    $ sudo ufw default allow outgoing
    Default incoming policy changed to 'deny'
    (be sure to update your rules accordingly)

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Now
you before you enable the UFW you have to add rules to allow connections
on specific port. **Most importantly allow connections on SSH port, if
you are doing all this on remote machine, over SSH. **Don't enable it
before you make sure you have added rule to allow connections over SSH
port.</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">add
rules to allow connections</span>  

    $ sudo ufw allow ssh
    or 
    $ sudo ufw allow 22/tcp

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Similarly
you can allow other connections over port 80 and if required 443 as
well</span>  

    $ sudo ufw allow www
    $ sudo ufw allow 443/tcp

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">you
can add deny rule like </span>  

    $ sudo ufw deny 80/tcp

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Delete
any rule like</span>  

    $ sudo ufw delete allow www

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Once
you have all rule set (Make sure you have added rule to allow ssh
connection). Now you can enable ufw to act as firewall</span>  

    $ sudo ufw enable
    Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
    Firewall is active and enabled on system startup
    $ sudo ufw status
    Status: active

    To                         Action      From
    --                         ------      ----
    22                         ALLOW       Anywhere
    443/tcp                    ALLOW       Anywhere
    80/tcp                     ALLOW       Anywhere

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span><span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
can disable it like</span>  

    $ sudo ufw disable

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span>
