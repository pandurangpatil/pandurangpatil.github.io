+++
title = ".profile is ignored when terminal is started in MAC-OSX"
slug = "2014-04-13-profile-is-ignored-when-terminal-is-started-in-mac-osx"
published = 2014-04-13T10:43:00.002000-07:00
author = "Pandurang Patil"
tags = ["mac", "OSX"]
+++

One fine day suddenly all environment variables that I have set inside `.profile` file of my machine stopped getting declared when machine is restarted.
  
It turns out that if you have `.bash_profile` or `.bash_login` file then `.profile` file will be ignored by bash.
  
So you need to make use of either `.profile` or `.bash_profile` not both of them, if you are using bash. 
