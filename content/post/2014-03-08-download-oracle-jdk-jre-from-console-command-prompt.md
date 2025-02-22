+++
title = "Download Oracle JDK / JRE from console / command prompt"
slug = "2014-03-08-download-oracle-jdk-jre-from-console-command-prompt"
published = 2014-03-08T00:03:00-08:00
author = "Pandurang Patil"
tags = [ "Java", "JDK", "wget",]
+++
Many a times we have to download `JDK`/`JRE` on remote machine through console. In most of the cases we tend to download it on our desktop and then upload it to the remote machine through `SCP` as the download link from Oracle website are not directly accessible. You need to first accept the agreement so that you get the download link. The link is not usable to download it using `wget` directly. It seems oracle site look at a cookie value which marks given download request as user's acceptance of agreement. And that cookie is

```
    Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F
```

Now you can download it using wget by passing this cookie with required download link as follows

```
    wget --header "Cookie:gpw\_e24=http%3A%2F%2Fwww.oracle.com%2F" http://download.oracle.com/otn-pub/java/jdk/7u51-b13/jdk-7u51-linux-x64.tar.gz
```