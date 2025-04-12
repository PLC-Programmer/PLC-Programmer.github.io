2025-04-12: work in progress

# (D) Working with simple build tool to create a standalone program ("Scala native") in Linux

If not yet happened, install the _clang_ compiler first. LLVM is not needed according to my tests. I used this description: https://www.cyberithub.com/how-to-install-clang-tool-on-ubuntu-or-debian-linux/ ("How to Install clang tool on Ubuntu or Debian Linux") and installed it like this:

_$ sudo apt install clang_

Then I checked version and availability:

_$ clang --version_

_Ubuntu clang version 18.1.3 (1ubuntu1)_

_Target: x86_64-pc-linux-gnu_

_Thread model: posix_

_InstalledDir: /usr/bin_

<br/>

Now open the Bash shell (Terminal) and set your working directory so that it will be **the parent directory of the later project root directory**:

_$ sbt new_  # create a new Scala project; this command also creates the project root directory

_Welcome to sbt new!_

_Here are some templates to get started:_
…

Select **option d)** with only pressing key [d] (and not pressing a following [ENTER]): _d) scala/scala3.g8 - Scala 3 seed template_

Now enter your project name (which is also the name of the project root directory in the filesystem of the OS):

_name [Scala 3 Project Template]: test_sbt_Linux_ # this is only an example project name

_Template applied in .\<project name>_

See also from this use case: https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(C)%20Working%20with%20simple%20build%20tool%20to%20run%20an%20app%20on%20the%20JVM%20in%20Windows%20with%20(3rd%20party)%20imports.md#select-option-d

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

But how to make this application "Scala Native"?

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



(TBD)

<br/>

##_end
