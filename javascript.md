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
  'yetAnother': 'This one's a string!'
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

<!--
----|----1----|----2----|----3----|----4----|----5----|----6----|----7----|----8
-->
