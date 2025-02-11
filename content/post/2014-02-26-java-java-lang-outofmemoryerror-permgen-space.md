+++
title = "Java java.lang.OutOfMemoryError: PermGen space"
slug = "2014-02-26-java-java-lang-outofmemoryerror-permgen-space"
published = 2014-02-26T12:11:00.001000-08:00
author = "Pandurang Patil"
tags = [ "GWT", "PermGen", "OutOfMemoryError"]
+++
**java.lang.OutOfMemoryError: PermGen space**
You get this error that means your JVM is running out of allocated memory
for storing class metadata information (class properties, methods
annotations etc). This space is not cleaned by Garbage Collected by
Garbage collector. When JVM run out of memory for this, it could happen
because of multiple reasons, </span>

1.  <span
    style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;">One
    you are dynamically generating classes and those are getting loaded
    in JVM. </span>
2.  <span
    style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;">Second
    your application is so big and it has more number of dependencies on
    other third party libraries.  Which in turn deploys huge number of
    jars.</span>
3.  <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">Third
    you are deploying multiple modules in the form separate wars
    (multiple war files) inside your application server. Which results
    in loading big number of classes in JVM's memory space.</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">In
either of the case to resolve this issue, you have to first try to
reduce the number of classes / jars that you are deploying with your
application. In some cases I have seen we tend to use multiple
frameworks in the same application when single framework can do the job.
Generally that happens if we don't keep a tap on what all frameworks
getting used in your application and every team member go ahead and add
new framework in application. Because he / she has already used it and
not willing to explore frame work being used currently in project. If we
try, avoid and exclude absolute dependency we can reduce the memory foot
print of the application. Which in turn reduces the possibility of
getting this errors. I also also see one more reason for this error that
is "Maven" which includes dependencies of dependencies some times
dependencies which are not needed. This happens without the knowledge to
the developer.  And it may become tedious to remove / exclude unwanted
dependencies with maven. I don't say it is not possible but it takes
some time.</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">In
some cases if you are deploying multiple applications (.war this in
context of deploying application on single servlet container). Every
application's dependencies will be isolated from each other, and thus it
ends up loading some common jars (across the deployed wars) multiple
times and in turn ends up consuming more memory. In such cases, one can
sort out all common jars across application and deploy them in
containers class path directly e.g. inside jetty you can copy those
common jar in &lt;jetty home&gt;/lib/ext. As well as remove such common
jar from individual war file and then deploy them. Now here there are
some challenges as well as some extra efforts and time you need to put
in to sort those dependencies. When I talk about challenges, I am
talking about situation where there is conflict of versions of
dependencies i.e. one app is used lower version of some library and
other one is using latest version of the same. In such cases you should
keep those dependencies packaged with war only. On extra efforts and
time, it depends on you whether you are ready invest your time or money
on spending more on hardware. (ok I prepared one utility that will scan
all war files, extract common shared jars in one folder and repackage
those war files once again excluding common jar
files [refer](http://www.pandurangpatil.com/2014/03/compare-more-than-two-war-files-and.html))</span>  
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">  
</span> <span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">If
you are developing your front end with GWT, then I have seen all GWT
libraries remain packaged with WAR file. Here I would like to point out
that when you compile your GWT project for deployment, all your GWT
client code has been converted to JavaScript. So you no more require
those classes to be deployed with your application unless those are
being used in backend code as well. And some times it becomes quite
tedious to isolate these classes. So I would suggest you to break down
you application in three modules, one for pure client side GWT code, one
for common code which will be shared across both GWT client side code as
well as backend code and third module will be for pure backend side
code. In this situation you could exclude the dependency or code from
pure GWT module while deployment.</span>  
  

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">After
you try all possibilities and you cannot reduce the memory foot print
you can try increasing the allocated permgen memory with following
options</span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;"><span
style="background-color: #eeeeee; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, serif; font-size: 14px; line-height: 17.804800033569336px; white-space: pre-wrap;">-XX:PermSize=64M
-XX:MaxPermSize=128M</span> Increase memory used for perm gen. Value for
these options you need to do trial and error. </span>

<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
can also try with following options if you are using AOP or dynamically
generating the classes.</span>

-   <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;"><span
    style="background-color: #eeeeee; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, serif; font-size: 14px; line-height: 17.804800033569336px; white-space: pre-wrap;">-XX:+CMSClassUnloadingEnabled</span> :
    Enables garbage collection in permgen </span>
-   <span
    style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">`-XX:+`<span
    style="background-color: #eeeeee; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, serif; font-size: 14px; line-height: 17.804800033569336px; white-space: pre-wrap;">CMSClassUnloadingEnabled</span><span
    style="background-color: white; font-family: Arial, 'Liberation Sans', 'DejaVu Sans', sans-serif; font-size: 14px; line-height: 17.804800033569336px;"> </span> Allows
    garbage collector to remove the classes.  </span>
