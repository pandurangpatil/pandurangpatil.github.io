+++
title = "Setup firewall with UFW on ubuntu"
slug = "2014-03-09-setup-firewall-with-ufw-on-ubuntu"
published = 2014-03-09T12:48:00-07:00
author = "Pandurang Patil"
tags = ["ubuntu", "firewall", "ufw", "linux"]
+++
It is very easy to setup `firewall` using `UFW` on `ubuntu` server. First you need to check if you have `UFW` installed on your machine. If it is installed you can check the status of the same using  

```
    $ sudo ufw status
    Status: inactive
```

In case it is installed but not `enabled`. If it is not installed then it will throw command not found error. If it is active then it will show out put similar like below output.

```
    Status: active

    To                         Action      From
    --                         ------      ----
    22                         ALLOW       Anywhere
```

If it is not installed then you can install it

```
    $ sudo apt-get install ufw
```

This will install `ufw`. Now when you will check the status it will be `inactive`. Before you `activate` the same you need to set the rules. Depending on your requirement, you can set default policy for incoming
as well as outgoing connections. If default policy for incoming is `deny` then all incoming connections are by default denied the access. Except on those ports which are made open. If you set default policy to
be `allow` then all incoming connections will be allowed except on those ports for which rule has been added to deny the connections. Same is true for outgoing connections. Ideally we should set default policy to be `deny` for all incoming connections and default policy to be `allow` for all out going connections.

Set default policy for incoming connections

```
    $ sudo ufw default deny incoming
    Default incoming policy changed to 'deny'
    (be sure to update your rules accordingly)
```

Set default policy for outgoing connections

```
    $ sudo ufw default allow outgoing
    Default incoming policy changed to 'deny'
    (be sure to update your rules accordingly)
```

Now you before you enable the `UFW` you have to add rules to allow connections on specific port. **Most importantly allow connections on `SSH` port, if you are doing all this on remote machine, over `SSH`.** Don't enable it before you make sure you have added rule to allow connections over `SSH` port.

add rules to allow connections to `SSH` port

```
    $ sudo ufw allow ssh
    or 
    $ sudo ufw allow 22/tcp
```

Similarly you can allow other connections over port `80` and if required `443` as well

```
    $ sudo ufw allow www
    $ sudo ufw allow 443/tcp
```

you can add deny rule like

```
    $ sudo ufw deny 80/tcp
```

Delete any rule like

```
    $ sudo ufw delete allow www
```

Once you have all rule set (Make sure you have added rule to allow 1 connection). Now you can enable `ufw` to act as firewall

```
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
```

You can disable it like

```
    $ sudo ufw disable
```
