# Arrays in Java

[← back](../index.md)

Arrays store several values of the same type.
Java arrays have a fixed size. Use `ArrayList` when you need push/pop-like operations.

## Summary

- [Create arrays](#create-arrays) - fixed-size arrays
- [Access elements](#access-elements) - read and write by index
- [Array length](#array-length) - get fixed array size
- [Loop through arrays](#loop-through-arrays) - classic loop and for-each
- [Multidimensional arrays](#multidimensional-arrays) - arrays of arrays
- [Fill arrays](#fill-arrays) - set all elements to one value
- [Copy arrays](#copy-arrays) - clone or copy values
- [Slice arrays](#slice-arrays) - copy a range
- [Sort arrays](#sort-arrays) - sort values in place
- [Search arrays](#search-arrays) - find values in arrays
- [Compare arrays](#compare-arrays) - compare contents
- [Convert arrays to strings](#convert-arrays-to-strings) - readable output and joined text
- [Convert strings to arrays](#convert-strings-to-arrays) - split text into parts
- [Convert arrays and lists](#convert-arrays-and-lists) - move between array and `List`
- [Use ArrayList](#use-arraylist) - dynamic list with add/remove
- [Push and pop](#push-and-pop) - append and remove last element
- [Filter and map](#filter-and-map) - transform values with streams
- [Primitive arrays and streams](#primitive-arrays-and-streams) - `int[]`, `double[]`, and stream helpers

## Create arrays
Create an array with a fixed size:

```java
int[] numbers = new int[3]; // [0, 0, 0]
String[] names = new String[2]; // [null, null]
```

Create an array with initial values:

```java
int[] numbers = { 10, 20, 30 };
String[] colors = { "red", "green", "blue" };
```

## Access elements
Indexes start from `0`.

```java
String[] colors = { "red", "green", "blue" };

String first = colors[0]; // "red"
colors[1] = "black";
```

Invalid indexes throw `ArrayIndexOutOfBoundsException`.

## Array length
```java
int[] numbers = { 10, 20, 30 };

int count = numbers.length; // 3
```

`length` is a field, not a method.

## Loop through arrays
Use a classic loop when you need the index:

```java
String[] colors = { "red", "green", "blue" };

for (int i = 0; i < colors.length; i++) {
    System.out.println(i + ": " + colors[i]);
}
```

Use for-each when you only need values:

```java
for (String color : colors) {
    System.out.println(color);
}
```

## Multidimensional arrays
```java
int[][] matrix = {
    { 1, 2, 3 },
    { 4, 5, 6 }
};

int value = matrix[1][2]; // 6
```

## Fill arrays
```java
import java.util.Arrays;

int[] numbers = new int[5];

Arrays.fill(numbers, 10); // [10, 10, 10, 10, 10]
```

## Copy arrays
```java
import java.util.Arrays;

int[] original = { 10, 20, 30 };

int[] copy1 = original.clone();
int[] copy2 = Arrays.copyOf(original, original.length);
int[] bigger = Arrays.copyOf(original, 5); // [10, 20, 30, 0, 0]
```

Assignment does not copy array contents.

```java
int[] a = { 1, 2 };
int[] b = a; // same array object
```

## Slice arrays
Use `Arrays.copyOfRange(array, from, to)`.
The start index is included. The end index is excluded.

```java
import java.util.Arrays;

int[] numbers = { 10, 20, 30, 40, 50 };

int[] middle = Arrays.copyOfRange(numbers, 1, 4); // [20, 30, 40]
```

## Sort arrays
```java
import java.util.Arrays;

int[] numbers = { 30, 10, 20 };

Arrays.sort(numbers); // [10, 20, 30]
```

`Arrays.sort()` changes the original array.

## Search arrays
For sorted arrays, use `Arrays.binarySearch()`.

```java
import java.util.Arrays;

int[] numbers = { 10, 20, 30 };

int index = Arrays.binarySearch(numbers, 20); // 1
```

For unsorted arrays, use a loop.

```java
String[] names = { "Ann", "Bob", "Chris" };
String target = "Bob";
int index = -1;

for (int i = 0; i < names.length; i++) {
    if (names[i].equals(target)) {
        index = i;
        break;
    }
}
```

## Compare arrays
Use `Arrays.equals()` to compare contents.

```java
import java.util.Arrays;

int[] a = { 1, 2, 3 };
int[] b = { 1, 2, 3 };

boolean same = Arrays.equals(a, b); // true
```

Use `Arrays.deepEquals()` for nested arrays.

```java
int[][] a = { { 1, 2 }, { 3, 4 } };
int[][] b = { { 1, 2 }, { 3, 4 } };

boolean same = Arrays.deepEquals(a, b); // true
```

## Convert arrays to strings
Use `Arrays.toString()` for readable output.

```java
import java.util.Arrays;

int[] numbers = { 10, 20, 30 };

String text = Arrays.toString(numbers); // "[10, 20, 30]"
```

Use `String.join()` for string arrays.

```java
String[] tags = { "java", "arrays", "strings" };

String csv = String.join(",", tags); // "java,arrays,strings"
```

For primitive arrays, convert values first.

```java
import java.util.Arrays;
import java.util.stream.Collectors;

int[] numbers = { 10, 20, 30 };

String csv = Arrays.stream(numbers)
    .mapToObj(String::valueOf)
    .collect(Collectors.joining(","));
```

## Convert strings to arrays
```java
String csv = "java,arrays,strings";

String[] tags = csv.split(",");
```

`split()` uses a regular expression.
Escape special regex characters.

```java
String filename = "report.pdf";

String[] parts = filename.split("\\.");
```

## Convert arrays and lists
Convert array to fixed-size list view:

```java
import java.util.Arrays;
import java.util.List;

String[] colors = { "red", "green", "blue" };

List<String> list = Arrays.asList(colors);
```

Convert array to mutable `ArrayList`:

```java
import java.util.ArrayList;
import java.util.Arrays;

ArrayList<String> list = new ArrayList<>(Arrays.asList(colors));
```

Convert list to array:

```java
String[] array = list.toArray(new String[0]);
```

## Use ArrayList
`ArrayList` is a dynamic array-like collection.

```java
import java.util.ArrayList;

ArrayList<String> colors = new ArrayList<>();

colors.add("red");
colors.add("green");
colors.add("blue");

String first = colors.get(0);
colors.set(1, "black");
colors.remove(0);

int count = colors.size();
```

## Push and pop
Java arrays do not have `push()` or `pop()` methods.
Use `ArrayList` for this behavior.

Push: append to the end.

```java
import java.util.ArrayList;

ArrayList<String> stack = new ArrayList<>();

stack.add("first");
stack.add("second");
```

Pop: remove from the end.

```java
String last = stack.remove(stack.size() - 1); // "second"
```

Check for empty list before popping.

```java
if (!stack.isEmpty()) {
    String last = stack.remove(stack.size() - 1);
}
```

## Filter and map
Use streams to filter values.

```java
import java.util.Arrays;

String[] names = { "Ann", "Bob", "Chris" };

String[] longNames = Arrays.stream(names)
    .filter(name -> name.length() > 3)
    .toArray(String[]::new);
```

Use streams to transform values.

```java
String[] upper = Arrays.stream(names)
    .map(String::toUpperCase)
    .toArray(String[]::new);
```

## Primitive arrays and streams
Primitive arrays use specialized streams.

```java
import java.util.Arrays;

int[] numbers = { 10, 20, 30 };

int sum = Arrays.stream(numbers).sum();
double avg = Arrays.stream(numbers).average().orElse(0);
int max = Arrays.stream(numbers).max().orElse(0);
```

Convert `int[]` to `Integer[]`:

```java
Integer[] boxed = Arrays.stream(numbers)
    .boxed()
    .toArray(Integer[]::new);
```
