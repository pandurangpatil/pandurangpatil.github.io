+++
title = "Setup eclipse project from a Maven project"
slug = "2011-08-11-setup-eclipse-project-from-a-maven-project"
published = 2011-08-11T07:46:00-07:00
author = "Pandurang Patil"
tags = [ "maven","eclipse"]
+++

Note: Below steps will work for 2.x and later version's of Maven
project.


**Assumption: You know eclipse.**

  

Eclipse version details: I would recommend to use latest version of Eclipse (Helios was the latest version while writing this blog and steps are tried with the same).

  
If you know how to install eclipse plugin then you can skip install steps and install following two plugins 

1. http://m2eclipse.sonatype.org/sites/m2e
2. http://m2eclipse.sonatype.org/sites/m2e-extras

**Install maven eclipse [plug-in](http://m2eclipse.sonatype.org/installing-m2eclipse.html) for more details [refer](http://m2eclipse.sonatype.org/installing-m2eclipse.html).**

Follow below steps to install eclipse plug-in.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-First.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-First.jpg)

-   Click on `Help=> Install New Software`

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-2nd.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-2nd.jpg)


-   Click on `Add` button on `Install` window.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-3rd.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-3rd.jpg)


-   On `Add Repository` window add any meaning full name like in this case `maven` and the corresponding URL for eclipse plugin (http://m2eclipse.sonatype.org/sites/m2e). And click on `Ok` button.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-4th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-4th.jpg)

-   check all required and click on `Next` follow the wizard and finally finish. It will install the plugin.
-   similarly install m2eclipse Extras URL (http://m2eclipse.sonatype.org/sites/m2e-extras). 


Once you install both the eclipse plug-ins for Maven your eclipse is ready to import Maven project. When you install those plug-in's it also installs Embedded Maven and it uses the same for imported projects. If you want to use other version of maven which installed on your machine. You can do the same follow below steps to select installed version of
Maven.

  

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-5th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-5th.jpg)


-   Click on `Window=> Preferences`

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-6th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-6th.jpg)

-   On Preferences window expand `Maven` and select `Installations`.
-   Under `Installations` option click on `Add` to select maven installation installed in previous steps.
-   When you click on `add`, it will pop up a folder browser window. Select the home location of maven installation in that Window.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-7th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-7th.jpg)

-   Once you select the maven installation home folder click on `Apply` and then click on `OK`.

**To setup eclipse project for your maven project follow below steps.**


[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-8th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-8th.jpg)


-   Click on menu `File=> Import...`

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-9th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-9th.jpg)

-   On `Import` Window expand `Maven` tag and select `Existing Maven Projects`. And click on `Next` button.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-10th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-10th.jpg)

-   On `Import Maven Projects` window click on Browse and select your base project folder which contains `pom.xml`. If you have multiple projects with one parent project. Just select the folder of parent project.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-11th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-11th.jpg)

-   Once you select the base folder it will show you the project/projects. Click on `Finish` button. It will setup the required project/projects for you.

[![](../images/thumbnails/2011-08-11-setup-eclipse-project-from-a-maven-project-12th.jpg)](../images/2011-08-11-setup-eclipse-project-from-a-maven-project-12th.jpg)


-   It creates required project as per packaging type. If packaging type is `war` it will create eclipse web project. It will add corresponding resources into source path, add web resource and also add dependencies inside classpath.
