+++
title = "Generate complete package (ZIP) of Java (executable jar) application with required dependencies in it using Maven"
slug = "2013-05-17-generate-complete-package-zip-of-java-executable-jar-application-with-required-dependencies-in-it-using-maven"
published = 2013-05-17T07:45:00.002000-07:00
author = "Pandurang Patil"
tags = [ "java", "assembly", "executableJar",]
+++
To generate a zip file, packaging all required dependent libraries and
newly generated jar, using maven-assembly-plugin (for more detail on
plugin
[refer](http://maven.apache.org/plugins/maven-assembly-plugin/index.html)).  
  
I will demonstrate generation of package using assembly descriptor
file.  

1. Create a assembly descriptor file which is a xml file (for more details
    [refer](http://maven.apache.org/plugins/maven-assembly-plugin/examples/single/filtering-some-distribution-files.html) and
    [format](http://maven.apache.org/plugins/maven-assembly-plugin/assembly.html) )
    as following. Create this file inside your project directory. One
    can keep this descriptor file any where inside given project
    directory. I have tried it by keeping this file at location
    &lt;Project dir&gt;/src/main/assembly/test-app-assembly.xml and
    providing complete path to descriptor file in pom.xml.

e.g
  

    1:  <?xml version="1.0" encoding="UTF-8"?>  
    2:  <assembly  
    3:       xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2"  
    4:       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    5:       xsi:schemaLocation="  
    6:    http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.2  
    7:     http://maven.apache.org/xsd/assembly-1.1.2.xsd  
    8:   ">  
    9:       <formats>  
    10:            <format>zip</format>  
    11:       </formats>  
    12:       <files>  
    13:            <file>  
    14:                 <outputDirectory>/</outputDirectory>  
    15:                 <source>target/test-app.jar</source>  
    16:            </file>  
    17:       </files>  
    18:       <!-- use this section if you want to package dependencies -->  
    19:       <dependencySets>  
    20:            <dependencySet>  
    21:                 <outputDirectory>lib</outputDirectory>  
    22:                 <useStrictFiltering>true</useStrictFiltering>  
    23:                 <useProjectArtifact>false</useProjectArtifact>  
    24:                 <scope>runtime</scope>  
    25:            </dependencySet>  
    26:       </dependencySets>  
    27:  </assembly>  

  
2. In above descriptor file, its assumed the current project artifact
    is generated before this plugin gets executed and
    maven-assembly-plugin configured to run in "install" phase only.
3. refer line 12 to 17 in above code. We are specifying include
    generated artifact from the current module inside packaging, which
    will be placed inside root "/" directory of the package zip. Note:
    by default maven generates artifact in following format
    "&lt;artifact name&gt;-&lt;version&gt;.jar" (with assumption
    packaging mentioned as "jar"). You need to make sure to specify
    constant file name using property &lt;finalName&gt; inside your
    pom.xml

e.g 

    1:  <build>  
    2:  ......  
    3:  ....  
    4:        <finalName>test-app.jar</finalName>   
    5:  .......  
    6:  ....  
    7:  </build>  
  

4. Next refer line 19 - 26. Here we are specifying copy all dependency
    jars inside "/lib" directory of the package zip.
5. Next refer below changes in pom.xml.

e.g. 

    1:  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    2:       xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    3:       ......  
    4:      .........  
    5:       <build>  
    6:            <finalName>test-app</finalName>  
    7:            <plugins>  
    8:                 <plugin>  
    9:                      <groupId>org.apache.maven.plugins</groupId>  
    10:                      <artifactId>maven-assembly-plugin</artifactId>  
    11:                      <executions>  
    12:                           <execution>  
    13:                                <id>create-distribution</id>  
    14:                                <phase>install</phase>  
    15:                                <goals>  
    16:                                     <goal>single</goal>  
    17:                                </goals>  
    18:                                <configuration>  
    19:                                     <descriptors>  
    20:                                          <descriptor>src/main/assembly/test-app-assembly.xml</descriptor>  
    21:                                     </descriptors>  
    22:                                </configuration>  
    23:                           </execution>  
    24:                      </executions>  
    25:                 </plugin>  
    26:              ................  
    27:              ................  
    28:            </plugins>  
    29:       </build>  
    30:  </project>  

6. Refer line 8 - 25 in above code from sample pom.xml. Here we are
    configuring maven-assembly-plugin to invoke "single" goal in
    "install" phase by referring test-app-assembly.xml file (refer line
    20).
7. When you run the build "mvn clean install" at the end you will see
    file "test-app.zip" is generated inside target folder. If you open
    the zip file you will find test-app.jar and "lib" folder in it and
    if you go inside lib folder you will find all required dependencies
    of current project are copied inside this "lib" folder.

  

Above steps demonstrates how to generate required single package as zip
with all required dependencies in it. Now we will look at how to make
given application as executable jar (When I say [executable
jar](http://docs.oracle.com/javase/7/docs/technotes/guides/jar/jarGuide.html),
one can configure main class of given application, so that JVM can
invoke the application directly without specifying which class to invoke
on command line. you can run application like "&lt;extracted location of
zip&gt;$ java -jar test-app.jar -classpath &lt;location of each
dependent jar file&gt;"). But its not just sufficient to just specify
only main class, we also need to add required dependent jar files in
class path while running application from command prompt. If we can add
those dependent jar locations inside jar itself then you don't have to
mention it at command line. Refer below code changes using
maven-jar-plugin.

  

    1:  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    2:       xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    3:       ......  
    4:      .........  
    5:       <build>  
    6:            <finalName>test-app</finalName>  
    7:            <plugins>  
    8:                 <plugin>  
    9:                      <groupId>org.apache.maven.plugins</groupId>  
    10:                      <artifactId>maven-assembly-plugin</artifactId>  
    11:                      <executions>  
    12:                           <execution>  
    13:                                <id>create-distribution</id>  
    14:                                <phase>install</phase>  
    15:                                <goals>  
    16:                                     <goal>single</goal>  
    17:                                </goals>  
    18:                                <configuration>  
    19:                                     <descriptors>  
    20:                                          <descriptor>src/main/assembly/test-app-assembly.xml</descriptor>  
    21:                                     </descriptors>  
    22:                                </configuration>  
    23:                           </execution>  
    24:                      </executions>  
    25:                 </plugin>  
    26:                 <plugin>  
    27:                      <groupId>org.apache.maven.plugins</groupId>  
    28:                      <artifactId>maven-jar-plugin</artifactId>  
    29:                      <configuration>  
    30:                           <archive>  
    31:                                <manifest>  
    32:                                     <addClasspath>true</addClasspath>  
    33:                                     <classpathPrefix>lib/</classpathPrefix>  
    34:                                     <mainClass>com.pp.test.Sample</mainClass>  
    35:                                </manifest>  
    36:                           </archive>  
    37:                      </configuration>  
    38:                 </plugin>  
    39:            </plugins>  
    40:       </build>  
    41:  </project>  

  
  

1. refer line 34, here we are specifying which the class having main
    method. At line 32 we are specifying add all dependency jars into
    classpath. But as all the dependent jars we have placed inside "lib"
    folder as per above packaging configuration, while specifying class
    path we need to prefix jar file name with "lib/". This will result
    in generation of META-INF/MANIFEST.MF file refer sample below.

Sample 

     
     Manifest-Version: 1.0  
     Archiver-Version: Plexus Archiver  
     Created-By: Apache Maven  
     Built-By: pandurang  
     Build-Jdk: 1.7.0_17  
     Main-Class: com.pp.test.Sample  
     Class-Path: lib/javapns-2.2.jar lib/junit-4.8.1.jar lib/commons-lang-2.6.jar lib/commons-io-2.4.jar lib/mail-1.4.5.jar lib/activation-1.1.jar lib/google-http-client-jackson2-1.13.1-beta.jar lib/j  
      ackson-core-2.0.5.jar lib/jcommander-1.30.jar lib/log4j-1.2.17.jar lib/slf4j-api-1.6.6.jar   

  

2. With this you will be able to generate complete zip file with an
    executable jar file in it. Which makes the deployment and execution
    of application very easy. For deployment you need to just ship this
    generated "test-app.zip" file which is a complete package. To run
    your application you can extract the zip file and issue following
    command "<span
    style="background-color: #f0f0f0; font-family: arial; font-size: 12px; line-height: 20px;">&lt;extracted
    location of zip&gt;$ java -jar test-app.jar</span>". Note here when
    jar is generated all required dependencies are mentioned inside
    MANIFEST.MF you don't have to specify them here.
