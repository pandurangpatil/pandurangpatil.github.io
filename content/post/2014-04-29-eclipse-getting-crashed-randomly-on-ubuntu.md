+++
title = "Eclipse getting crashed randomly on ubuntu"
slug = "2014-04-29-eclipse-getting-crashed-randomly-on-ubuntu"
published = 2014-04-29T19:02:00-07:00
author = "Pandurang Patil"
tags = ["eclipse", "ubuntu"]
+++
If your eclipse is getting crashed randomly and that too frequently look at the crash reported. This crash report will be placed in the directory from where you start the eclipse and search for `/usr/lib/x86\_64-linux-gnu/gtk-2.0/modules/liboverlay-scrollbar.so`. If find this string then this issues of overlay scrollbar library. This will be solved once you remove that library. Sometimes, you will not find crash report generated, even in that case it is most probably the
issue of overlay scrollbar.


	sudo apt-get remove overlay-scrollbar


for more details refer this [bug](https://bugs.eclipse.org/bugs/show_bug.cgi?id=416869). If you don't find above mentioned string, search google with few strings from that crash report.
