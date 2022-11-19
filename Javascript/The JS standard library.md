 
Some datatypes, such as numbers and strings, objects, and arrays are so fundamental to JavaScript that we can consider them to be part of the language itself. This chapter covers other important but less fundamental APIs that can be thought of as defining the “**standard library**” for JavaScript: these are useful classes and functions that are built in to JavaScript and available to all JavaScript programs in both web browsers and in Node

## Set and WeakSet

A **set** is a collection of values, like an array is. Unlike arrays, however, sets are not ordered or indexed, and they do not allow duplicates: a value is either a member of a set or it is not a member; it is not possible to ask how many times a value appears in a set. The argument to the Set() constructor need not be an array: any iterable object (including other Set objects) is allowed:

The **add()** method takes a single argument; if you pass an array, it adds the array itself to the set, not the individual array elements. add() always returns the set it is invoked on, however, so if you want to add multiple values to a set, you can used chained method calls like 

```
s.add('a').add('b').add('c');
```

The delete() method also only deletes a single set element at a time. Unlike add(), however, delete() returns a boolean value. If the value you specify was actually a member of the set, then delete() removes it and returns true. Otherwise, it does nothing and returns false. 

the JavaScript Set class always remembers the order that elements were inserted in, and it always uses this order when you iterate a set: the first element inserted will be the first one iterated (assuming you haven’t deleted it first), and the most recently inserted element will be the last one iterated.

Sets are often described as “**unordered collections**.” This isn’t exactly true for the JavaScript Set class, however. A JavaScript set is unindexed: you can’t ask for the first or third element of a set the way you can with an array.

**WeakSet** implements a set of objects that does not prevent those objects from being garbage collected. 

## Map and WeakMap

A Map object represents a set of values known as keys, where each key has another value associated with (or “mapped to”) it. In a sense, a map is like an array, but instead of using a set of sequential integers as the keys, maps allow us to use arbitrary values as “indexes .

Like the add() method of Set, the set() method of Map can be chained, which allows maps to be initialized without using arrays of arrays: 

```
let m = new Map().set("one", 1).set("two", 2).set("three", 3);
```

If you want to iterate just the keys or just the associated values of a map, use the **keys**() and **values**() methods: 

The **WeakMap** class is a variant (but not an actual subclass) of the Map class that does not prevent its key values from being garbage collected. 

**Garbage collection** is the process by which the JavaScript interpreter reclaims the memory of objects that are no longer “reachable” and cannot be used by the program. A regular map holds “strong” references to its key values, and they remain reachable through the map, even if all other references to them are gone. The WeakMap, by contrast, keeps “weak” references to its key values so that they are not reachable through the WeakMap, and their presence in the map does not prevent their memory from being reclaimed.

The intended use of WeakMap is to allow you to associate values with objects without causing memory leaks. Suppose, for example, that you are writing a function that takes an object argument and needs to perform some time-consuming computation on that object. For efficiency, you’d like to cache the computed value for later reuse. If you use a Map object to implement the cache, you will prevent any of the objects from ever being reclaimed, but by using a WeakMap, you avoid this problem.  

**Typed arrays**, which are new in ES6, are much closer to the low-level arrays of those languages. Typed arrays are not technically arrays (Array.isArray() returns false for them), but they implement allmost of the array methods.
The elements of a typed array are all numbers. Unlike regular JavaScript numbers, however, typed arrays allow you to specify the type (signed and unsigned integers and IEEE-754 floating point) and size (8 bits to 64 bits) of the numbers to be stored in the array. You must specify the length of a typed array whenyou create it, and that length can never change. The elements of a typed array are always initialized to 0 when the array is created. 

JavaScript does not define a TypedArray class. Instead, there are 11 kinds of typed arrays, each with a different element type and constructor: 
- Int8Array() signed bytes 
- Uint8Array() unsigned bytes 
- Uint8ClampedArray() unsigned bytes without rollover 
- Int16Array() signed 16-bit short integers 
- Uint16Array() unsigned 16-bit short integers 
- Int32Array() signed 32-bit integers 
- Uint32Array() unsigned 32-bit integers 
- BigInt64Array() signed 64-bit BigInt values (ES2020) 
- BigUint64Array() unsigned 64-bit BigInt values (ES2020) 
- Float32Array() 32-bit floating-point value 
- Float64Array() 64-bit floating-point value

```
let rgba = new Uint8ClampedArray(4); // A 4-byte RGBA pixel value 
let sudoku = new Int8Array(81); // A 9x9 sudoku board When you create typed arrays in this way, the array elements are all guaranteed to be initialized to 0, 0n, or 0.0. But if you know the values you want in your typed array, you can also specify those values when you create the array. Each of the typed array constructors has static from() and of() factory methods that work like Array.from() and Array.of(): 
let white = Uint8ClampedArray.of(255, 255, 255, 0); // RGBA opaque white
```

