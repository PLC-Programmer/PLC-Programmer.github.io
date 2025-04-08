2025-04-08: work in progress

<br/>

Sometimes you want more detailed warnings during compilation, something which can be really helpful when working with intractable third-party libraries.

Edit _built.sbt_ file and add:

_scalacOptions ++= Seq("-deprecation", "-feature")_

Seen from here https://alvinalexander.com/scala/scala-sbt-re-run-with-deprecation-feature-message/

<br/>

##_end
