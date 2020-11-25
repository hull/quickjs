# QuickJS

[![quickjs](https://github.com/webfolderio/quickjs/workflows/quickjs/badge.svg)](https://github.com/webfolderio/quickjs/actions) [![License](https://img.shields.io/badge/license-Apache-blue.svg)](https://github.com/webfolderio/quickjs/blob/master/LICENSE)

Java binding for [quickjs 2020-07-05](https://bellard.org/quickjs/), a very compact embedded ECMAScript (JavaScript) engine.

**Important Note:** This project copied from: [quack](https://github.com/koush/). Original project supports only Android but this version supports regular JVM.

Supported Java Versions
-----------------------

Oracle & OpenJDK Java 8, 11.

Both the JRE and the JDK are suitable for use with this library.

Stability
---------
This library is suitable for use in production systems.

Supported Platforms
-------------------
* Windows 8 & Windows 10 (64-bit) (MSVC 2017)
* Ubuntu (64-bit) (gcc)
* macOS Catalina (10.15) (clang)

Download
--------
[quickjs-1.0.0.jar](https://repo1.maven.org/maven2/io/webfolder/quickjs/1.0.0/quickjs-1.0.0.jar) - 1589 KB

How it is tested
----------------
quickjs is regularly tested on [github actions](https://github.com/webfolderio/quickjs/actions).

Integration with Maven
----------------------

To use the official release of quickjs, please use the following snippet in your `pom.xml` file.

Add the following to your POM's `<dependencies>` tag:

```xml
<dependency>
    <groupId>io.webfolder</groupId>
    <artifactId>quickjs</artifactId>
    <version>1.0.0</version>
</dependency>
```

License
-------
Licensed under the [Apache License](https://github.com/webfolderio/quickjs/blob/master/LICENSE).