## Regular expression

A **regular expression** is an object that describes a textual pattern. The JavaScript RegExp class represents regular expressions, and both String and RegExp define methods that use regular expressions to perform powerful pattern-matching and search-and-replace functions on text 

In JavaScript, regular expressions are represented by **RegExp objects**. RegExp objects may be created with the RegExp() constructor, of course, but they are more often created using a special literal syntax. Just as string literals are specified as characters within quotation marks, regular expression literals are specified as characters within a pair of slash (/) characters. 

the regular expression /java/ matches any string that contains the substring “java”.

Strings support four methods that use regular expressions. *

The simplest is **search()**. This method takes a regular expression argument and returns either the character position of the start of the first matching substring or −1 if there is no match

The **replace()** method performs a search-and-replace operation. It takes a regular expression as its first argument and a replacement string as its second argument. It searches the string on which it is called for matches with the specified pattern. If the regular expression has the g flag set, the replace() method replaces all matches in the string with the replacement string; otherwise, it replaces only the first match it finds. If the first argument to replace() is a string rather than a regular expression, the method searches for that string literally rather than converting it to a regular expression with the RegExp() constructor, as search() does.

The **match()** method is the most general of the String regular expression methods. It takes a regular expression as its only argument (or converts its argument to a regular expression by passing it to the RegExp() constructor) and returns an array that contains the results of the match, or null if no match is found. If the regular expression has the g flag set, the method returns an array of all matches that appear in the string.

The **matchAll()** method is defined in ES2020, and as of early 2020 is implemented by modern web browsers and Node. matchAll() expects a RegExp with the g flag set. Instead of returning an array of matching substrings like match() does, however, it returns an iterator that yields the kind of match objects that match() returns when used with a non-global RegExp. 

The last of the regular expression methods of the String object is **split().** This method breaks the string on which it is called into an array of substrings, using the argument as a separator.

The **RegExp()** constructor takes one or two string arguments and creates a new RegExp object. The first argument to this constructor is a string that contains the body of the regular expression—the text that would appear within slashes in a regular-expression literal. The second argument to RegExp() is optional. If supplied, it indicates the regular expression flags. It should be g, i, m, s, u, y, or any combination of those letters. 

The **test()** method of the RegExp class is the simplest way to use a regular expression. It takes a single string argument and returns true if the string matches the pattern or false if it does not match.

The RegExp **exec()** method is the most general and powerful way to use regular expressions. It takes a single string argument and looks for a match in that string. If no match is found, it returns null. If a match is found, however, it returns an array just like the array returned by the match() method for non-global searches.
Element 0 of the array contains the string that matched the regular expression, and any subsequent array elements contain the substrings that matched any capturing groups. The returned array also has named properties: the index property contains the character position at which the match occurred, and the input property specifies the string that was searched, and the groups property, if defined, refers to an object that holds the substrings matching the any named capturing groups. 

## Date 

The **Date** class is JavaScript’s API for working with dates and times. Create a Date object with the Date() constructor. With no arguments, it returns a Date object that represents the current date and time: 

```
let now = new Date(); // The current time 
```

If you pass one numeric argument, the Date() constructor interprets that argument as the number of milliseconds since the 1970 epoch: 

```
let epoch = new Date(0); // Midnight, January 1st, 1970, GMT 
```

One quirk of the Date API is that the first month of a year is number 0, but the first day of a month is number 1. If you omit the time fields, the Date() constructor defaults them all to 0, setting the time to midnight. 

To get or set the year of a Date object, for example, you would use getFullYear(), getUTCFullYear(), setFullYear(), or setUTCFullYear().

JavaScript represents dates internally as integers that specify the number of milliseconds since (or before) midnight on January 1, 1970, UTC time. Integers as large as 8,640,000,000,000,000 are supported, so JavaScript won’t be running out of milliseconds for more than 270,000 years. For any Date object, the getTime() method returns this internal value, and the setTime() method sets it. 

These millisecond values are sometimes called **timestamps**, and it is sometimes useful to work with them directly rather than with Date objects.

The timestamps returned by Date.now() are measured in milliseconds. A millisecond is actually a relatively long time for a computer, and sometimes you may want to measure elapsed time with higher precision. The **performance.now()** function allows this: it also returns a millisecond-based timestamp, but the return value is not an integer, so it includes fractions of a millisecond. The value returned by performance.now() is not an absolute timestamp like the Date.now() value is. Instead, it simply indicates how much time has elapsed since a web page was loaded or since the Node process started

## Throw, catch and error

