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

| Type   | Helper    | Description                    |
| ------ | --------- | ------------------------------ |
| char   | Character | 16-bit unsigned (Unicode char) |
| byte   | Byte      | 8-bit signed int               |
| short  | Short     | 16-bit signed int              |
| int    | Integer   | 32-bit signed int              |
| long   | Long      | 64-bit signed int              |
| float  | Float     | 32-bit float                   |
| double | Double    | 64-bit float                   |

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

### Wrapper classes

Every primitive type in Java has a corresponding wrapper class (also called
_reference types_). These are classes that encapsulate a primitive value, and
that come with many convenience functions built in. To review:

| Wrapper   | Primitive |
| --------- | --------- |
| Boolean   | boolean   |
| Character | char      |
| Byte      | byte      |
| Short     | short     |
| Integer   | int       |
| Long      | long      |
| Float     | float     |
| Double    | double    |

These are called refernce types because they are stored as references, not as
primitive values. (That's Java-speak for pointers).

## Control structures
Java's control structures are very C-like, but with a few variations.

### if and kin
Just as in C:

#### Simple usage

```java
if(a){
    Thing b = new Thing();
    b.doSomething();
}
```

Just as with C, the Boolean statement inside the parantheses is followed by a code
block, so if it's a single statement, the curly braces are not required (but still
probably a good idea).

#### With else

```java
if(a){
    Thing b = new Thing();
    b.doSomething();
} else {
    OtherThing c = new OtherThing();
    c.doSomethingElse();
}
```

#### With else if

```java
if(a){
    Thing b = new Thing();
    b.doSomething();
} else if(y) {
    OtherThing c = new OtherThing();
    c.doSomethingElse();
} else {
    System.out.println("Nothing to do.");
}
```

### switch (thank the gods)

```java
switch(month){
    case "September":
    case "April":
    case "June":
    case "November":
        days = 30;
        break;
    case "February":
        if (isLeapYear())
            days = 29;
        else
            days = 28;
        break;
    // Of course, this only works in contexts where there is no danger of bogus
    //  data in the month variable. A more robust implementation would list the
    //  other months explicitly so that default could be the invalid month case.
    default:
        days = 31;
        break;
}
```

### for
For loops are just like C:

```java
for (int i = 0; i < numThings; i++){
    doSomething(i);
}
```

To review, the three parts are initialization, expression, and update.

-   Initialization happens once at the beginning of the statement.
-   Expression is evaluated at the top of each iteration:
    -   If true, the for's block runs.
    -   If false, the block isnot run and program execution resumes after the for.
-   The update expression (by convention it's usually i++) runs after each
    iteration where the block runs. A couple of points:
    1.  If the expression is true, the block always runs before the update, so an
        update of i++ is identical to ++i.
    2.  The update doesn't happen on the final iteration. This shouldn't matter,
        because the update should only be changing the locally defined iterator.

### Enhanced for

This is specific to Java (which is to say, not inherited from C). It simplifies
the common case of looping through the members of an iterable object or array.

```java
for (Thing t : listOfThings) {
    t.doSomething();
}
```
### while

Both pre and post:

```java
while(lives > 0) {
    game.play();
}
```

```java
do {
    game.playOneRound();
} while (stillPlaying)
```

## Common tasks and library biz

### Strings

Strings are objects that encapsulate an array of **char** values. Lots of default
functionality.

#### Formatting strings with concatenation

The concatenation operator is powerful. The system is smart enough to implicitly 
convert things to string when you need to. For example:

```java
int five = 5,
    six = 6,
    seven = 7,
    eight = 8,
    nine = 9,
    ten = 10;
    
String allTogetherNow = five + ", " + six + ", " + seven + ", " +
                        eight + ", " + nine + ", " + ten + " I love you!";
                        
System.out.println(allTogetherNow);
```

Prints out:

```
5, 6, 7, 8, 9, 10 I love you!
```

##### Important warning!!

Java might get confused if you rely to carelessly on implicit conversion to strings.
Here are some variations of the string formatting from the previous example:

```java
String allTogetherNow = five + six + seven + eight + nine + ten + " I love you!";
```

Prints:

```
45 I love you!
```

But this version:

```java
String allTogetherNow = "" + five + six + seven + eight + nine + ten + " I love you!";
```

Prints:
```
5678910 I love you!
```

However, if you find yourself needing to trick the compiler with empty strings,
you should consider that there's probably a better way to do what you want.

#### Formatting strings, C-style

String handling is one place where Java's tendency to support an old-school
paradigm from C while also providing a more modern approach is most apparent.
For example, you can format your strings like C's **sprintf** by using
**String.format**:

```java
String allTogetherNow = String.format("%d, %d, %d, %d, %d, %d I love you!", five, 
                                      six, seven, eight, nine, ten);
```

Just as with **sprintf**, you can get much more complicated with your formatting.

### Shell output

Printing to stdout follows the C paradigm to some degree. Use the methods of `System.out`:

##### `System.out.print`

Print a string without a trailing newline.

```java
System.out.print("Hip, hip, ");
```

##### `System.out.println`

Print a string with a trailing newline appended.

```java
System.out.println("Hooray!");
```

##### `System.out.format`

Print a formatted string (equivalent to `printf` in C).

```java
System.out.format("Hi, %s! You have %d new messages.", name, newMessageCount);
```

<!----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8     -->
