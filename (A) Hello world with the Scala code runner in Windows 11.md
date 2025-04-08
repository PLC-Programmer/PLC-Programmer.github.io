2025-04-08: work in progress

# Installations in Windows 11

Some notes on Scala installations for Windows 11. Install these components if not done yet:

#### a/ Scala 3

See https://scala-cli.virtuslab.org/install/

As described in this document, run in a Windows termninal ("cmd.exe") this command: _> winget install virtuslab.scalacli_

When running Scala tools the first time in a Windows terminal, expect more downloads and installations, like with these commands:

_\> scala-cli_

_Welcome to Scala 3.6.4 (17.0.14, Java OpenJDK 64-Bit Server VM)._

_Type in expressions for evaluation. Or try :help._

_scala>_  # the Scala command prompt; type _:exit_ to leave it

<br/>

_\> scala_

_Welcome to Scala 3.6.4 (17.0.14, Java OpenJDK 64-Bit Server VM)._

_Type in expressions for evaluation. Or try :help._

_scala>_

(the same output)
 
<br/>

Also make sure that these scala tools can be found in your Windows _PATH_ environment variable, for example like this:

_C:\Program Files\scala-cli-x86_64-pc-win32_

<br/>

_C:\Users\...\AppData\Local\Coursier\data\bin_  -- this path came with the Scala installer for Windows based on Coursier: _cs-x86_64-pc-win32.exe_ from here: https://docs.scala-lang.org/getting-started/index.html#using-the-scala-installer-recommended-way

I just installed this too.

#### b/ Java Runtime Environment (JRE)

The installation process of the winget command is looking for an installed JVM on your Windows computer.

If a JRE (something like "Java 8 Update...") ist not yet existing on your computer, install it from here: https://www.java.com/en/download/manual.jsp

I took the "Windows Offline (64-bit)" _jre-8u441-windows-x64.exe_ installation file:

![plot](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/jre8.png)

Check the presence of Java from a Windows Terminal:

_\> java -version_

_java version "1.8.0_441"_

_Java(TM) SE Runtime Environment (build 1.8.0_441-b07)_

_Java HotSpot(TM) 64-Bit Server VM (build 25.441-b07, mixed mode)_

<br/>

Windows _PATH_ should now include these additional pathes:

_C:\Program Files (x86)\Common Files\Oracle\Java\java8path_

_C:\Program Files (x86)\Common Files\Oracle\Java\javapath_

#### c/ sbt (simple build tool)

https://www.scala-sbt.org/download/: I think downloading and installing the _sbt-1.10.11.msi_ file is a good choice.

#### d/ C/C++ compiler for Scala native

Optional and only needed when building so called "Scala native" app's for Windows: install the _cl.exe_ compiler from a "C++ Workload" with Microsoft Visual Studio 2022 for example: https://learn.microsoft.com/en-us/cpp/build/vscpp-step-0-installation?view=msvc-170

Open a Windows Terminal and test the presence of this compiler like this for example:

_\> cl_

_Microsoft (R) C/C++-Optimierungscompiler Version 19.43.34809 für x64_

_Copyright (C) Microsoft Corporation. Alle Rechte vorbehalten._

...

Again, make sure that the _cl.exe_ file can be found in your _PATH_:

_C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\bin\Hostx64\x64_

<br/>

## (A) Hello world with the Scala code runner in Windows 11


(TBD)


##_end
