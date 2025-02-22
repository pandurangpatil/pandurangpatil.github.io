+++
title = "Access file (JAVA)"
slug = "2013-10-26-access-file-java"
published = 2013-10-26T11:23:00-07:00
author = "Pandurang Patil"
tags = [ "java", "fileIO"]
+++
**Access resource / file packaged inside a jar or a located on classpath.**
Two ways to access the file located inside jar or located on classpath.


1.  Use `getResourceAsStream("filename")` on ClassLoader, one can retrieve the class loader instance from class instance of any class or `Thread.currentThread().getClassLoader()`. When you try to load the file using class loader, file will be always searched inside root folder on classpath. e.g. `Thread.currentThread().getClassLoader().getResourceAsStream("config.properties")` and `Thread.currentThread().getClassLoader().getResourceAsStream("/config.properties")` either way class loader will try to search file from root folder which is on class path or from root folder inside jar.
2.  Use `getResourceAsStream("filename")` on Class instance of a class. One can retrieve the `class` instance using `ClassName.class` or `this.getClass()`. When you try to load the file using class, file search will depend on how do you specify the file name. When you specify file `config.properties` `this.getClass().getResourceAsStream("config.properties")`, file will be searched inside same package as that of given class on which you are calling `getResourceAsStream()`. When you specify file like `/config.properties` given file will be searched from root folder which is on class path or from root folder inside jar.

**Access resource / file from file location**
  
To access file form given path outside the class path, one need to make use of `java.io.File`


    File file = new File(“filename with absolute path”);
    FileInputStream fStream = new FileInputStream(file);   
