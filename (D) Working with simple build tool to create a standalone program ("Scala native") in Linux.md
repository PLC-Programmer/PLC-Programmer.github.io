2025-04-12: work in progress

Direct jump to [(D2) Working with scala-cli to create a standalone program in Windows 11](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(D)%20Working%20with%20simple%20build%20tool%20to%20create%20a%20standalone%20program%20(%22Scala%20native%22)%20in%20Linux.md#d2-working-with-scala-cli-to-create-a-standalone-program-in-windows-11)

# (D) Working with simple build tool to create a standalone program ("Scala native") in Linux

If not happened yet, install the _clang_ compiler first. LLVM is not needed according to my tests. I used this description: https://www.cyberithub.com/how-to-install-clang-tool-on-ubuntu-or-debian-linux/ ("How to Install clang tool on Ubuntu or Debian Linux") and installed it like this:

_$ sudo apt install clang_

Then check version and availability:

_$ clang --version_

_Ubuntu clang version 18.1.3 (1ubuntu1)_

_Target: x86_64-pc-linux-gnu_

_Thread model: posix_

_InstalledDir: /usr/bin_

### Install Scala on Ubuntu and test it a little bit

You can install Scala on Ubuntu like this:

_$ curl -fL https://github.com/coursier/coursier/releases/latest/download/cs-x86_64-pc-linux.gz | gzip -d > cs && chmod +x cs && ./cs setup_

...

_Checking if a JVM is installed_

...

_No JVM found, should we try to install one? [Y/n]_ --> press [Y]

...

In case of a problem, here's the official installation guide for latest **Coursier** version 2.1.25-M4: https://get-coursier.io/docs/cli-installation

_These instructions will install the coursier CLI cs itself, as well as a typical Scala development environment._

Now a reboot of the Linux machine is needed, not only a re-opening of the Linux shell.

<br/>

Check the installation after the reboot:

_$ scala -version_

_Scala code runner version: 1.5.4_

_Scala version (default): 3.6.4_

### Start a Scala project

Now open the Bash shell (Terminal) and set your working directory so that it will be **the parent directory of the later project root directory**:

_$ sbt new_  # create a new Scala project; this command also creates the project root directory

_Welcome to sbt new!_

_Here are some templates to get started:_
…

Select **option d)** with only pressing key [d] (and not pressing a following [ENTER]): _d) scala/scala3.g8 - Scala 3 seed template_

Now enter your project name (which is also the name of the project root directory in the filesystem of the OS):

_name [Scala 3 Project Template]: test_sbt_Linux_ # this is only an example project name

_Template applied in .\<project name>_

See also from this use case: [Select option d)](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(C)%20Working%20with%20simple%20build%20tool%20to%20run%20an%20app%20on%20the%20JVM%20in%20Windows%20with%20(3rd%20party)%20imports.md#select-option-d)

<br/>

Optionally edit the _**build.sbt**_ file in _./\<project root dir\>/build.sbt_: often one or more library dependencies have to be added there, here for example:

_libraryDependencies += "org.typelevel" %% "cats-core" % "2.13.0"_

You may look up the exact version of a library from searching here: https://mvnrepository.com/
	
<br/>

Now change into the project root directory:

_$ cd <project root dir>_

..and start the sbt again:

_$ sbt_

_[info] welcome to sbt 1.10.11 (Eclipse Adoptium Java 11.0.26)_

_[info] loading project definition from /home/ ... /\<project name\>/project_

_[info] loading settings for project root from build.sbt..._

_[info] set current project to \<project name\> (in build file:/home/\<user\>/ ... /\<project name\>/)_

_[info] sbt server started at local:///home/\<user\>/.sbt/1.0/server/35e75b11c375067c3e8d/sock_

_[info] started sbt server_

Now the **sbt prompt** should show up:

_sbt:\<project name\>>_

<br/>

As a test, build and run this demo project:

_sbt:\<project name\>> run_

There should be success now:

_[info] compiling 1 Scala source to /home/\<user\>/ ... /\<project name\>/target/scala-3.6.4/classes ..._

_[info] running hello_

_**Hello world!**_

_I was compiled by Scala 3. :)_

_[success] Total time: 3 s, completed Apr 12, 2025, 10:41:22 AM_

<br/>

But how to make this application "Scala native"?

I followed this advice at chapter "Compiling and running your Scala Native application" from:

_Getting Started with Scala Native: A Comprehensive Guide for Beginners_

https://medium.com/@diehardankush/getting-started-with-scala-native-a-comprehensive-guide-for-beginners-dedafeed7f25
Ankush Singh, Apr 23, 2023

…and found this command:

_sbt:<project name>> **nativeLink**_

_[error] Not a valid command: nativeLink_

_[error] Not a valid project ID: nativeLink_

_[error] Expected ':'_

_[error] Not a valid key: nativeLink_

_[error] nativeLink_

_[error]           ^_

_sbt:\<project name\>>_

<br/>

Apparently, the _build.sbt_ file must be fixed first.

**Without leaving the sbt**, open a second Terminal (and keep it running!) and **append** line _enablePlugins(ScalaNativePlugin)_ like this for example (you could also use a text editor for doing this parallel job):

_\<project root dir\>/project$ echo "enablePlugins(ScalaNativePlugin)" > build.sbt_

You may also check success of this operation like this for example:

_\<project root dir\>/project$ cat build.sbt_

```
val scala3Version = "3.6.4"

lazy val root = project
  .in(file("."))
  .settings(
    name := "test_sbt_Linux",
    version := "0.1.0-SNAPSHOT",

    scalaVersion := scala3Version,

    libraryDependencies += "org.scalameta" %% "munit" % "1.0.0" % Test
  )

enablePlugins(ScalaNativePlugin)
```

