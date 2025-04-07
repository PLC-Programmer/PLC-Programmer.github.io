## 2025-04-07: starting with a series on "Running and building Scala programs - baby steps"

2025-04-07: work in progress

# Intro

Scala: the last high level, general purpose programming language before AI takes over programming?

<br/>

Anyhow, I discovered that making my very first "shippable" Scala applications, with latest Scala version 3, with the official tool called **sbt** (**"simple build tool"**: https://www.scala-sbt.org/) was not easy. It took me numerous trials and errors.

Understanding the sbt - at least to some extent - was my **key to understand practical coding with Scala** for more than just printing "Hello World!" to the console.

And it's super-easy to trap into the Scala, sbt, Java version hell and to become lost in an increasingly cluttered project files directory.

<br/>

In case you don't know: Scala heavily relies on the **Java ecosystem**. However, whenever I was in doubt with one of the numerous third party libraries, I turned to an official and hopefully latest version of a Java or close to Java library. This was one of the better experiences, though the state of the Java ecosystem after all those year since 1996(!) appears strange to me: https://www.geeksforgeeks.org/the-complete-history-of-java-programming-language/

I fought a lot with successfully **importing and using libraries** into my first, little scala source code files (~.scala). But I think I'm on a way to somehow master this challenge.

Just the week before, I've built successfully my first little Go (from Google) program: https://go.dev/ -- even with a version where I tested - also successfully - the famous and so called "goroutines".

This was a very positive experience, though I heard good things about Go before. I could concentrate on coding instead of fighting with the ecosystem.

Well, this is apparently the difference between a programming language from a multi billion dollar company or something else.

<br/>

I knew for years that Scala has - by design and constraints - only a slim core ecosystem. However, I was surprised of the length of my struggles to get little things finally running.

However, after elaborate experimentations I "cracked the code"!! After this, I could also build **default JVM**, **"native" Scala** and even **JavaScript** based executables in Linux (here Ubuntu LTS 24) without overwhelming efforts. The only flavor missing at the moment is something that can run on node.js, so something else than a web browser.

<br/>

Throughout my Scala journey so far, I discovered the first "dead" part of the Scala ecosystem, here a libary called "breeze" for mathematical functions (with Scala and Java these are not part of the standard libraries): https://github.com/scalanlp/breeze

I only needed something to calculate the (sample) mean and (sample) standard deviation of a set of numbers. Finally, I turned successfully to this library: https://commons.apache.org/proper/commons-math/

But boy, can't this age-old library have an inbuilt function for standard deviation?!?

Instead, one has first to use the function for variance and then take the square root: https://commons.apache.org/proper/commons-math/userguide/stat.html

```
import org.apache.commons.math3.stat.StatUtils  // StatUtils.mean, StatUtils.variance
import org.apache.commons.math3.util._          // FastMath.sqrt()
...
    // type casting over an array:
    val durations_Dbl: Array[Double] = durations.map(_.toDouble)

    val avg = StatUtils.mean(durations_Dbl)

    // variance and standard deviation of **sample**:
    val stddev = FastMath.sqrt(StatUtils.variance(durations_Dbl, avg))
```

<br/>

Here I will tell you already a "big secret": declaring the imports in a Scala source code file isn't enough. You have to have it listed in a configuration file of the sbt tool, called _build.sbt_ and hopefully with the right version numbers and syntax:

```
libraryDependencies += "org.apache.commons" % "commons-math3" % "3.6.1"
```

(memo to myself: I hope that I remember to add now and then some examples for this and another configuration file for the sbt tool for an example project. You necessarily don't need a build tool for very simple things, but for anything more demanding and stepping outside of the Scala core, this tool - or another build tool - is **essential** from my point of view.)



<br/>

Of course, it's never a good sign when a language specific library, which was under development and in use for more than a decade, becomes retired.

From my point of view it would be a real pittly if the Scala programming language, just after the boost of the major step forward with the version 3, starting around 2019/2020, becomes less and less used in the "real world":

https://docs.scala-lang.org/scala3/new-in-scala3.html: "Scala 3 is a complete overhaul of the Scala language." 

2021-02-17: https://dotty.epfl.ch/blog/2021/02/17/scala3-rc1.html: "Scala 3.0.0-RC1 – first release candidate is here"


##_end


