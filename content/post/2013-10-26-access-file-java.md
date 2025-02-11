+++
title = "Access file (JAVA)"
slug = "2013-10-26-access-file-java"
published = 2013-10-26T11:23:00-07:00
author = "Pandurang Patil"
tags = [ "java", "fileIO"]
+++
**Access resource / file packaged inside a jar or a located on
classpath.**
Two ways to access the file located inside jar or located on classpath.


1.  <span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">Use
    <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">getResourceAsStream("filename")</span>
    on ClassLoader, one can retrieve the class loader instance from
    class instance of any class or <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">Thread.currentThread().getClassLoader()</span>.
    When you try to load the file using class loader, file will be
    always searched inside root folder on classpath. e.g </span>  
    <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">Thread.currentThread().getClassLoader().getResourceAsStream("config.properties")
    <span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">and</span>
    </span><span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">Thread.currentThread().getClassLoader().getResourceAsStream("/config.properties")</span><span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">
    either way class loader will try to search file from root folder
    which is on class path or from root folder inside jar.</span>
2.  <span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">User
    <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">getResourceAsStream("filename")</span>
    on Class instance of a class. One can retrieve the class instance
    using <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">ClassName.class</span>
    or <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">this.getClass()</span>.
    When you try to load the file using class, file search will depend
    on how do you specify the file name. When you specify file <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">"config.properties"</span>
    <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">this.getClass().getResourceAsStream("config.properties")</span>,
    file will be searched inside same package as that of given class on
    which you are calling <span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">getResourceAsStream()</span>.
    When you specify file like </span><span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"><span
    style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"><span
    style="font-family: &quot;Courier New&quot;,Courier,monospace;">"/config.properties"</span></span>
    given file will be searched from root folder which is on class path
    or from root folder inside jar.</span>

<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;">**Access
resource / file from file location**</span>  
  
<span
style="font-family: &quot;Helvetica Neue&quot;,Arial,Helvetica,sans-serif;"> 
To access file form given path outside the class path, one need to make
use of <span
style="font-family: &quot;Courier New&quot;, Courier, monospace;">java.io.File</span>


    File file = new File(“filename with absolute path”);
    FileInputStream fStream = new FileInputStream(file);   
