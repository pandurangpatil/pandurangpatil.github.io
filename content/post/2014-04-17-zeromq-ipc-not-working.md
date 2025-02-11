+++
title = "ZeroMQ ipc not working"
slug = "2014-04-17-zeromq-ipc-not-working"
published = 2014-04-17T05:20:00.001000-07:00
author = "Pandurang Patil"
tags = [ "zeromq",]
+++
If you are using Zero MQ IPC endpoint url like `ipc://someendpoint`. Then communication between two threads of same process will work perfectly fine. But it will fail if you are trying to communicate across the processes. If you look at [ZeroMQ](http://api.zeromq.org/2-1:zmq-ipc) document properly end point should correspond to path. Thats where above end point url works fine for intra process communication as this file `someendpoint` will correspond to file in current directory from where you are running this app. Both the threads will connect to same file. But in case of communication between two process, if you are running these application from different locations then `someendpoint` will correspond to two different paths.

So perfect endpoint for inter process communication is to have fully qualified file path e.g. (considering `tmp` folder is present inside root folder) `/tmp/someendpoint` complete url will be `ipc:///tmp/someendpoint`.
