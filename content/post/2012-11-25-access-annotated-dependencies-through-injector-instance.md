+++
title = "Access annotated dependencies through injector instance"
slug = "2012-11-25-access-annotated-dependencies-through-injector-instance"
published = 2012-11-25T00:56:00.002000-08:00
author = "Pandurang Patil"
tags = [ "Google", "Guice"]
+++
Following sample will demonstrate how to access guice dependency
annotated with some annotation through direct Guice injector instance.  
  
Bar.java  
  

     import java.lang.annotation.Retention;  
     import java.lang.annotation.RetentionPolicy;  
     import com.google.inject.BindingAnnotation;  
     @Retention(RetentionPolicy.RUNTIME)  
     @BindingAnnotation  
     public @interface Bar {  
     }  

  
Foo.java  
  

     import java.lang.annotation.Retention;  
     import java.lang.annotation.RetentionPolicy;  
     import com.google.inject.BindingAnnotation;  
     @Retention(RetentionPolicy.RUNTIME)  
     @BindingAnnotation  
     public @interface Foo {  
     }  

  
TestDepdency.java  
  

     public interface TestDepdency {  
          String getValue();  
     }  

  
FooTestDependencyImpl.java  
  

     public class FooTestDependencyImpl implements TestDepdency {  
          @Override  
          public String getValue() {  
               return "Foo";  
          }  
     }  

  
BarTestDependencyImpl.java  
  

     public class BarTestDependencyImpl implements TestDepdency {  
          @Override  
          public String getValue() {  
               return "Bar";  
          }  
     }  

  
Test.java  
  

     import com.google.inject.AbstractModule;  
     import com.google.inject.Guice;  
     import com.google.inject.Injector;  
     import com.google.inject.Key;  
     public class Test {  
          public static void main(String[] args) {  
               Injector injector = Guice.createInjector(new AbstractModule() {  
                    @Override  
                    protected void configure() {  
                         bind(TestDepdency.class).annotatedWith(Foo.class).to(FooTestDependencyImpl.class);  
                         bind(TestDepdency.class).annotatedWith(Bar.class).to(BarTestDependencyImpl.class);  
                    }  
               });  
               TestDepdency foo = injector.getInstance(Key.get(TestDepdency.class, Foo.class));  
               System.out.println(foo.getValue());  
               TestDepdency bar = injector.getInstance(Key.get(TestDepdency.class, Bar.class));  
               System.out.println(bar.getValue());  
          }  
     }  

  
  
Final output  
  

     Foo  
     Bar  

  
  
In the similar way you can retrieve the annotated provider.
