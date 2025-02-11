+++
title = "Advantage of using Maven over ant."
slug = "2012-06-28-advantage-of-using-maven-over-ant"
published = 2012-06-28T09:07:00.001000-07:00
author = "Pandurang Patil"
tags = [ "maven", "ant",]
+++
**What is [Maven](http://maven.apache.org/)?**
  
It is a tool that can be used for build process and managing Java project. The way ant is used for build process of Java projects. But it does it very smartly and you can set-up your Java project very fast.  
  
**Advantage of using [Maven](http://maven.apache.org/) over [Ant](http://ant.apache.org/)**.

-   With ant you have to do everything on your own, you have to write lot of `code/configuration` in `build.xml`. Where as maven is simple, easy and with minimal code you can start.
-   The main important advantage you get is to manage your artifact (could be `.jar` or `.war` ) by way of properly versioned artifactes. And easy way of managing dependencies (as in other libraries required by given project) of of a project.
-   Another advantage it has which is more interesting for people who are using Eclipse as IDE. That is **maven project can be directly imported into Eclipse** with the help of few plugins for more details [refer](http://blog.pandurangpatil.com/2011/08/setup-eclipse-project-from-maven.html). It will setup a required eclipse project by looking at your maven build script. You might say it is possible with ant also you just have to configure Ant builder in Eclipse and one can fire the build from eclipse but it simply calls ant build as it is the way it can be fired through command prompt. But you yourself have to configure and setup project by configuring all of its dependencies. There are ways to import ant build files but it fails to import some complicated ant projects. Where as in case of Maven it doesn't fire maven build as it is the way it will be fired through command prompt. When you import maven project into eclipse it sets up eclipse project on its own by configuring all of its dependencies. It also configures eclipse builders that are used to build given project, which will make it more easier for developers to work in properly configured eclipse project.
-   It has major and important feature to share your artifact with other people required in your company or even you can share with wide audience over Internet with the help of some openly available software tools.
-   It has life cycle phase in which your junits are invoked.
-   It enforces proper arrangement of your source code directories.
-   I have seen in lot of the projects which uses ant as a build tool. Keep all their source files at one location. And generate multiple artifactes from the same source location by including and excluding some packages. This way of managing code makes it more difficult for a new person to understand the code arrangement and what goes in which artifact. This could be bad way of doing things, for which ant should not be blamed. But in contrary Maven don't allow you to generate multiple artifact by including few resources in one artifact and excluding those from others. That way you are forced to create another module and add dependency of that module where ever it is required. That makes your code more readable and segregated and looking at the dependency you can easily make out at what all places it is getting used.

[refer](http://stackoverflow.com/questions/80622/maven-or-ant) this discussion for more detailed insights  
  
look out for my next blog on [Start with maven](http://blog.pandurangpatil.com/2012/06/start-with-maven.html)
