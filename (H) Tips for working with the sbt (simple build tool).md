2025-04-09: work in progress

<br/>

# (H) Tips for working with the sbt (simple build tool)

Sometimes you want more detailed warnings during compilation, something which can be really helpful when working with intractable third-party libraries.

Edit _built.sbt_ file and add:

_scalacOptions ++= Seq("-deprecation", "-feature")_

Seen from here https://alvinalexander.com/scala/scala-sbt-re-run-with-deprecation-feature-message/

<br/>

##_end
