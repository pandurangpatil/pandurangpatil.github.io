+++
title = "Get New line after using float:left or right"
slug = "2012-05-20-get-new-line-after-using-float-left-or-right"
published = 2012-05-20T11:27:00.001000-07:00
author = "Pandurang Patil"
tags = [ "html", "css", "styling",]
+++
To get new line after using float property on previous element. I found straight forward solution to use either `clear: both;` on next element.  

e.g.  

    1:  <div style=“float: left;">
    2:  	....  
    3:  </div>  


    1:  <div style=“clear: both;">
    2:  	....  
    3:  </div>  

  
for more details [refer](http://www.positioniseverything.net/easyclearing.html)
