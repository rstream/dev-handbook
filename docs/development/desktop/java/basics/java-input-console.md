# Console input in Java

[← back](../index.md)

Read keyboard input in console with `Scanner`.

## Summary

- [Create scanner](#create-scanner) - connect `Scanner` to keyboard input
- [Read string line](#read-string-line) - read a full line
- [Read numbers](#read-numbers) - read numeric values
- [Close Scanner](#close-scanner) - free the input resource
- [Full example](#full-example) - complete console input program

## Create scanner
```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
```
> Note: created scanner should be closed after usage (full example below)

## Read string (line)
```java
String name = sc.nextLine();
```

## Read numbers
```java
int age = sc.nextInt();
double score = sc.nextDouble();
```

## Close Scanner
Close Scanner and free resource:
```java
sc.close();
```

## Full example
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter name: ");
        String name = sc.nextLine();

        System.out.print("Enter age: ");
        int age = sc.nextInt();

        System.out.printf("Hello, %s (%d)%n", name, age);
        sc.close();
    }
}
```
