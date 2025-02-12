+++
title = "maven properties not being substituted inside resources"
slug = "2013-10-18-maven-properties-not-being-substituted-inside-resources"
published = 2013-10-18T10:09:00-07:00
author = "Pandurang Patil"
tags = [ "maven", "properties",]
+++
You need to add following configuration which indicates those resources need
to be processed and property values will be replaced. By default `Maven` resources `plug-in` will not do property value substitution (filtering), so it will need to be enabled within the `<build>` section of the `pom.xml` file. Filtering value true will enable the resources processing and substitute property values. In addition to that one can include/exclude the resources


     <build>  
          .....  
          .....  
          <resources>  
               <resource>  
                    <directory>src/main/resources</directory>  
                    <filtering>true</filtering>  
               </resource>  
          </resources>  
          .....  
          .....  
     </build>
