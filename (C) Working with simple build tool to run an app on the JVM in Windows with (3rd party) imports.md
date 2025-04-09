2025-04-09: work in progress

# (C) Working with simple build tool to run an app on the JVM in Windows with (3rd party) imports

Open the Windows command prompt ("cmd.exe"): ...\> 

*** **Set your working directory so that it will be the parent directory of the later project root directory.** ***

_\> sbt new_  # create a new Scala project; this command also creates the project root directory

_Welcome to sbt new!_

_Here are some templates to get started:_

Select **option d)** with only pressing key [d] (and not pressing a following [ENTER]): _d) scala/scala3.g8 - Scala 3 seed template_

Now enter your project name (which is also the name of the project root directory in the filesystem of the OS): 

_name [Scala 3 Project Template]:_ _test_sbt_Windows_  # this is only an example project name

_Template applied in .\<project name>_
	
![plot](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/sbt_new_Windows.png)

Now the **sbt prompt** should show up:

_sbt:\<project name\>>_

<br/>

Optionally edit, without leaving this sbt session, the _**build.sbt**_ file in the _.\<project root dir>\build.sbt_: often one or more library dependencies have to be added there, here for example:

_libraryDependencies += "org.typelevel" %% "cats-core" % "2.13.0"_

You may look up the exact version of a library from searching here: https://mvnrepository.com/
	
<br/>

Now build and run this demo project like this:

_sbt:\<project name\>> run_

There should be a success now:

 _[info] compiling 1 Scala source to … .\<project name>\target\scala-3.6.4\classes ..._

_[info] running hello_

_**Hello world!**_

_I was compiled by Scala 3. :)_

_[success] Total time: 3 s, completed 05.04.2025, 21:44:50_

_sbt:\<project name\>>_

<br/>
 
Now you can edit the Scala source code file with the main function (_@main def hello(): Unit =_ or something like this) at this relative path:

_**.\<project name>\src\main\scala\Main.scala**_

In the meantime you can put the sbt into the listening mode with the "~" character before a command to start building and running again when the _Main.scala_ file has been changed by you:

 _sbt:\<project name\>> ~run_

_[info] 1. Monitoring source files for root/run..._

_[info]    Press <enter> to interrupt or '?' for more options._

_[info] Build triggered by … .\<project name>\src\main\scala\Main.scala. Running 'run'._
	
_[info] compiling 1 Scala source to … .\<project name>\target\scala-3.6.4\classes ..._

_[info] running hello_

_**Hello world!++**_

_I was compiled by Scala 3. :)_

_[success] Total time: 0 s, completed 05.04.2025, 21:49:33_

_[info] 2. Monitoring source files for root/run..._

_[info]    Press <enter> to interrupt or '?' for more options._

We end this monitoring session now, so press key [ENTER]

_[info] Received input event: CancelWatch._

...and finally leave this sbt session with this command:

_sbt:\<project name\>> exit_

_[info] shutting down sbt server_

Now we are back at the Windows Terminal:

\>

<br/>

When you want to continues with this project, do this: **in the project root directory** enter (in the Windows Terminal): _\> sbt_

_[info] welcome to sbt 1.10.11 (Oracle Corporation Java 23.0.2)_

<br/>

### (C) as a basic workflow with my Scala programming

This workflow (C), be it in Windows or Linux, is kind of a basic workflow for my (little) Scala programming. It involves 4 key concepts:

* the starting point is opening an OS shell and changing to a directory which will be the parent directory of the later project root directory
* remember that with the _> sbt new_ command from the OS shell and setting a project name at: _name [Scala 3 Project Template]:_ inside the simple build tool you will automatically create the OS project root directory!
* working on the _build.sbt_ configuration file located in the project root directory
* the operation of the sbt, often having a leading "~" character at a sbt command to work in the foreground on source code files and project configuration files

It look me a while to become familiar with this basic workflow.

<br/>

##_end
