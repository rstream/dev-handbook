# Java dev tools for Linux

[← back](index.md)

## 1 Install/update JDK

Check the installed versions of Java runtime and compiler:
```sh
java -version
javac -version
```

If one of them is missing or they are outdated - update to more recent version.
Usually the package name is called like `java-21-openjdk-devel`.  
Suffix `-devel` is important, since you need not only a Java Runtime Environment (JRE) - but a **Java Dev Kit (JDK)**.

Get the list of available JDK packages:
```sh
zypper search java-??-openjdk-devel
```

Install the recent version:
```sh
sudo zypper install java-21-openjdk-devel
```

> Note: install `-devel` package version, since `java-21-openjdk` is just a runtime without dev tools.