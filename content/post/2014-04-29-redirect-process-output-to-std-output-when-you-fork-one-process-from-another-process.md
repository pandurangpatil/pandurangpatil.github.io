+++
title = "Redirect process output to std output when you fork one process from another process."
slug = "2014-04-29-redirect-process-output-to-std-output-when-you-fork-one-process-from-another-process"
published = 2014-04-29T04:58:00.002000-07:00
author = "Pandurang Patil"
tags = ["Java"]
+++
In the situation where you want to redirect input / output of one process to the std input output of parent process (from which you are starting first process). You can make use of inheritIO() method of a ProcessBuilder.

    ProcessBuilder pb = new ProcessBuilder("command", "argument);
    pb.directory(new File(<directory from where you want to run the command>));
    pb.inheritIO();
    Process p = pb.start();
    p.waitFor();

It may not be necessary to call waitFor() method in above code. This will just help to wait current process to wait for this child process to get complete.

There exist few other options as well, through which you can redirect required stream to standard output and input.

    pb.redirectInput(Redirect.INHERIT);
    pb.redirectOutput(Redirect.INHERIT);
    pb.redirectError(Redirect.INHERIT);

