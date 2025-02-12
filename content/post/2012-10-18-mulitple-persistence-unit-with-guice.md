+++
title = "Mulitple persistence Unit with Guice"
slug = "2012-10-18-mulitple-persistence-unit-with-guice"
published = 2012-10-18T05:57:00.002000-07:00
author = "Pandurang Patil"
tags = [ "Google", "Guice", "DI"]
+++
If you want to use `Guice` with multiple persistence Unit. Then its not much difficult task to do it, `Guice's` official wiki document says it all [refer](http://code.google.com/p/google-guice/wiki/GuicePersistMultiModules). But I feel it has missed out most important part from it i.e. to expose dependencies, if those dependencies need to be used outside the scope of give `PrivateModule`.  
  
Note : I have created a complete working sample with multiple persistent unit refer - https://github.com/pandurangpatil/guice-gwt/ for the code. This sample mainly demonstrates integration of `Guice` with `GWT` but I have added multiple persistent unit sample in the same.  
  
Lets take the same example to understand how to use multiple persistent unit. In this sample there are two persistent units `Address` and `User` each having one entity `Address` and `Person` respectively ( I have taken single entities in each persistent unit for the sake of simplicity). You have separate `DAO` created to manage each of the persistent unit. In this example we have `AddressDao` and `PearsonDao`. As per [document](http://code.google.com/p/google-guice/wiki/GuicePersistMultiModules) you need to bind dependencies with their respective private module.

e.g.  
  
I have created `AddressPersistModule` and `UserPersistModule` each of them is separate private module loading `Address` and `User` persistence unit respectively and bind `Dao` in respective module.  
  
  

     public class UserPersistModule extends PrivateModule {  
          @Override  
          protected void configure() {  
               install(new JpaPersistModule("users"));  
               bind(PersistenceLifeCycleManager.class).annotatedWith(  
                         UserPersistService.class).to(  
                         UserPersistenceLifeCycleManager.class);  
               expose(PersistenceLifeCycleManager.class).annotatedWith(  
                         UserPersistService.class);  
               bind(PersonDao.class).asEagerSingleton();  
               expose(PersonDao.class);  
          }  
     }  

  
  

     public class AddressPersistModule extends PrivateModule {  
          @Override  
          protected void configure() {  
               install(new JpaPersistModule("addresses"));  
               bind(PersistenceLifeCycleManager.class).annotatedWith(  
                         AddressPersistService.class).to(  
                         AddressPersistenceLifeCycleManager.class);  
               expose(PersistenceLifeCycleManager.class).annotatedWith(  
                         AddressPersistService.class);  
               bind(AddressDao.class).asEagerSingleton();  
               expose(AddressDao.class);  
          }  
     }  

  
In respective `Dao` you can inject `EntityManager`, and `Guice` will take care of injecting respective EntityManager for required Persistent Unit. (Note: you will find some different mechanism in above mentioned sample code. but even if you inject just `EntityManager` it will work seamlessly as per mentioned in [document).](http://code.google.com/p/google-guice/wiki/GuicePersistMultiModules)  
  
Now in above code you will notice we have to expose `AddressDao` and `PersonDao` from their respective private modules. Because of which those dependencies will be available globally in given parent injector.  
  
Now you can create the injector like  
  

     Injector injector = Guice.createInjector( new UserPersistModule(), new AddressPersistModule(), ... any other modules );  

  
You will have other dependencies configured in different modules and you can inject exposed private module dependencies with them. In this way you can have service class which will have `AddressDao` and `PersonDao` injected into it and you can use them at single place. Refer below code  

     public class PersonService {  
          @Inject  
          private Injector injector;  
          public boolean savePerson(Person p) {  
               PersonDao pd = injector.getInstance(PersonDao.class);  
               pd.savePerson(p);  
               return true;  
          }  
         .  
         .  
         .  
         .  
          public boolean saveAddresss(String personId, List<Address> addresses) {  
               AddressDao ad = injector.getInstance(AddressDao.class);  
               for (Address address : addresses) {  
                    if (address.getId() == null || "".equals(address.getId())) {  
                         address.setId(java.util.UUID.randomUUID().toString());  
                    }  
                    address.setPersonId(personId);  
                    ad.saveAddress(address);  
               }  
               return true;  
          }  
     }
