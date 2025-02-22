+++
title = "MySql Datafiles are getting corrupted on Mac-OSX abrupt shutdown"
slug = "2014-04-12-mysql-datafiles-are-getting-corrupted-on-mac-osx-abrupt-shutdown"
published = 2014-04-12T21:19:00-07:00
author = "Pandurang Patil"
tags = ["mysql", "mac", "OSX"]
+++
I have consistently faced this issue of `MySql` data files getting corrupted when my machine is rebooted abruptly. This has resulted into repetitive work that I have to do to rebuild the data. I tried to google for the solution and see if somebody else has seen this issue. But it seems this the way it will work, as `MySql` data files are not closed properly which results into corrupt database in case your machine gets abruptly restarted. I got this reference on [stackexchange](http://superuser.com/questions/704393/mysql-tables-corrupt-when-plugging-off-power-on-mac-os-server)

To recover corrupted data some times following commands worked well but not always.

    $ sudo mysqladmin refresh  
    $ sudo mysqladmin flush-tables


Finally restart your `myql` server.  

So to over come this issue, I stoped my `MySql` service when I am not using it. This is not the perfect solution, as there is a still possibility your machine gets hanged or restarted abruptly while you are working with `MySql`. But at least it will lower down the possibility of corruption when you are not using it.
