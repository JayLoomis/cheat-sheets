# Java Script Cheat Sheet

Here are my notes as I learn JS (heaven help me).

## Data types

JS is a little wonky about how it types things:

-   It's dynamically typed.
-   There are some primative types.
-   There's a generic `Object` type that gets used as a container.

### Using `typeof`

The `typeof` operator lets you get the type of an object, but beware: the value
you get might not be the one you want. Search the Web for information about how
to predict what you'gg get, or just test it out when you need it.

```javascript
if (typeof someVariable == 'string'){
    var isString = true;
}
```

### Strings

Strings are objects. When you use a literal, you're essentially creating
a new String object. These two statements are functionally identical:

```javascript
var someString = 'This is a string.';

var someOtherString = new String('This is a string.');
```

#### More about string literals

##### Type of quotes

You can use single or double quotes to signify a string literal. These are 
equivalent:

```javascript
var s1 = "this is a string";
var s2 = 'this is a string';
```

##### Escaping characters

Use a backslash (`\`) in front of a character to escape it, C-style. There are
two common cases:

-   Non-visible characters, as in C: (`\n`, `\t`, etc.). 
    _Note that many of these are of little use in many JS scripts, because
    they have no effect on HTML rendering of strings._
    
-   Escaping the type of quote character used to define the string:
    
    ```javascript
    var s1 = 'What's wrong with this string?';
    var s2 = 'What\'s wrong with this string? Nothing!';
    ```

##### Dealing with long string literals

You can use the backslash character break string literals across lines. JS
continues defining the string on the next line:

```javascript
var s1 = 'String literal broken \
          over two lines.';
```

When you're working in HTML, the extra spaces before the text of the second
line is collapsed, so it works out fine. However, it can be confusing to have
those extra spaces in the object. One way out is to start the new line
unindented, but that's not very clean. Instead, it's almost always better to
just concatenate multiple strings:

```javascript
var s2 = 'Two strings ' +
         'concatenated.';
```
#### String methods

<!--
----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8
-->
### Using a generic `Object` as a dictionary

JS has no explicit type for a dictionary, but you can use a generic object.

#### Creating

As with many object-oriented languages, there's a formally correct way:

```javascript
var myDict = new Object();
```

And there's a shorthand way that everybody uses:

```javascript
var myDict = {};
```

You can add some key/value pairs at creation when using the shortcut:

```javascript
var myDict = {
  aVal: 42,
  anotherVal: 333,
  // Note that both identifiers and string literals can be used for keys.
  'yetAnother': 'This one\'s a string!'
};
```

#### Getting values

You can get values using object notation:

```javascript
var myCat = {'breed': 'oriental shorthair', 'age': 16, 'sex': 'neutered male'};

var breed = myCat.breed;
```

Or you can use dictionary notation:

```javascript
var breed = myCat['breed'];
```

**Note**: JS handles requests for nonexistent properties gracefully. It doesn't
throw an exception or otherwise register an error. Instead, it returns the
keyword `undefined`. What you do with that information is entirely up to you.

#### Setting values

You can arbitrarily set values, again using either object or dictionary
notation.

```javascript
var myDict = {};

// This works.
myDict.term1 = 'first term';

// So does this.
myDict['term2'] = 'second term';
```

Terms and definitions can be of basically any type.

#### Iterating

The easiest way is to do a `for` loop:

```javascript
for(var key in myDict) {
    var value = myDict[key];
}
```

# Miscelany

This is a section to contain anything I learn that's not an obvious part of
another section, or that would be hard to find is buried within a related topic.

## Null coalescing

This is a term that's new to me. Funnily enough, there isn't a null coalescing
operator in JavaScript, so I learned about it from the JavaScript workaround.

The basic idea is to define a specific operator syntax that covers a very
common case: you assign a variable to the value that mightbe null and you want
to assign some default value if it is.

```
a = someFunc(b);

if (a == null) {
    a = '';
}
```

### In other languages

There's a big list of other languages and their special null coalescing
operators on [Wikipedia](https://en.wikipedia.org/wiki/Null_coalescing_operator).

For example, in C#:

```c#
string pageTitle = suppliedTitle ?? "Default Title";
```

### In JavaScript

Instead of a special operator as such, JS uses a special case of the logical
OR:

```javascript
var pageTitle = (suppliedTitle || 'Default Title');
```
<!--
----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8
-->
