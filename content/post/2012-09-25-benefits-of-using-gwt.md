+++
title = "Benefits of using GWT"
slug = "2012-09-25-benefits-of-using-gwt"
published = 2012-09-25T07:44:00.001000-07:00
author = "Pandurang Patil"
tags = [ "GWT", "JSP", "GoogleWebToolkit",]
+++
I have been exploring GWT for 4 years now. I have seen it enhancing and improving year over year. I have also used it in few of my projects. After using it for long I see following benefits of using GWT. I have added these point based on my experience after using GWT. So I might be wrong on some points please feel free to add your comments about the
same. I would be more than happy to understand other angles of given point. As I feel there is lot I have to learn in this space.

1. Every JSP call made to server takes some CPU cycles of server to execute the JSP and return the results. Results will be mostly in the form of HTML.

2. In case of GWT it's up to you as developer which calls needs to be evaluated by server. You can create an application with single HTML/JSP page loaded once and rest of the pages are generated on client side i.e. on browser side. Your application only have to make data calls back to the server. If your application is very big with lot of screens, you can make use of lazy loading of JavaScript. If you feel your application would become heavy then you can create multiple modules and divide the number of screens in different modules.

3.  The advantage you get with GWT is distribution of work load across individual user's browser for generation of HTML. Which in case of JSP has to be borne by the server. Even if you cache the JSP results on server, still there is a cost involved in making a call to server and server has to at least flush the cached HTML. In normal JSP based application, with increase in number of users, load on your server also increases drastically as more requests will be processed by server to serve HTML's. In turn increase in cost of Hardware. In case of GWT or any other JavaScript library your application load gets distributed across multiple browsers (clients) to generate HTML. So if user base increases, load on server should not increase that much in comparison with that of JSP application ( it also depends on how big and heavy data processing your application is doing on server side. If you are doing some heavy data processing on server then in that case even if you use `GWT` with increase in number of users your hardware cost may increase) server only need to handle data calls.

