+++
title = "Set Servlet RequestScope Guice dependencies"
slug = "2013-01-02-set-servlet-requestscope-guice-dependencies"
published = 2013-01-02T07:13:00.005000-08:00
author = "Pandurang Patil"
tags = [ "Google", "Guice",]
+++
Set some commonly used dependencies which are dependent on some parameter of `HTTP` Request.  
  
The most common use case is to add logged in user context in `request scope` from `session id` inside filter. To do that you need to bind such a dependency inside your `ServletModule` like following.  
  

     bind(User.class).annotatedWith(Names.named("user")).to(User.class).in(ServletScopes.REQUEST);  

  
You are just binding a given `User.class` with `@Named("user")` annotation inside `RequestScope`. Now you have to take care of setting required value when request is made. Which can be achieved by using `Servlet filter` as follows.  
  

    public class AuthCheckFilter implements Filter {  
        @Override  
        public void destroy() {  
        }  
        
        @Override  
        public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {  
            HttpServletRequest httpRequest = (HttpServletRequest) request;  
            .....< Code to retrieve session from request either through query param, cookie or HTTP header and validate the session. session is not valid throw error as per application specific requirement>.....  
            User us = ...<code to retrieve user from session>  
            httpRequest.setAttribute(Key.get(User.class, Names.named("user")).toString(), us);  
            chain.doFilter(httpRequest, response);  
        }  
        
        @Override  
        public void init(FilterConfig arg0) throws ServletException {  
        }  
    }  

  
Note: We are setting `User` object for `@Named("user")` dependency at line `no 12`. When you set the user value inside `httpRequest` object as attribute.  
  
Now that we have set the value. We can access it or inject it  
  

    @Singleton  
    public class SomeDao {  
        @Inject  
        @Named("user")  
        Provider<User> user;  
        public void someMethod() {  
            User user = user.get();  
        }  
    }  

  
As it is request scoped dependency you need to access/inject it through Provider.  
  
http://code.google.com/p/google-guice/wiki/ServletModule refer Using `RequestScope` section.
