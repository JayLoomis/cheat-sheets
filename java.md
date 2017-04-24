# Java Quick Reference

## Naming conventions

There are pretty consistent standards for names in Java:

| Identifier type | Convention                    | Examples                                    |
| --------------- | ----------------------------- | ------------------------------------------- |
| class           | noun, camel-caps              | Customer, RoughCustomer                     |
| interface       | adjective/noun, camel-caps    | Runnable, ActionListener                    |
| method          | verb, lower-camel-caps        | doTheThing, rename, makeDefault             |
| variable        | noun, lower-camel-caps        | firstName, orderNumber, nonSquarePixelRatio |
| package         | noun, all-lower, run together | pricingcalculator                           |
| constant        | noun, all-upper, underscores  | RED, BLUE, MAX_WIDTH                        |

## Very basics

### Files

Code is organized into classes. Files must (really?) contain a single top-level
class and the filename must match the class name. It's case-sensitive!

### Command-line args

You can deal with command-line arguments as a simple array of strings, a
parameter called _args_ by convention.

A simple main method looks like this:

```java
public static void main(String[] args) {
    ...
}
```

You can access the args array directly, but doing anything complicated with
arguments this way would be difficult. I assume there's a library class to
handle command-line args more gracefully.

### Packages

*   Java packages are defined by directory structure.
*   Names are reverse URL plus identifier by convention:

    ```java
    package com.jayloomis.example
    ```
    
*   It's not clear to me how a package is different from a namespace (in C#
    for example.
    
#### Package directories

You set up your directory structure to match your package names, from a common
root directory.

So `com.jayloomis.example` identifies a directory:

```bash
...packages/com/jayloomis/example
```

#### Files in a package

Each file is still named to match a single, top-level class, but the package
information precedes the class definition.

The following is the top-level text in a file named `Hello1.java` that lives in
`<root>/com/jayloomis/example/`.

```java
package com.jayloomis.example;

public class Hello1 {
    ...
}
```

#### Building and running package files

Compile your source file from the root directory of your Java packages. Use the
path to the file:

```bash
javac com/jayloomis/example/Hello1.java
```

However, when you run the compiled code, use the package identifier:

```bash
java com.jayloomis.example.Hello1
```

## Variables

Java supports both primitive variables and objects.

### Primitives

Simple values that can be stored directly for fastest access.
Numbers, characters, Boolean. Strings are not primitive.

Most primitives have an equivalent helper class that trades the speed of a raw
primitive for the encapsulated functionality of a complex object. These are
mostly named identically to the primitive type, but with an initial capiatal
letter.

Helper classes are defined in java.lang (e.g. `java.lang.Double`)

#### Primitive data types

| Type   | Helper  | Description       |
| ------ | ------- | ----------------- |
| byte   | Byte    | 8-bit signed int  |
| short  | Short   | 16-bit signed int |
| int    | Integer | 32-bit signed int |
| long   | Long    | 64-bit signed int |
| float  | Float   | 32-bit float      |
| double | Double  | 64-bit float      |

#### Floating point imprecision

Java floating point values (both float and double) can be minutely imprecise.
You can get around this and force decimal precision by using the `BigDecimal`
class instead of the primitive. This can be important in applications where
absolute precision is important (financials, e.g.).

#### Casting of primitives

You can implicitly cast when widening the data type:

```java
byte byteValue1 = 42;
int intValue1 = byteValue1;
```

You can't go the other way:

```java
int intValue2 = 42;
byte byteBalue2 = intValue2;
\\ Compile error!
```

You can force cast, C-style:

```java
int intValue2 = 42;
byte byteValue2 = (byte)intValue2;
```

But when you do, the value is truncated:

```java
int intValue3 = 350;
byte byteValue3 = (byte)intValue3;
// byteValue3 == 94 (350 - 256)
```



<!----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8     -->
