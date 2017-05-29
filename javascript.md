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

### Using a generic `Object` as a dictionary

JS has no explicit type for a dictionary, but you can use a generic object.

#### Creating

As with many OO languages, there's a formally correct way:

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
  'aVal': 42,
  'anotherVal': 333,
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
