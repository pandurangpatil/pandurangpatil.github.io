+++
title = "Troubleshout Open file limit"
slug = "2015-12-11-troubleshout-open-file-limit"
published = 2015-12-11T03:36:00.003000-08:00
author = "Pandurang Patil"
tags = [ "ubuntu", "linux"]
+++

  
1. Show no of open files sorted by PID  - `lsof | awk '{ print $2; }' | uniq -c | sort -rn | head`  
2. Check individual file limits of a process  - `cat /proc/<PID>/limits`  
3. to obtain a precise count of the open files at given instant of time - `ls /proc/<PID>/fd | wc -l`  
4. This will list all open files with given process  - `lsof -p <PID>`
  
  
In some cases you might have to look at the open file limit of the process which started your process.  
  
Make sure you add `ulimit -n XXX` values inside your startup script, if you have configured it to start the process on machine startup or restart. Especially on Debian Linux flavour refer (https://bugs.launchpad.net/ubuntu/+source/upstart/+bug/938669)
