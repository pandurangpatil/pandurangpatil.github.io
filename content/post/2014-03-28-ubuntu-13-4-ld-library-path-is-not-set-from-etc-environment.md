+++
title = "UBUNTU 13.4 LD_LIBRARY_PATH is not set from /etc/environment"
slug = "2014-03-28-ubuntu-13-4-ld-library-path-is-not-set-from-etc-environment"
published = 2014-03-28T00:49:00.003000-07:00
author = "Pandurang Patil"
tags = ["ubuntu", ]
+++

For some reason `LD_LIBRARY_PATH` value is not getting set through `/etc/environment`. All other variables are getting initialized properly when it is been set through `/etc/environment`. After searching for the solution I came to know after UBUNTU 9.04 release you are not able to set `LD_LIBRARY_PATH` from `$HOME/.profile`, `/etc/profile`, nor `/etc/environment` refer [documentation](https://help.ubuntu.com/community/EnvironmentVariables#List_of_common_environment_variables)

Run following command and restart the machine to workaround the issue.

```
    echo STARTUP=\"/usr/bin/env LD_LIBRARY_PATH=\${LD_LIBRARY_PATH} \${STARTUP}\" | sudo tee /etc/X11/Xsession.d/90preserve_ld_library_path
```

For more details refer [comment](https://bugs.launchpad.net/ubuntu/+source/xorg/+bug/366728) \#17 at this bug report, aswell as [refer](https://bugs.launchpad.net/ubuntu/+source/xorg/+bug/380360)

