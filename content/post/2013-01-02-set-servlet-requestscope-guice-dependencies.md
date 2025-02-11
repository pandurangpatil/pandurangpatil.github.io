+++
title = "Set Servlet RequestScope Guice dependencies"
slug = "2013-01-02-set-servlet-requestscope-guice-dependencies"
published = 2013-01-02T07:13:00.005000-08:00
author = "Pandurang Patil"
tags = [ "Google", "Guice",]
+++
Set some commonly used dependencies which are dependent on some
parameter of HTTP Request.  
  
The most common use case is to add logged in user context in request
scope from session id inside filter. To do that you need to bind such a
dependency inside your ServletModule like following.  
  

     bind(User.class).annotatedWith(Names.named("user")).to(User.class).in(ServletScopes.REQUEST);  

  
You are just binding a given User.class with @Named("user") annotation
inside RequestScope. Now you have to take care of setting required value
when request is made. Which can be achieved by using Servlet filter as
follows.  
  

    1:  public class AuthCheckFilter implements Filter {  
    2:       @Override  
    3:       public void destroy() {  
    4:       }  
    5:       @Override  
    6:       public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {  
    7:            HttpServletRequest httpRequest = (HttpServletRequest) request;  
    8:            .....< Code to retrieve session from request either through query param,   
    9:            cookie or HTTP header and validate the session.   
    10:            session is not valid throw error as per application specific requirement>.....  
    11:            User us = ...<code to retrieve user from session>  
    12:            httpRequest.setAttribute(Key.get(User.class, Names.named("user")).toString(), us);  
    13:            chain.doFilter(httpRequest, response);  
    14:       }  
    15:       @Override  
    16:       public void init(FilterConfig arg0) throws ServletException {  
    17:       }  
    18:  }  

  
Note: We are setting User object for @Named("user") dependency at line
no 12. When you set the user value inside httpRequest object as
attribute.  
  
Now that we have set the value. We can access it or inject it  
  

    1:  @Singleton  
    2:  public class SomeDao {  
    3:    @Inject  
    4:    @Named("user")  
    5:    Provider<User> user;  
    6:    public void someMethod() {  
    7:      User user = user.get();  
    8:    }  
    9:  }  

  
As it is request scoped dependency you need to access / inject it
through Provider.  
  
http://code.google.com/p/google-guice/wiki/ServletModule refer Using
RequestScope section.
