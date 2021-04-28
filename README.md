# google-format-gradle

Sample project integrating `google-java-format` into a gradle build script.

## Configuration

How the project was configured:

```
$ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Scala
  6: Swift
Enter selection (default: Java) [1..6] 3

Split functionality across multiple subprojects?:
  1: no - only one application project
  2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 1

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit 4) [1..4] 2

Project name (default: t): sample
Source package (default: sample):

> Task :init
Get more help with your project: https://docs.gradle.org/7.0/samples/sample_building_java_applications.html

BUILD SUCCESSFUL in 1m 17s
2 actionable tasks: 2 executed
```
