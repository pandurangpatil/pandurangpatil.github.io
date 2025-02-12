+++
title = "Singleton Factory"
slug = "2012-11-25-singleton-factory"
published = 2012-11-25T00:16:00.002000-08:00
author = "Pandurang Patil"
tags = [ "SingletonFactory", "Java",]
+++
**Singleton factory for single threaded environment:**  
  
It is simple to create Singleton factory for single threaded application.  
  

     public class SingleThreadSingleton {  
          private static SingleThreadSingleton     instance;  
          private SingleThreadSingleton() {  
               // Initialise  
          }  
          public static SingleThreadSingleton getInstance() {  
               if (instance == null) {  
                    instance = new SingleThreadSingleton();  
               }  
               return instance;  
          }  
     }  

  
**Singleton factory for multi threaded application:**  
  
When you want to create `Singleton` factory for multi threaded application. In which you want single instance to be maintained across all thread. You need to `synchronize` the creation of a instance. In which
case if you `synchronize` the `complete` getInstance method in above example you are creating the bottleneck to access the instance. The requirement is to just synchronize the creation of instance. Following is sample `Singleton` factory for multi threaded application.  
  

    1:  public class MultiThreadSingleton {  
    2:       private static MultiThreadSingleton     instance;  
    3:       private MultiThreadSingleton() {  
    4:            // Initialise  
    5:       }  
    6:       public static MultiThreadSingleton getInstance() {  
    7:            if (instance == null) {  
    8:                 synchronized (MultiThreadSingleton.class) {  
    9:                      if (instance == null) {  
    10:                           instance = new MultiThreadSingleton();  
    11:                      }  
    12:                 }  
    13:            }  
    14:            return instance;  
    15:       }  
    16:  }  

  
As there is possibility that multiple thread calls getInstance method simultenously before instance is initialized. In that case there is possibility that multiple threads get inside initialization `block` ( ref line no. 7). As inside code is synchronized only one thread would get access to it at given instant of time. Other thread will wait till the time first thread release the `lock`. First thread gets a access it will initialize the instance. When first thread goes out of synchronized block other next thread waiting for the access will get inside synchronized `block`. Now if we don't add null check for instance inside synchronized block ( ref line no. 9) the second thread will initialize the instance again. Same will happen if there are more threads waiting for the access. To avoid reinitialization we have to add null check for instance inside Synchronized block also. Once instance is created then there is no need to have synchronization to access the instance.
