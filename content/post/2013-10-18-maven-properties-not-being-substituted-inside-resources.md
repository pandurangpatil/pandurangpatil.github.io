+++
title = "maven properties not being substituted inside resources"
slug = "2013-10-18-maven-properties-not-being-substituted-inside-resources"
published = 2013-10-18T10:09:00-07:00
author = "Pandurang Patil"
tags = [ "maven", "properties",]
+++
<span
style="font-family: Helvetica Neue, Arial, Helvetica, sans-serif;">You
need to add following configuration which indicates those resources need
to be processed and property values will be replaced. By default Maven
resources plug-in will not do property value substitution (filtering),
so it will need to be enabled within the &lt;build&gt; section of the
pom.xml file. Filtering value true will enable the resources processing
and substitute property values. In addition to that o</span><span
style="font-family: 'Helvetica Neue', Arial, Helvetica, sans-serif;">ne
can include / exclude the resources</span>

  
  

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