<br/>

Then the _plugin.sbt_ file must be added in the already existing _./project_ sub directory and have this plugin being added:

_\<project root dir\>$ cd project_

_\<project root dir\>/project$ echo "addSbtPlugin(\"org.scala-native\" % \"sbt-scala-native\" % \"0.5.7\")" > plugin.sbt_

I got this latest Scala native version number from here: https://www.scala-native.org/en/stable/

Again, you can check success like this:

_\<project root dir\>/project$ cat plugin.sbt_

```
addSbtPlugin("org.scala-native" % "sbt-scala-native" % "0.5.7")
```

<br/>

You may edit the _Main.scala_ source code file in the _\<project root dir\>/src/main/scala_ sub directory like this as a test:

```
@main def hello(): Unit =
  println("Hello world from Scala Native with version 0.5.7!")
  println(msg)

def msg = "I was compiled by Scala 3. :)"
```

<br/>

Now return to the Terminal with the sbt running and apply these commands:

_sbt:\<project name\>> reload_  # reload the changed project configuration

\<hopefully some downloading is happening here\>
	
Do again:

_sbt:\<project name\>> nativeLink_

\<hopefully some more downloading is happening here and then some building\>

_[success] Total time: 5 s, completed Apr 12, 2025, 11:27:35 AM_

_sbt:\<project name\>>_

Make a run from the sbt as a test:

_sbt:\<project name\>> run_

_[info] Build skipped: No changes detected in build configuration and class path contents since last build._

**_Hello world from Scala Native with version 0.5.7!_**

_I was compiled by Scala 3. :)_

_[success] Total time: 0 s, completed Apr 12, 2025, 11:29:53 AM_

_sbt:\<project name\>>_

<br/>

**The executable** can now be found in sub directory _\<project root dir\>/target/scala-3.6.4/_ with file name **\<project name\>**

Run it in the second Terminal (so still keep the sbt running in the first Terminal):

_\<project root dir\>/target/scala-3.6.4$_ ./\<project name\>

_Hello world from Scala Native with version 0.5.7!_

_I was compiled by Scala 3. :)_

_\<project root dir\>/target/scala-3.6.4$_

Bingo!

<br/>

As a second test, I copied file \<project name\> to another Ubuntu 24 LTS system and run it there (with no Scala, Java etc. resources installed).

Don't forget to do first: _$ chmod 774 ./_\<project name\>

_$_ ./\<project name\>

_Hello world from Scala Native with version 0.5.7!_

_I was compiled by Scala 3. :)_

Double Bingo!

<br/>

Finally do this:

_sbt:\<project name\>> exit_

_[info] shutting down sbt server_

_$_

<br/>

I also tried option c) at the _sbt new_ command:

_c) sbt/cross-platform.local - A cross-JVM/JS/Native project_

..but was not really sure so far what to make out of the _./\<project root dir\>/core_ sub directory and all the other created artefacts.

<br/>

Fun fact: a cool 6.711 items, totalling 34,5 MB, have been created for this project so far! 

<br/>


### (D2) Working with scala-cli to create a standalone program in Windows 11

"Standalone program" == "Scala native" program

In Windows, the Scala shell, that is the command-line tool _scala-cli_, can be used to compile Scala source code into an executable Windows program.

If not done yet, download and install something like this: **Visual Studio Community 2022** with the "C++ for Desktop workload".

Manually add path to _cl.exe_ to the Windows _PATH_ environment variable; for example:

_C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\MSVC\14.43.34808\bin\Hostx64\x64;_

Check availability of _cl.exe_ in a Windows Terminal ("cmd.exe"):

_> cl.exe_

_Microsoft (R) C/C++-Optimierungscompiler Version 19.43.34809 für x64_

...

Change to the directory of the source code file which contains _main_, here _hello_world.scala_:

```
@main def helloWorld() = println("Hello, world!")
```

This directory may contain only this source code file, nothing more is needed.

Run build command like this. It may take some time the first time:

_> scala-cli package hello_world.scala -o hello_world --native-image --power_

_Starting compilation server_

_Compiling project (Scala 3.6.4, JVM (17))_

_Compiled project (Scala 3.6.4, JVM (17))_

_\<project dir\>>chcp 437_

_Active code page: 437_

...

_----------------------------------------------------------------------_

_Produced artifacts:_

_\<project dir\>\hello_world.build_artifacts.txt (txt)_
 
_\<project dir\>\hello_world.exe (executable)_

_======================================================================_

_Finished generating 'hello_world' in 12,7s._

_Wrote \<project dir\>\hello_world.exe, run it with_

_.\hello_world.exe_

Do this as told:

_**Hello, world!**_


<br/>

### Is "Scala native" worth the effort?

I don't think so. I think the natural runtime environment for Scala programs is (still) the Java Runtime Environment (JRE).

When I wrote a more elaborate Scala program, I noticed that running this program in the JRE is (substantially) **faster** than the "Scala native" version! :flushed:

This seems to be specifically true if a program is doing big and/or a lot of iterations.

See from here for example: https://www.oreilly.com/library/view/learning-java-5th/9781492056263/

_Historically, interpreters have been considered slow, but Java is not a traditional interpreted language. In addition to compiling source code down to portable bytecode, Java has also been carefully designed so that software implementations of the runtime system can further optimize their performance by compiling bytecode to native machine code on the fly. This is called just-in-time (JIT) or dynamic compilation. With JIT compilation, Java code can execute as fast as native code and maintain its transportability and security._

So, compiling Scala source code to OS specific binary code is not necessarily a better thing than compiling it to standard and portable bytecode for the JVM.

<br/>

##_end
