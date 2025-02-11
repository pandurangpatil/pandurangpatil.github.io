+++
title = "GWT Jquery integration"
slug = "2014-05-20-gwt-jquery-integration"
published = 2014-05-20T23:38:00-07:00
author = "Pandurang Patil"
tags = [ "GWT", "Jquery",]
+++
It is very easy to have GWT Jquery integration using [gwtquery](http://code.google.com/p/gwtquery/). Follow below
steps
Add maven dependency for `gwtquery`, at the time of writing this article it
was 1.4.2 and tested it with GWT 2.5.0 version.

    <dependency>
        <groupId>com.googlecode.gwtquery</groupId>
        <artifactId>gwtquery</artifactId>
        <version>1.4.2</version>
        <scope>provided</scope>
    </dependency>

Then inherit your module from required gwtquery module.

    <inherits name='com.google.gwt.query.Query'/>

User jquery api wrappers as follows.

    import static com.google.gwt.query.client.GQuery.$;
    ..
    ...
    public class GwtJquery implements EntryPoint {

        @Override
        public void onModuleLoad() {
            $("#startup").fadeIn(1000);
            $("#product").delay(2000).fadeIn(1000);
        }
    ...
    ...
    }

  
For More details refer [getting started](http://code.google.com/p/gwtquery/wiki/GettingStarted)
