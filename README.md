# gradle-javadoc-notimestamp-error
Public repro of a Gradle 6.0 javadoc task bug with -notimestamp and custom doclets

To repro, run `./gradlew buildXmlJavadoc` using a Java 8 JVM (Java 9+ will give an unrelated error specific to the doclet):

```
> Task :buildXmlJavadoc FAILED
SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
SLF4J: Defaulting to no-operation (NOP) logger implementation
SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
javadoc: error - invalid flag: -doctitle
Usage: javadoc [options] [packagenames] [sourcefiles] [@files]
...
```

The issue is that Gradle is sending -doctitle and -notimestamp flags to Javadoc, which are not recognized by the custom doclet; these flags are used by the standard doclet.
