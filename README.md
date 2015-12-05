Logback Gaffer - Sift
=====================
Extends Logback Gaffer so can configure SiftingAppender in Groovy DSL, e.g.:

```groovy
import ch.qos.logback.classic.sift.SiftingAppender
import ch.qos.logback.classic.sift.MDCBasedDiscriminator
import ch.qos.logback.classic.PatternLayout

appender("SIFT", SiftingAppender) {
  discriminator(MDCBasedDiscriminator) {
    key = "userid"
    defaultValue = "unknown"
  }
  sift {
    appender("FILE-${userid}", FileAppender) {
      file = "${userid}.log"
      append = false
      layout(PatternLayout) {
        pattern = "%d [%thread] %level %mdc %logger{35} - %msg%n"
      }
    }
  }
}

root(DEBUG, ["SIFT"])
```

Usage instruction
-----------------
1. Build or [download](https://github.com/yihtserns/logback-gaffer-sift/releases/latest) the jar for this project.
2. Put it where you put `logback-classic-$VERSION.jar`.
3. Done!
