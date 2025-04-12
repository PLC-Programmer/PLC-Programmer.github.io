2025-04-12: work in progress

# (E) From a Scala program to JavaScript for the web browser

Windows 11: the official Scala to JavaScript demo didn't work for me (that is in the sbt taking option _m) scala-js/vite.g8 - A Scala.JS + Vite project_), but in Ubuntu 24 LTS!

I did this:

### Install Vite and Yarn

At first I installed Vite (a frontend build tool) and Yarn (a JavaScript package manager): https://tecadmin.net/install-yarn-on-ubuntu-22-04/ --> I took method 1:

_$ sudo apt update_

_$ sudo apt install nodejs npm_

_$ sudo npm install --global yarn_

_$ yarn --version_

_1.22.22_

_$ nodejs --version_

_v18.19.1_

### Build the default demo project with the sbt

Run in your project root directory:

_$ sbt new_

Here take option _m) scala-js/vite.g8 - A Scala.JS + Vite project_

As usual just enter the [m] key here, do not press [ENTER] at this, or any other option!!

name: press [ENTER] to accept this demo project name "scalajs-vite-example"

use_yarn: press [ENTER] to use yarn

...
_.\Template applied in Template applied in ... ./scalajs-vite-example_

Change into the project root directory:

_$ cd ./scalajs-vite-example_

Now do the background build of this demo project after every source code change ("~"):

_$ sbt ~fastLinkJS_

...

_[success] Total time: 15 s, completed Apr 2, 2025, 9:12:40 PM_

_[info] 1. Monitoring source files for root/fastLinkJS..._

_[info]    Press <enter> to interrupt or '?' for more options._ <-- I pressed the [ENTER] key because I didn't open a second Terminal for the next steps

_[info] Received input event: CancelWatch._

_[info] shutting down sbt server_

Do this for every new project:

_$ yarn_

...

_yarn install v1.22.22_

_info No lockfile found._

_[1/4] Resolving packages..._

_[2/4] Fetching packages..._

_[3/4] Linking dependencies..._

_[4/4] Building fresh packages..._

_success Saved lockfile._

_Done in 15.69s._

<br/>

Now start the web server:

_$ npm run dev_

_> scalajs-vite-example \@ 0.1.0-SNAPSHOT dev_

_> vite_

_[info] welcome to sbt 1.8.2 (Eclipse Adoptium Java 11.0.26)_

_[info] loading settings for project scalajs-vite-example-build from plugins.sbt ..._

_[info] loading project definition from ... ./Scala/scalajs-vite-example/project_

_[info] loading settings for project root from build.sbt ..._

_[info] set current project to scalajs-vite-example (in build file: ... ./scalajs-vite-example/)_

_... ./scalajs-vite-example/target/scala-3.2.2/scalajs-vite-example-fastopt_

_VITE v4.5.11  ready in 3764 ms_

_➜  Local:   http://localhost:5173/_
  
_➜  Network: use --host to expose_
  
_➜  press h to show help_

<br/>

Now open a local web browser to the given address http://localhost:5173/ -- but be careful not to stop the web server with wrong mouse clicks or so in this reactive Terminal (otherwise restart it with running _npm run dev_ again).

Here we are:

![plot](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/hello_world_from_vite.png)

<br/>

### Building my own little demo project with the sbt

After this initial success (though Vite complained about _Sourcemap for "... .js" points to missing source files_ four times), I started another demo project with only a few changes in a different project root directory named _hello_world2_with_sbt_:

_$ sbt new_ --> after selecting option m) again, enter _hello_world2_with_sbt_ as the project name

<sbt is doing its stuff>

Now I worked a bit on the main source code file, the project configuration file and the project directory structure:

#### Change #1

Starting with the project root directory, I moved file _./src/main/scala/example/Main.scala_ to _./src/main/scala/main/Main.scala_

Having a _main_ subdirectory under directory _scala_ isn't very creative indeed, it's just a replacement for _example_ from the sbt.

I modified _Main.scala_ like this:

```
package main
@main def something(): Unit =  // @main is obviously important, def xxxx() is not
  // some more fancy HTML code:
  dom.document.querySelector("#app").innerHTML = s"""
  <head>
    <style>
      .my-element {
        width: 600px; /* Set the width to 600 pixels */
      }
    </style>
  </head>
  <body>
    <div class="my-element">
      __** this is an example element with a constant width of 600 pixels **__
    </div>
  </body>
  """
```





#### Change #2


(TBD)

<br/>

##_end