The JavaScript throw and catch statements can throw and catch any JavaScript value, including primitive values. There is no exception type that must be used to signal errors. JavaScript does define an Error class, however, and it is traditional to use instances of Error or a subclass when signaling an error with throw. One good reason to use an Error object is that, when you create an Error, it captures the state of the JavaScript stack, and if the exception is uncaught, the stack trace will be displayed with the error message, which will help you debug the issue.

**Error objects** have two properties: message and name, and a toString() method. The value of the message property is the value you passed to the Error() constructor, converted to a string if necessary. For error objects created with Error(), the name property is always “Error”. The toString() method simply returns the value of the name property followed by a colon and space and the value of the message property. 

Although it is not part of the ECMAScript standard, Node and all modern browsers also define a stack property on Error objects. The value of this property is a multi-line string that contains a stack trace of the JavaScript call stack at the moment that the Error object was created. This can be useful information to log when an unexpected error is caught. 

In addition to the Error class, JavaScript defines a number of subclasses that it uses to signal particular types of errors defined by ECMAScript. These subclasses are **EvalError**, **RangeError**, **ReferenceError**, **SyntaxError**, **TypeError**, and **URIError**. You can use these error classes in your own code if they seem appropriate

You should feel free to define your own Error subclasses that best encapsulate the error conditions of your own program.

## Serialization 

When a program needs to save data or needs to transmit data across a network connection to another program, it must to convert its in-memory data structures into a string of bytes or characters than can be saved or transmitted and then later be parsed to restore the original in-memory data structures. This process of converting data structures into streams of bytes or characters is known as **serialization** (or marshaling or even pickling). 

JavaScript supports JSON serialization and deserialization with the two functions JSON.stringify() and JSON.parse()

## Internationalization 

The JavaScript internationalization API consists of the three classes **Intl.NumberFormat**, **Intl.DateTimeFormat**, and **Intl.Collator** that allow us to format numbers (including monetary amounts and percentages), dates, and times in locale-appropriate ways and to compare strings in locale-appropriate ways.

Users around the world expect numbers to be formatted in different ways. The Intl.NumberFormat class defines a format() method that takes all of these formatting possibilities into account.

## console

**console.assert()** If the first argument is truthy (i.e., if the assertion passes), then this function does nothing. But if the first argument is false or another falsy value, then the remaining arguments are printed as if they had been passed to console.error() with an “Assertion failed” prefix. 

**console.clear()** This function clears the console when that is possible. This works in browsers and in Node when Node is displaying its output to a terminal. — location: [15769]() ^ref-47247

**console.table()** This function is a remarkably powerful but little-known feature for producing tabular output, and it is particularly useful in Node programs that need to produce output that summarizes data. 

**console.trace()** This function logs its arguments like console.log() does, and, in addition, follows its output with a stack trace.

**console.count()** This function takes a string argument and logs that string, followed by the number of times it has been called with that string. This can be useful when debugging an event handler, for example

**console.group()** This function prints its arguments to the console as if they had been passed to console.log(), then sets the internal state of the console so that all subsequent console messages (until the next console.groupEnd() call) will be indented relative to the message that it just printed. This allows a group of related messages to be visually grouped with indentation.

**console.groupCollapsed()** This function works like console.group() except that in web browsers, the group will be “collapsed” by default and the messages it contains will be hidden unless the user clicks to expand the group 

**console.groupEnd()** This function takes no arguments. It produces no output of its own but ends the indentation and grouping caused by the most recent call to console.group() or console.groupCollapsed(). 

**console.time()** This function takes a single string argument, makes a note of the time it was called with that string, and produces no output. 

**console.timeLog()** This function takes a string as its first argument. If that string had previously been passed to console.time(), then it prints that string followed by the elapsed time since the console.time() call. If there are any additional arguments to console.timeLog(), they are printed as if they had been passed to console.log(). 

**console.timeEnd()** This function takes a single string argument. If that argument had previously been passed to console.time(), then it prints that argument and the elapsed time. After calling console.timeEnd(), it is no longer legal to call 

**console.timeLog()** without first calling console.time() again. 

## URL 
The URL class parses URLs and also allows modification (adding search parameters or altering paths, for example) of existing URLs. It also properly handles the complicated topic of escaping and unescaping the various components of a URL.

**encodeURI()** takes a string as its argument and returns a new string in which non-ASCII characters plus certain ASCII characters (such as space) are escaped. **decodeURI()** reverses the process. Characters that need to be escaped are first converted to their UTF-8 encoding, then each byte of that encoding is replaced with a %xx escape sequence, where xx is two hexadecimal digits.

**encodeURIComponent()** and **decodeURIComponent()** This pair of functions works just like encodeURI() and decodeURI() except that they are intended to escape individual components of a URI, so they also escape characters like /, ?, and # that are used to separate those components.