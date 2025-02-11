+++
title = "Override JPA persistence unit properties in code with Google Guice"
slug = "2013-08-06-override-jpa-persistence-unit-properties-in-code-with-google-guice"
published = 2013-08-06T23:20:00-07:00
author = "Pandurang Patil"
tags = [ "JPA","Google", "Guice",]
+++
To override properties from persistence.xml through code while using it
with Google guice. One can read the properties from different source and
add those properties while installing JpaPersistModule. Following is the
sample  
  
  

    1:  Properties persistenceUnit = new Properties();  
    2:  persistenceUnit.put("javax.persistence.jdbc.url", "jdbc:mysql://192.168.9.102/MyDB");  
    3:  persistenceUnit.put("javax.persistence.jdbc.user", "myuser");  
    4:  persistenceUnit.put("javax.persistence.jdbc.password", "mypassword");  
    5:  Injector injector = Guice.createInjector(new JpaPersistModule("my-persistence-unit").properties(persistenceUnit));  

  
  
One can chose to read this configuration from some other file and
install JpaPersistModule with those properties. This could be useful to
override database url for test and production.
