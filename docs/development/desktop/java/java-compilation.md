# Java compilation

[← back](index.md)

## Compile java sources to byte-code

If you have a single file:

```sh
javac MyApp.java
```
Will product a file `MyApp.class`.

For multiple files:
```sh
javac *.java
```
or
```sh
javac MyApp.java Second.java Third.java
```
Will produce several `*.class` files.

## Run java apps

### Running source code (*.java) files

Need to use IDE for running *.java files before compilation to byte-code.  
Also it's possible to do if you have only 1 class:
```sh
java MyApp.java
```

### Running byte-code (*.class) files

To run - pass the main class as a parameter (without extension):
```sh
java MyApp
```
This will execute **MyApp.class** file  
Need to pass only 1 file (the main one), all dependent classes will be loaded automatically.

## Create JAR

### Create a manifest file

Create file `manifest.txt` with the following content:
```
Main-Class: MyApp

```
> Note: it's important to make a blank line at the end

### Compile everything into JAR

JAR file is a zip archive - a production representation of a java application.

#### Create JAR for a single class file

```sh
jar cfm MyApp.jar manifest.txt MyApp.class
```
#### Create JAR for multiple files

Simple way (all files from a current folder)
```sh
jar cfm MyApp.jar manifest.txt *.class
```

Flexible & recommended way (all files from a specific folder - recursive)
```sh
jar cfm MyApp.jar manifest.txt -C out .
```
This will do:
* change (temporarily) current folder to `./out`
* take all files in `./out` and all its subfolders
> Note: this syntax takes all files, not only `*.class` - so make sure there are no non-class files in this folder.

Flags:
* c = create
* f = output file name goes as a 1st param
* m = manifest included

jar command has strict param order:
1. flags
2. output file
3. manifest file
4. other files (compiled java sources)

**Running JAR**
```sh
java -jar MyApp.jar
```