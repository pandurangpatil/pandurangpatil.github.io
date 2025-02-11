+++
title = "Open link in new Tab / Window (Html Anchor tag)"
slug = "2014-04-11-open-link-in-new-tab-window-html-anchor-tag"
published = 2014-04-11T20:07:00-07:00
author = "Pandurang Patil"
tags = ["html", "Anchor"]
+++
To Open respective page pointed by hyperlink in new tab or window one need to make use of target attribute for more details [refer](http://www.w3schools.com/tags/att_a_target.asp). As per below description following configuration will help you to control where a respective link will be displayed.


| Value    | Description |
| :------- | :---------- |
| _blank   | Opens the linked document in a new window or tab    |
| _self    | Opens the linked document in the same frame as it was clicked (this is default)     |
| _parent  | Opens the linked document in the parent frame    |
| _top     | Opens the linked document in the full body of the window    |
| framename  | pens the linked document in a named frame    |

Sometimes you have to open a link inside new tab e.g. deep linked help pages on different pages of your application. But while doing that you don't want to annoy user by opening each link inside new tab. Instead you can open the link in new tab for very first time link, further links will be opened / displayed into same new tab created when user clicked on very first link. To achieve this you need to specify target as some unique string other than above mentioned values which starts with.

    <a target="help-tab" href="http://pandurangpatil.com/sample/help/firstchapter.html">First Help</a>


    <a target="help-tab" href="http://pandurangpatil.com/sample/help/secchapter.html">Second Help</a>

