+++
title = "GWT browser specific css "
slug = "2014-05-20-gwt-browser-specific-css"
published = 2014-05-20T23:52:00.001000-07:00
author = "Pandurang Patil"
tags = [ "GWT",]
+++
Yea it is possible to write browser specific css with GWT application which
uses CSS through CssResource. 

    @if user.agent gecko1_8 {
        .startup p {
            color: #000000;
            text-shadow: 0 0 3px #000000;
        }
    } @else {
        .startup p {
            color: #000000;
        }
    }


Note: You can use this logical if else and many more other expression inside css which are used inside GWT code. Only through CssResource interface. If you are directly using the respective css inside html main source
file then this will not work.

For more details [refer](http://www.gwtproject.org/doc/latest/DevGuideClientBundle.html#CssResource)
