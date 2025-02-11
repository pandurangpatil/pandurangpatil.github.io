+++
title = "Start with maven"
slug = "2012-06-28-start-with-maven"
published = 2012-06-28T09:06:00.004000-07:00
author = "Pandurang Patil"
tags = [ "mvn", "maven"]
+++
**Start with Maven**
  
To start with Maven lets create a sample application which will result into artifact packaged into `.jar`. Maven being build system for Java application, you need to have following software's installed on your machine and set few environment variables.  

-   JDK may be latest version at least `jdk 1.6`.
-   Maven installation [download](http://maven.apache.org/download.html) latest version.
-   Set Maven's bin directory into path variable so that it is accessible from anywhere.
-   Set `JAVA_HOME` environment variable pointing to required JDK installation

It is very easy to create simple jar project with the help of Maven [archetype](http://maven.apache.org/guides/introduction/introduction-to-archetypes.html) (in short it is a Java project templating tool, which has different
templates to create different kinds of projects. Which makes it easier for developer to setup the required project quickly with bare minimal configuration)  

    1:  mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart  
  
When you run above command it will run a wizard which will ask you few inputs following are the details for the same.  
  
    1:  Define value for property 'groupId': : com.sample  

A. **groupId:** you need to provide meaningful group id to your `module/artifact`. `Group Id` is something which will help you categorize your artifacts. So when you have multiple modules you have clear segregation of those modules. It acts like namespace or package (most prominently similar to package concept inside java).  

    1:  Define value for property 'artifactId': : test  
  
B. **artifactId:** You need to provide some meaningful name to your `module/project/artifact`.  

    1:  Define value for property 'version': 1.0-SNAPSHOT: :  
  
C. **version:** You need to provide the version for given module/project. It shows default value as `1.0-SNAPSHOT`. Will explain in detail in my next blog what's the meaning of `SNAPSHOT`. In short when you are developing your code and it is under development for long time. You should keep the version of your module in prefixed with `-SNAPSHOT`.  

    1:  Define value for property 'package': com.sample: :  


D. **package:** This input is not exactly related to artifact. When I say exactly related it means its not part of the requirement to define a `module/project` in maven. This is being asked by this archetype is because this is quick start template. So it creates a sample project with sample `Hello World` app, to place the required Java class, it will
ask you to provide some package name. As default value it will assume value of the groupId you have provided previously.  
  
Once you enter all the values required by the wizard, it will show you entered values for required parameters and will ask you to confirm the same. Once you confirm the inputs. It will create a sample `module/project` with given input.  
  
If you look into directory from where you run this quick start archetype, it must have created a directory with the same name as that of artifactId. And directory structure under that directory will be as follows  
  

    1:  test  
    2:  |-- pom.xml  
    3:  `-- src  
    4:    |-- main  
    5:    |  `-- java  
    6:    |    `-- com  
    7:    |      `-- sample  
    8:    |        `-- App.java  
    9:    |            
    10:    `-- test  
    11:      `-- java  
    12:        `-- com  
    13:          `-- sample  
    14:            `-- AppTest.java  

  
This quick start archetype creates a jar module. When I say jar module, packaging type of the module will be `jar`.  
  
To make a build from command prompt. Follow below commands.  
  

    1:  $ cd test  
    2:  $ mvn clean package  

  
This will make a build, Maven creates target folder inside respective module folder, to generate build output, once you run above command to build the module. You will find a jar created inside `test/target` folder with the name `test-1.0-SNAPSHOT.jar`. So final artifact will be generated as `<artifactId>-<version>.jar` for jar packaging type. One can override the default name with their own name by using `<finalName>` tag inside `<build>` tag inside your `pom.xml` file (refer [pom reference](http://maven.apache.org/pom.html)).  
  
To test the application which just compiled run following command  
  

    1:  $ java -cp target/test-1.0-SNAPSHOT.jar com.sample.App  

  
This should print out as  
  

    1:  Hello World!  

  
  
For more details refer [getting started guide](http://maven.apache.org/guides/getting-started/index.html) and
[maven in 5 mins](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).  
  
To import the maven project inside eclipse to setup eclipse project [refer](http://blog.pandurangpatil.com/2011/08/setup-eclipse-project-from-maven.html)
