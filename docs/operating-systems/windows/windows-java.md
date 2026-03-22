# Java dev tools for Windows

[← back](index.md)

## 1 Install/update JDK

## Check Java runtime and compiler

Check the installed versions of Java runtime and compiler:
```sh
java -version
javac -version
```

## Check JAR

Make sure that Java archive tool is present:
```sh
where jar
```
If JAR is not found try to find it in `Program Files` and add that folder to PATH.

## Update path

If some of the above commands are not working - this may be caused by the fact that java folder is not included in the PATH.  
Usually the path to java looks like:
```
c:\Program Files\Java\jdk-17.0.5\bin\
```

## Install JDK

If there's no JDK installed - download and install it:  
https://adoptium.net/temurin/releases