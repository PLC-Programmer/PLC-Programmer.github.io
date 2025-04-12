2025-04-12: work in progress

<br/>

# (H) Tips for working with the sbt (simple build tool)

### More detailed compilation warnings

Sometimes you want more detailed warnings during compilation, something which can be really helpful when working with intractable third-party libraries.

Edit _built.sbt_ file and add:

_scalacOptions ++= Seq("-deprecation", "-feature")_

Seen from here https://alvinalexander.com/scala/scala-sbt-re-run-with-deprecation-feature-message/

### Just keep it standard and compile to bytecode for the JVM:

See from here: [Is "Scala native" worth the effort?](https://github.com/PLC-Programmer/PLC-Programmer.github.io/blob/main/(D)%20Working%20with%20simple%20build%20tool%20to%20create%20a%20standalone%20program%20(%22Scala%20native%22)%20in%20Linux.md#is-scala-native-worth-the-effort)

<br/>

##_end
