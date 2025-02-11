+++
title = "Remove cookie."
slug = "2014-02-09-remove-cookie"
published = 2014-02-09T02:02:00.003000-08:00
author = "Pandurang Patil"
tags = [ "remove", "cookie"]
+++
To remove cookie from server one need to set its expiry time to current
time.  
  
e.g. J2EE container one can remove the cookie in following way  
  

    HttpServletResponse response = (HttpServletResponse) servletResponse;
    Cookie cookie = new Cookie("cookie-key", "");
    .... set all the other attributes same as that of existing cookie, like path and domain.  
    cookie.setMaxAge(0);
    response.addCookie(cookie);

  
setting max age of cookie to '0' I am setting its expiry to current
machine time.  
  
JavaScript  
  

    document.cookie = "username=; expires=Thu, 01 Jan 1970 00:00:00 GMT";

  

For more details [refer](http://www.w3schools.com/js/js_cookies.asp)
