+++
title = "Check Cron executed or not."
slug = "2014-03-10-check-cron-executed-or-not"
published = 2014-03-10T04:02:00.004000-07:00
author = "Pandurang Patil"
tags = ["cron", "linux", "ubuntu"]
+++
Many a times it happens we schedule some `cron` job to get executed, we do check as well whether command gets executed properly or not. And even though we tried the command your `cron` fail to execute. There
are two possibilities either `cron` is not configured properly or some how command is failed. Now in this case how do we check if `cron` is getting executed or not. Does it gets logged some where when is last `cron` executed? Yes it does get logged in `syslog` you can run following command to check `cron` entries

```
    $ grep CRON /var/log/syslog
    Mar 10 08:00:01 staging01 CRON[23609]: (root) CMD (my-command)
    Mar 10 08:00:01 staging01 CRON[23608]: (CRON) info (No MTA installed, discarding output)
    Mar 10 08:10:01 staging01 CRON[23611]: (root) CMD (my-command)
    Mar 10 08:10:01 staging01 CRON[23610]: (CRON) info (No MTA installed, discarding output)
    Mar 10 08:17:01 staging01 CRON[23613]: (root) CMD (   cd / && run-parts --report /etc/cron.hourly)
    Mar 10 08:20:01 staging01 CRON[23616]: (root) CMD (my-command)
    Mar 10 08:20:01 staging01 CRON[23615]: (CRON) info (No MTA installed, discarding output)
    Mar 10 08:30:01 staging01 CRON[23618]: (root) CMD (my-command)
    Mar 10 08:30:01 staging01 CRON[23617]: (CRON) info (No MTA installed, discarding output)
    Mar 10 08:40:01 staging01 CRON[23620]: (root) CMD (my-command)
    Mar 10 08:40:01 staging01 CRON[23619]: (CRON) info (No MTA installed, discarding output)
    Mar 10 08:50:01 staging01 CRON[23698]: (root) CMD (my-command)
```
