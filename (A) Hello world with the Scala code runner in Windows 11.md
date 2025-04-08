2025-04-08: work in progress

# Installations in Windows 11

Some notes on Scala installations for Windows 11. Install these components if not done yet:

#### a/ Scala 3

See https://scala-cli.virtuslab.org/install/

As described in this document, run in a Windows termninal ("cmd.exe") this command: _> winget install virtuslab.scalacli_

When running Scala tools the first time in a Windows terminal, expect more downloads and installations, like these commands:

_\> scala-cli_
 
_\> scala <name of a Scala source code file>_

Also make sure that these scala tools can be found in your Windows _PATH_ environment variable, for example like this:

_C:\Program Files\scala-cli-x86_64-pc-win32_

_C:\Users\...\AppData\Local\Coursier\data\bin_  (where did this come from?)

The installation process of the winget command is looking for a installed JVM on your Windows computer. I cannot say if one has to manually install the JDK for Windows, if no installed JVM was found: https://docs.oracle.com/en/java/javase/index.html

#### b/ JDK and JVM

I've JDK version 23 installed on my PC: https://docs.oracle.com/en/java/javase/23/install/overview-jdk-installation.html

But I think the exact version doesn't really matter at this point. So, the latest JDK version 24 should also work: https://docs.oracle.com/en/java/javase/24/index.html

I have these paths included in my Windows _PATH_ environment variable:

_C:\Program Files\Common Files\Oracle\Java\javapath_

_C:\Program Files (x86)\Common Files\Oracle\Java\java8path_

_C:\Program Files (x86)\Common Files\Oracle\Java\javapath_

#### c/ sbt

https://www.scala-sbt.org/download/: I think downloading and installing the _sbt-1.10.11.msi_ file is a good choice.

#### d/ C/C++ compiler for Scala native

Optional and only needed when building so called "Scala native" app's for Windows: install the _cl.exe_ compiler from a "C++ Workload" with Microsoft Visual Studio 2022 for example: https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170

Open a Windows Terminal and test the presence of this compiler like this for example:

_\> cl_

Again, make sure that the _cl.exe_ file can be found in your _PATH_:

_C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\bin\Hostx64\x64_

<br/>

## (A) Hello world with the Scala code runner in Windows 11


(TBD)


##_end
