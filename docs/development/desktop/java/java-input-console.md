# Console input in Java

[← back](index.md)

Read keyboard input in console with `Scanner`.

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
