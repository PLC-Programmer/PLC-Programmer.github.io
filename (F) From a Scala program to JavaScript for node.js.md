2025-04-14: work in progress

Spoler alert: this use case has practically no value for me because so far I couldn't find a solution for this open point described below: [How to read from the console when executing JavaScript on node.js?](#how-to-read-from-the-console-when-executing-javascript-on-node)

<br/>

# (F) From a Scala program to JavaScript for node.js

#### The Hello world! example

Start a new sbt project in a parent directory of the later project root directory:

_$ sbt new_

Again, choose **option m)** (see also from here: [Build the default demo project with the sbt](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(E)%20From%20a%20Scala%20program%20to%20JavaScript%20for%20the%20web%20browser.md#build-the-default-demo-project-with-the-sbt) )

and enter _scala_to_js_on_nodejs_ as the project name for example.

Rename sub directory _./src/main/scala/example_ to _./src/main/scala/main_ and change _example_ to _main_ in the _build.sbt_ configuration file too (just to get away from term "example").

Change application source code file _Main.scala_ to this, which is the **real change** compared to use case [(E) From a Scala program to JavaScript for the web browser](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(E)%20From%20a%20Scala%20program%20to%20JavaScript%20for%20the%20web%20browser.md#e-from-a-scala-program-to-javascript-for-the-web-browser):

```
object Main {
  def main(args: Array[String]): Unit = {
    println("Hello world!")
  }
}
```

See also from here: https://www.scala-js.org/doc/project/building.html

In the project root directory change configuration file _build.sbt_ like this:

```
…
    scalaVersion := "3.6.4",
…
         scalaJSLinkerConfig ~= {
      _.withModuleKind(ModuleKind.ESModule)
      .withModuleSplitStyle(ModuleSplitStyle.SmallModulesFor(List("main")))
    },
…
```

You can delete line _libraryDependencies += "org.scala-js" %%% "scalajs-dom" % "2.4.0",_ because it's not needed here, only in a web app.

In config file _plugins.sbt_ in the _./project_ directory add this line:

```
addSbtPlugin("org.scala-js" % "sbt-scalajs" % "1.18.2")
```

Again, you can look up the exact version numbers from here: https://mvnrepository.com/artifact/org.scala-js/sbt-scalajs_2.12_1.0/1.18.2

<br/>

Now in the project root directory do:

_$ sbt_

_sbt:scala_to_js_on_nodejs>_

_sbt:scala_to_js_on_nodejs> compile_

…

_[success] …_

_sbt:scala_to_js_on_nodejs> **fastLinkJS**_

…

[success] …

See also from here: https://www.scala-js.org/doc/project/building.html

<br/>

Now run this app:

_sbt:scala_to_js_on_nodejs> run_

_[info] Running Main._

_**Hello world!**_

_[success] Total time: 0 s, completed Apr 13, 2025, 1:09:15 PM_

_sbt:scala_to_js_on_nodejs>_

<br/>

You can find the transpiled JavaScript file in this directory:

_./scala_to_js_on_nodejs/target/scala-3.6.4/scala_to_js_on_nodejs-fastopt/main.js_

Execute this JavaScript code on node.js like this: _**$ node main.js**_

_**Hello world!**_

<br/>

Of course this can be done also in other directories, when _main.js_ has been copied there and maybe, as in this case, being renamed to a more descriptive name like _scala_to_js_on_nodejs.js_ for example:

_$ mv main.js scala_to_js_on_nodejs.js_

_$ node scala_to_js_on_nodejs.js_

_Hello world!_

See also more official advice from here: https://scala-cli.virtuslab.org/docs/guides/advanced/scala-js/

<br/>

#### "Stopwatch" app in JavaScript for node.js

This little demo app doesn't implement a real stopwatch here since no genuine computations going on, but a timeout of 1,000 milliseconds.

```
//> using scala 3.6.4
import scala.scalajs.js.timers
import scala.scalajs.js.Date
object stopwatch_in_JavaScript {
  def main(args: Array[String]): Unit = {
    println("Welcome to a test of some imported scala.scalajs.js methods:")
    val sleep_ms = 1000
    val t0 = Date.now()
    val sleep = timers.setTimeout(sleep_ms) {
                  val t1 = Date.now()
                  val time_diff = t1 - t0
                  val out_str = "this was a waiting time of " + time_diff + " milliseconds"
                  println(out_str)
                }
  }
}
```

Again, check config files _plugins.sbt_ and _build.sbt_.

In _build.sbt_ line:

_scalaJSUseMainModuleInitializer := true,_

..is needed, otherwise the app cannot be linked (with the fastLinkJS command in the sbt).

Check for _**%%%**_ in _build.sbt_:

_libraryDependencies += "org.typelevel" **%%%** "cats-effect" % "3.6.1"_

> **Use %%% instead of %% when depending on other Scala.js library's**

See from here: https://www.scala-js.org/doc/project/linking-errors.html

You can look up details of the _**scala.scalajs.js**_ package from here: https://javadoc.io/doc/org.scala-js/scalajs-library_2.12/latest/scala/scalajs/js/index.html

<br/>

### How to read from the console when executing JavaScript on node.js?

(TBD)

<br/>

##_end
