# Gradle Test Logger Plugin
[![license](https://img.shields.io/github/license/radarsh/gradle-test-logger-plugin.svg)](https://github.com/radarsh/gradle-test-logger-plugin/blob/develop/LICENSE)
[![CircleCI branch](https://img.shields.io/circleci/project/github/radarsh/gradle-test-logger-plugin/develop.svg)](https://circleci.com/gh/radarsh/gradle-test-logger-plugin/tree/develop)
[![AppVeyor branch](https://img.shields.io/appveyor/ci/radarsh/gradle-test-logger-plugin/develop.svg)](https://ci.appveyor.com/project/radarsh/gradle-test-logger-plugin/branch/develop)

A Gradle plugin for printing beautiful logs on the console while running tests.

## Standard theme

![Standard theme](docs/standard-theme.gif)

## Mocha theme

![Mocha theme](docs/mocha-theme.gif)

## Usage

### Modern Gradle

```groovy
plugins {
    id 'com.adarshr.test-logger' version '1.0.1'
}
```

### Gradle < 2.1

```groovy
buildscript {
    repositories {
        maven {
            url 'https://plugins.gradle.org/m2/'
        }
    }
    dependencies {
        classpath 'com.adarshr:gradle-test-logger-plugin:1.0.1'
    }
}

apply plugin: 'com.adarshr.test-logger'
```

## Configuration

### Switch themes

```groovy
testlogger {
    theme 'mocha'
}
```

The following themes are currently supported:

1. `plain` - displays no colours or Unicode symbols
2. `standard` - displays colours but no Unicode symbols
3. `mocha` - similar to what [mochajs](https://github.com/mochajs/mocha) prints, with colours and Unicode symbols

### Hide exceptions

By default, the `showExceptions` flag is turned on. This shows why the tests failed including the location of the
failure. Of course, you can switch off this slightly more verbose logging by setting `showExceptions` to `false`.

```groovy
testlogger {
    showExceptions false
}
```

### Define slow threshold

Tests that are too slow will have their duration logged. However, "slow" is a relative terminology varying widely
depending on the type of tests being executed, environment, kind of project and various other factors. Therefore you
can define what you consider as slow to suit your needs.

```groovy
testlogger {
    slowThreshold 5000
}
```

The default value of `slowThreshold` is `1` second. So all tests that take longer than a second to run will have their
actual execution time logged.

If you want to turn off the logging of time taken completely, simply set the threshold to a very large value.

## FAQ

### Does it work on Windows?

Mostly. The `standard` and `plain` themes work out of the box but you might have to make a few modifications to your
system settings to see Unicode symbols when using the `mocha` theme.

1. Set or update `JAVA_OPTS` with the system property `-Dfile.encoding=UTF-8`
2. Change the terminal code page to 65001 by executing `chcp 65001`

### How to disable colours and Unicode symbols at runtime such as on Jenkins consoles?

You can switch off ANSI control characters and Unicode symbols by adding `--console=plain` to your Gradle command line.
