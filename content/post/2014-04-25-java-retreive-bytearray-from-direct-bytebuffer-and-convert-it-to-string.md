+++
title = "Java: Retreive ByteArray from Direct ByteBuffer and convert it to String"
slug = "2014-04-25-java-retreive-bytearray-from-direct-bytebuffer-and-convert-it-to-string"
published = 2014-04-25T06:45:00-07:00
author = "Pandurang Patil"
tags = ["Java"]
+++
I assume you understand what is [Direct ByteBuffer](http://docs.oracle.com/javase/7/docs/api/java/nio/ByteBuffer.html). I was trying to retrieve `byte[]` from Direct ByteBuffer

    ByteBuffer buffer = ByteBuffer.allocateDirect(10000);
    .....
    .....
    buffer.flip();
    byte[] data = buffer.array();

and I was getting this error

    Exception in thread "main" java.lang.UnsupportedOperationException
     at java.nio.ByteBuffer.array(ByteBuffer.java:959)

I was able to solve this as follows

    ByteBuffer buffer = ByteBuffer.allocateDirect(10000);
    .....
    .....
    buffer.flip();
    byte[] data = new byte[buffer.remaining()];
    buffer.get(data);
    // Here you hava data populated inside data[] array
    String token = new String(data);

