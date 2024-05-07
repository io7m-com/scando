scando
===

[![Maven Central](https://img.shields.io/maven-central/v/com.io7m.scando/com.io7m.scando.svg?style=flat-square)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.io7m.scando%22)
[![Maven Central (snapshot)](https://img.shields.io/nexus/s/com.io7m.scando/com.io7m.scando?server=https%3A%2F%2Fs01.oss.sonatype.org&style=flat-square)](https://s01.oss.sonatype.org/content/repositories/snapshots/com/io7m/scando/)
[![Codecov](https://img.shields.io/codecov/c/github/io7m-com/scando.svg?style=flat-square)](https://codecov.io/gh/io7m-com/scando)
![Java Version](https://img.shields.io/badge/17-java?label=java&color=007fff)

![com.io7m.scando](./src/site/resources/scando.jpg?raw=true)

| JVM | Platform | Status |
|-----|----------|--------|
| OpenJDK (Temurin) Current | Linux | [![Build (OpenJDK (Temurin) Current, Linux)](https://img.shields.io/github/actions/workflow/status/io7m-com/scando/main.linux.temurin.current.yml)](https://www.github.com/io7m-com/scando/actions?query=workflow%3Amain.linux.temurin.current)|
| OpenJDK (Temurin) LTS | Linux | [![Build (OpenJDK (Temurin) LTS, Linux)](https://img.shields.io/github/actions/workflow/status/io7m-com/scando/main.linux.temurin.lts.yml)](https://www.github.com/io7m-com/scando/actions?query=workflow%3Amain.linux.temurin.lts)|
| OpenJDK (Temurin) Current | Windows | [![Build (OpenJDK (Temurin) Current, Windows)](https://img.shields.io/github/actions/workflow/status/io7m-com/scando/main.windows.temurin.current.yml)](https://www.github.com/io7m-com/scando/actions?query=workflow%3Amain.windows.temurin.current)|
| OpenJDK (Temurin) LTS | Windows | [![Build (OpenJDK (Temurin) LTS, Windows)](https://img.shields.io/github/actions/workflow/status/io7m-com/scando/main.windows.temurin.lts.yml)](https://www.github.com/io7m-com/scando/actions?query=workflow%3Amain.windows.temurin.lts)|

## scando

A trivial command-line wrapper around [japicmp](https://siom79.github.io/japicmp/CliTool.html).

### Features

  * Simple command-line tool for checking jar version changes.
  * Compare `jar` files for semantic versioning conformance.
  * Compare Android `aar` files for semantic versioning conformance.
  * Powered by [japicmp](https://github.com/siom79/japicmp).
  * High-coverage automated test suite.</li>
  * ISC license.

### Building

```
$ mvn clean verify
```

### Usage

```
Usage: scando [options]
  Options:
    --excludeList
      A file containing a list of package/class exclusions
    --help
      Display this help message
  * --htmlReport
      The output file for the HTML report
    --ignoreMissingOld
      Trivially succeed if the old jar is missing.
      Default: false
  * --newJar
      The new jar file
  * --newJarVersion
      The new jar version
  * --oldJarUri
      The old jar/aar file/URI
  * --oldJarVersion
      The old jar version
  * --textReport
      The output file for the plain text report

$ java -jar \
  com.io7m.scando.cmdline-0.0.1-main.jar \
  --oldJarUri https://repo1.maven.org/maven2/com/io7m/jtensors/io7m-jtensors-core/7.1.0/io7m-jtensors-core-7.1.0.jar \
  --newJar com.io7m.jtensors.core-9.0.0.jar \
  --oldJarVersion 7.1.0 \
  --newJarVersion 7.2.0 \
  --textReport report.txt \
  --htmlReport report.html
INFO: Text report written to report.txt
INFO: HTML report written to report.html
ERROR: Version change between 7.1.0 and 7.2.0 is MINOR, but the changes made to code require a MAJOR version change

$ echo $?
1
```

The `--excludeList`parameter, if specified, gives the path of a file containing
one exclude pattern per line. Empty lines, and lines starting with `#`are ignored.
See [japicmp](https://siom79.github.io/japicmp/CliTool.html) for the syntax of
exclude patterns.

The `--ignoreMissingOld` parameter, if specified, allows for ignoring a missing
"old" jar. This is useful when, for example, a new module is added to a project.

