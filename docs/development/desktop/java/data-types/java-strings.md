# Strings in Java

[← back](../index.md)

Strings store text data.
Use them for names, messages, paths, input values, JSON text, and formatted output.

## Summary

- [Define strings](#define-strings) - create string values
- [Concatenate strings](#concatenate-strings) - join text values
- [String length](#string-length) - get character count
- [Access characters](#access-characters) - read characters by index
- [Compare strings](#compare-strings) - compare text content
- [Find text](#find-text) - search inside strings
- [Extract substrings](#extract-substrings) - take part of a string
- [Replace text](#replace-text) - replace characters or text fragments
- [Trim whitespace](#trim-whitespace) - remove leading and trailing spaces
- [Change case](#change-case) - convert to lower or upper case
- [Split and join strings](#split-and-join-strings) - convert between strings and arrays/lists
- [Format strings](#format-strings) - build formatted text
- [Convert strings and bytes](#convert-strings-and-bytes) - encode and decode text
- [Convert other types to string](#convert-other-types-to-string) - numbers, booleans, and objects to text
- [Parse values from strings](#parse-values-from-strings) - strings to numbers and booleans
- [JSON](#json) - convert objects to JSON and JSON to objects

## <a id="define-strings"></a>Define strings

```java
String name = "Alice";
String empty = "";
String text = new String("hello");
```

Usually prefer string literals (`"Alice"`) instead of `new String(...)`.

## <a id="concatenate-strings"></a>Concatenate strings

```java
String firstName = "Alice";
String lastName = "Smith";

String fullName = firstName + " " + lastName;
```

For many concatenations in a loop, use `StringBuilder`.

```java
StringBuilder sb = new StringBuilder();

sb.append("Name: ");
sb.append(name);
sb.append(", age: ");
sb.append(age);

String result = sb.toString();
```

## <a id="string-length"></a>String length

```java
String text = "hello";

int len = text.length(); // 5
```

## <a id="access-characters"></a>Access characters

Indexes start from `0`.

```java
String text = "hello";

char first = text.charAt(0); // 'h'
char last = text.charAt(text.length() - 1); // 'o'
```

## <a id="compare-strings"></a>Compare strings

Use `.equals()` to compare string content.

```java
String a = "hello";
String b = "hello";

boolean same = a.equals(b); // true
```

Use `.equalsIgnoreCase()` when letter case should not matter.

```java
boolean sameName = "Alice".equalsIgnoreCase("alice"); // true
```

Do not use `==` for string content comparison. It compares object references.

## <a id="find-text"></a>Find text

Use `.contains()` when you only need a boolean result.

```java
String email = "user@example.com";

if (email.contains("@")) {
    System.out.println("Looks like an email");
}
```

Use `.indexOf()` when you need the position.

```java
String filename = "report.pdf";

int dot = filename.indexOf(".");
```

`indexOf()` returns `-1` when text was not found.

## <a id="extract-substrings"></a>Extract substrings

```java
String text = "abcdef";

String firstThree = text.substring(0, 3); // "abc"
String fromThree = text.substring(3);     // "def"
```

The start index is included. The end index is excluded.

## <a id="replace-text"></a>Replace text

```java
String title = "hello world";

String slug = title.replace(" ", "-"); // "hello-world"
```

Use `.replaceAll()` for regular expressions.

```java
String cleaned = text.replaceAll("[^a-zA-Z0-9]", "");
```

## <a id="trim-whitespace"></a>Trim whitespace

```java
String raw = "  hello  ";

String trimmed = raw.trim();   // "hello"
String stripped = raw.strip(); // "hello"
```

`strip()` is Unicode-aware and is usually a better choice in modern Java.

## <a id="change-case"></a>Change case

```java
String name = "Alice";

String upper = name.toUpperCase(); // "ALICE"
String lower = name.toLowerCase(); // "alice"
```

## <a id="split-and-join-strings"></a>Split and join strings

```java
String csv = "java,strings,json";

String[] parts = csv.split(",");
String line = String.join(", ", parts);
```

With a list:

```java
import java.util.List;

List<String> tags = List.of("java", "strings", "json");

String line = String.join(", ", tags);
```

## <a id="format-strings"></a>Format strings

```java
String name = "Alice";
int count = 5;

String message = String.format("%s has %d messages", name, count);
```

For console output:

```java
System.out.printf("%s has %d messages%n", name, count);
```

## <a id="convert-strings-and-bytes"></a>Convert strings and bytes

Use a charset explicitly when converting between text and bytes.

```java
import java.nio.charset.StandardCharsets;

String text = "hello";

byte[] bytes = text.getBytes(StandardCharsets.UTF_8);
String decoded = new String(bytes, StandardCharsets.UTF_8);
```

## <a id="convert-other-types-to-string"></a>Convert other types to string

```java
int age = 25;
double score = 95.5;
boolean active = true;

String ageText = String.valueOf(age);
String scoreText = Double.toString(score);
String activeText = Boolean.toString(active);
```

Objects are converted with their `.toString()` method.

```java
String text = String.valueOf(user);
```

## <a id="parse-values-from-strings"></a>Parse values from strings

```java
String ageText = "25";
String scoreText = "95.5";
String activeText = "true";

int age = Integer.parseInt(ageText);
double score = Double.parseDouble(scoreText);
boolean active = Boolean.parseBoolean(activeText);
```

Invalid numeric strings throw `NumberFormatException`.

```java
try {
    int value = Integer.parseInt(input);
} catch (NumberFormatException e) {
    System.out.println("Not a valid integer");
}
```

## <a id="json"></a>JSON

Java does not have one built-in general-purpose JSON API in the standard library.
A common practical choice is Jackson.

Maven dependency:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.21.3</version>
</dependency>
```

Example class:

```java
public class User {
    public String name;
    public int age;
}
```

Convert object to JSON string:

```java
import com.fasterxml.jackson.databind.ObjectMapper;

ObjectMapper mapper = new ObjectMapper();

User user = new User();
user.name = "Alice";
user.age = 25;

String json = mapper.writeValueAsString(user);
```

Convert JSON string to object:

```java
String json = "{\"name\":\"Alice\",\"age\":25}";

User user = mapper.readValue(json, User.class);
```

Convert JSON string to `Map`:

```java
import com.fasterxml.jackson.core.type.TypeReference;
import java.util.Map;

Map<String, Object> data = mapper.readValue(
    json,
    new TypeReference<Map<String, Object>>() {}
);

String name = (String)data.get("name");
int age = ((Number)data.get("age")).intValue();
```