4. As `GWT` client application is written in `Java`, one get an opportunity to catch syntactical mistakes at compile time because of the same (Though it doesn't support all the `JRE` classes as those features are not supported by the browsers itself). Lets take an example to understand what I am saying. If you misspell a `JavaScript` variable name by using pure `JavaScript` library. The only way you can catch such mistake is to run the application and test for desired results.

5. `Java` features like `Generics` and `Annotations` can be used in your application.

6. One can make use of existing available libraries or write one to generate code as per requirement with ease as the code that need to be generated need to be in `Java`. `GWT` compiler takes care of compiling it and converting it in to `JavaScript`.

7. Management of code becomes more easier.

8. One can simply write some common business logic in a such way that it can be used in `GWT` client side code and also on server side code as its in Java e.g. validation of data or some common utility functions.

9. With the use of `GWT` eclipse plug-in, you can easily debug the client code in `Java` for your business logic. 

10. As `GWT` compiler compiles your client `Java` code and generates `JavaScript` out of it. Which you need deploy it to your server, and it gets served and executed in user browser when requested. While generating this `JavaScript` it will do some optimisations. 

-   It doesn't consider dead code while generating `JavaScript`, when I say dead code I mean to say `code which is there but not getting called from main flow`. In turn reduces the effective size of your final `JavaScript` code.
-   It takes care of `obfuscating` generated `JavaScript` code.
-   It does `minification` of generated `JavaScript` code.
-   And more importantly it will generate browser specific optimised code separately. When I say separately, it will generate browser specific separate `JavaScript` which will be served when respective request is received from given browser. Which in turn reduces the size of the `JavaScript` code which gets downloaded for specific browser as it doesn't contain all browser specific handling in one single code.
    

11. If you are writing your application for different languages i.e. English,
Hindi, Marathi etc by using Internationalisation feature of `GWT`. While generating `JavaScript` code it creates copy per language and browser combination. Which makes generated `JavaScript` code for given combination of language and browser most optimal and small one.

12. In case you need to use direct `JavaScript` which can be called from `Java GWT` code one can do it using [JSNI](https://developers.google.com/web-toolkit/doc/latest/DevGuideCodingBasicsJSNI) `(JavaScript Native Interface)`. One can even call `GWT Java` Code back from `JavaSctipt`.

13. If you want to make Bookmark able pages then you can make use of [History](https://developers.google.com/web-toolkit/doc/latest/DevGuideCodingBasicsHistory) feature of `GWT`.

14. If you want to make use of JSON as data format for communication and manipulation it has very good feature called [JavaScript Overlay Types](https://developers.google.com/web-toolkit/doc/latest/DevGuideCodingBasicsOverlay).

15. [Deferred Binding](https://developers.google.com/web-toolkit/doc/latest/DevGuideCodingBasicsDeferred) feature of `GWT` is a good feature which I suppose is possible to provide because of `Java`.

16. You can build your user interface using available widgets of `GWT` in `Java Swing` style. You can even create your custom widgets very easily.

17. If you want to build your user interface ( Web pages ) in pure html style, you can make use of [Declarative
UI](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiBinder) feature of `GWT`. Which I feel one of the major feature of `GWT`. Which makes it easier for developer to build pages in pure `HTML` style. Which I suppose is more maintainable than Swing style coding. And most importantly you can still have your logic in `Java` and only presentation part in pure `HTML`. (Note: which ever method you use (Declarative UI or Swing Style) ultimately its going to be `HTML` only but what makes difference is the way you code and maintain it).

18. [Client Bundle](https://developers.google.com/web-toolkit/doc/latest/DevGuideClientBundle) feature of `GWT` makes it very easy to manage your other web resources like `css`, `images` and other text contents.

-   [CSS resources](https://developers.google.com/web-toolkit/doc/latest/DevGuideClientBundle#CssResource) makes it possible to have conditional logic inside your `css`. You can also access some dynamic values from you `GWT` client side `Java` code. It will also take care of obfuscating your css classes. And most importantly `GWT` has automated generation of interfaces from your `css` files to use `css` classe's. 
-   [Image resource](https://developers.google.com/web-toolkit/doc/latest/DevGuideClientBundle#ImageResource) makes it easier for developer to use images in your application in very easily maintainable fashion. When I say easily I mean to say when you want to use images in `GWT Java` code rather than using hard coded URL, you can use image resource. Benefit you will get using image resource is if you are going to change the location or use some different image with different name you just need to change it at one location. More important feature of image resource is when you use it with `CSS` resource as sprite. It will take care of making that image as in-line [data uri](http://en.wikipedia.org/wiki/Data_URI_scheme). I don't say its not possible to do it with other frameworks what's more important is how fast and easily you can do it. `GWT` makes it much easier for you.
-   [Data Resource](https://developers.google.com/web-toolkit/doc/latest/DevGuideClientBundle#DataResource) add some optimisation for data files like `.pdf` to rename those files based on their contents to make it strongly cacheable by browser. Small data files may be converted in to in-line [data uri](http://en.wikipedia.org/wiki/Data_URI_scheme). 
-   By making use of `Client Bundle` for other web resources and if you properly structure you application into different modules. It can become completely reusable modules as whole with every resource. What's the big deal about reusable modules? well if you are using images by using direct URL in some module. And if you include that module in other module and try to use the components created in that module you still need to have those images copied to public URL of your final application. Which you don't have to do it if you use those images as image resources.
-   Other optimisation you can achieve by creating small modules by using client bundle for `css` and `images`. Where you can chose to include only required modules inside your final module/s. The difference it will make is final module JavaScript and other resources will only contain required contents and not the whole contents even if you want to use small piece of the module.

19. [Cell Widgets](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiCellWidgets): To present paginated data collection `GWT` has Cell Widgets. There are widgets like `CellTable`, `CellList`, `CellTree` and `CellBrowser`.

-   [CellTable](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiCellTable) is meant for presenting data in paginated table format, it has feature where in you can change the contents of given `cell` in place. It supports pagination on client side and server side both, it support sorting on column and also it supports selection of one or multiple records and generating events for the same.
-   [CellList](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiCellWidgets#celllist) can be used to present data in list format and items can displayed in [custom format](http://gwt.google.com/samples/Showcase/Showcase.html#!CwCellList). It also supports client and server side pagination and selection of one or multiple records and generates events for selection.
-   [CellTree](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiCellWidgets#celltree) and
    [CellBrowser](https://developers.google.com/web-toolkit/doc/latest/DevGuideUiCellWidgets#cellbrowser) can be used to present data in tree format.

20. Communication with server from `GWT` client code. It supports multiple ways to implement client server communication.

-   If you are not concerned about the protocol being used for data transfer then it provides GWT [RPC](https://developers.google.com/web-toolkit/doc/latest/DevGuideServerCommunication#DevGuideRemoteProcedureCalls) mechanism. Its very easy to integrate your client side code for data transfer with server. You can define custom `DTO's` (data transfer object) in client code which can be even used on server side code. Server side implementation accepts the same `DTO's` as parameter or return value. Everything else is taken care by `GWT RPC` frame work. It even propagates exceptions raised from server side code to caller in client side code (Provided you need to define those Exception classes inside client side code package. `GWT RPC` internally makes use of `AJAX` calls with their own custom protocol for data transfer.
-   If you don't want to use `GWT RPC` you can make server `AJAX` calls to fetch data from server using [Request Builder](https://developers.google.com/web-toolkit/doc/latest/DevGuideServerCommunication#DevGuideHttpRequests). Which is also much easier to implement.
-   It also has interesting feature [Request Factory](https://developers.google.com/web-toolkit/doc/latest/DevGuideRequestFactory). With this feature you can make your `DAO` or `Service` layer exposed to get called from client code. To do that you need define few set of interfaces for your service and custom data types. And using these interfaces you can access those services from client code. I have written maven plugin to generate these interface. If you annotate your `DAO` layer with some required annotations [refer](https://github.com/pandurangpatil/gwt-mvn-helper) refer `mvn-helper-test` module inside it for usage. `RequestFactory` is more targeted to integrate with `ORM` layer like `JDO` or `JPA` on server. It has a support to call persist on given entity from client code. And most important when you call persist method it compute and send only change (delta) to server to save.
-   If you want to make cross domain JSONP call you can do the same [refer](https://developers.google.com/web-toolkit/articles/using_gwt_for_json_mashups).

21. Logging

22. Junit

23. Deployment
