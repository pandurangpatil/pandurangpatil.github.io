+++
title = "Java: Add shutdown hook invoked even with CTRL + C"
slug = "2014-04-16-java-add-shutdown-hook-invoked-even-with-ctrl-c"
published = 2014-04-16T09:15:00.004000-07:00
author = "Pandurang Patil"
tags = ["Java"]
+++

Add Shutdown hook with JVM, which will be invoked even when application is killed by pressing `CTRL + C`

Create a separate class which extends `java.lang.Thread` class or implements `java.lang.Runnable` interface


    public class AppShutDownHook extends Thread {
        @Override
        public void run() {
            // TODO: Complete your shutdown activity here.
        }
    }

Register this thread with Java Runtime in your code where your application is getting initialised. Most probably inside main.

    public static void main(String[] args) {
        AppShutDownHook shutDownHook = new AppShutDownHook();
        Runtime.getRuntime().addShutdownHook(shutDownHook);
            .
            . 
            .
            . 
    }

