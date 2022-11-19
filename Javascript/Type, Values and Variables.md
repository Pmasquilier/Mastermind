---
deck: Mastermind my memory::Javascript
---

## Hexadecimal, binary and octal values

<!-- basicblock-start oid="Obsv1h7ueqzGJygc7DDkYnuM"-->
**What are the 4 differents base to describe an integer ?** ::

In addition to **base-10 integer** literals, JavaScript recognizes **hexadecimal (base-16) values**. A hexadecimal literal begins with 0x or 0X, followed by a string of hexadecimal digits. A hexadecimal digit is one of the digits 0 through 9 or the letters a (or A) through f (or F), which represent values 10 through 15. 

```
Here are examples of hexadecimal integer literals: 
0xff // => 255: (15*16 + 15) 
0xBADCAFE // => 195939070
```

In ES6 and later, you can also express integers in **binary (base 2)** or **octal (base 8)** using the prefixes 0b and 0o (or 0B and 0O) instead of 0x: 0b10101 

```
21: (1*16 + 0*8 + 1*4 + 0*2 + 1*1) 0o377 
255: (3*64 + 7*8 + 7*1) 
```
<!-- basicblock-end -->

## Separators in Numeric Literals 

You can use underscores within numeric literals to break long literals up into chunks that are easier to read: 
```
let billion = 1_000_000_000; // Underscore as a thousands separator.
```

## Floating-point representation

<!-- basicblock-start oid="ObswyAgdYC6G7EcXpAien1aV" -->
**What is the floating point representation and what problems can it lead ?** ::

The **IEEE-754 floating-point representation** used by JavaScript (and just about every other modern programming language) is a binary representation, which can exactly represent fractions like 1/2, 1/8, and 1/1024. 
Unfortunately, the fractions we use most commonly (especially when performing financial calculations) are decimal fractions: 1/10, 1/100, and so on. 
Binary floating-point representations cannot exactly represent numbers as simple as 0.1. JavaScript numbers have plenty of precision and can approximate 0.1 very closely. But the fact that this number cannot be represented exactly can lead to problems. 

*Consider this code:*
```
let x = .3 - .2; // thirty cents minus 20
cents let y = .2 - .1; // twenty cents minus 10 cents 
x === y // => false: the two values are not the same! 
x === .1 // => false: .3-.2 is not equal to .1 
y === .1 // => true: .2-.1 is equal to .1
```

If these floating-point approximations are problematic for your programs, consider using scaled integers. For example, you might manipulate monetary values as integer cents rather than fractional dollars.
<!-- basicblock-end -->

## BigInt

One of the newest features of JavaScript, defined in ES2020, is a new numeric type known as **BigInt**.
BigInt is a numeric type whose values are integers. The type was added to JavaScript mainly to allow the representation of 64-bit integers, which are required for compatibility with many other programming languages and APIs.

But BigInt values can have thousands or even millions of digits, should you have need to work with numbers that large.

## Template literals 

In ES6 and later, string literals can be delimited with backticks:
```
let s = `hello world`; 
```
This is more than just another string literal syntax, however, because these template literals can include arbitrary JavaScript expressions :
```
let name = "Bill"; let greeting = `Hello ${ name }.`;
// greeting == "Hello Bill." 
```
Everything between the ${ and the matching } is interpreted as a **JavaScript expression**. Everything outside the curly braces is **normal string literal text**.

<!-- basicblock-start oid="ObsSHe015uvVpiTu3dj7STAX" -->
**What is String.raw() ?**::
ES6 has one built-in tag function: **String.raw()**. It returns the text within backticks without any processing of backslash escapes: 
```
`\n`.length // => 1: the string has a single newline character 
String.raw`\n`.length // => 2: a backslash character and the letter n 
```
<!-- basicblock-end -->

## Falsy and truthy values 

<!-- basicblock-start oid="ObssApmxM8FHf53to4WFJxVq" -->
**What are the 6 falsy values ?** ::

The following values convert to, and therefore **work like, false**:
```
undefined null 0 -0 NaN "" // the empty string 
```
All other values, including all objects (and arrays) convert to, and work like, true. false, and the six values that convert to it, are sometimes called **falsy values**, and all other values are called **truthy**.
<!-- basicblock-end -->

## Symbols

<!-- basicblock-start oid="Obs9TLsfDVhWcqWNOumEpBW6" -->
**What is Symbols ?**::

**Symbols** were introduced in ES6 to serve as non-string property names. To understand Symbols, you need to know that JavaScript’s fundamental Object type is an unordered collection of properties, where each property has a name and a value. Property names are typically (and until ES6, were exclusively) strings. But in ES6 and later, Symbols can also serve this purpose:

```
let strname = "string name";
let symname = Symbol("propname");

typeof strname // "string"
typeof symname // "symbol"
```
<!-- basicblock-end -->

<!-- basicblock-start oid="Obso7qORUs2fGXwhOtHlGkOg" -->
**What's Symbol.for() function and what's the different whith Symbol() ?**::

The **Symbol.for()** function takes a string argument and returns a Symbol value that is associated with the string you pass. 
If no Symbol is already associated with that string, then a new one is created and returned; otherwise, the already existing Symbol is returned. 

That is, the Symbol.for() function is completely different than the Symbol() function: **Symbol() never returns the same value twice, but Symbol.for() always returns the same value when called with the same string.** 

```
let s = Symbol("shared");
let t = Symbol("shared");
s === t // false

let sfor = Symbol.for("shared");
let tfor = Symbol.for("shared");
sfor === tfor // true
```
<!-- basicblock-end -->

## Global object 

<!-- basicblock-start oid="ObscCwPScZaKjC2a6tNGAdgB" -->
**What is the global object and how to refer to it ?** ::

ES2020 defines **globalThis** as the standard way to refer to the global object in any context. 

**The global object** is a regular JavaScript object that serves a very important purpose: the properties of this object are the globally defined identifiers that are available to a JavaScript program.
<!-- basicblock-end -->

## Primitives types and object types

<!-- basicblock-start oid="ObsAQzjjkrgCMxqRfnJAiuxH" -->
**What are the two categories for JS types and are they include ?**::

JavaScript types can be divided into two categories: **primitive types** and **object types**. JavaScript’s 
- Primitive types include numbers, strings of text (known as strings), Boolean truth values (known as booleans), symbol null and undefined.
- Others are objects. Object (that is, a member of the type object) is a collection of properties where each property has a name and a value.
<!-- basicblock-end -->

There is a fundamental difference in JavaScript between primitive values (undefined, null, booleans, numbers, and strings) and objects (including arrays and functions).

### Primitives 

<!-- basicblock-start oid="ObsVNrBSedWIvZrTzSHDrrWR" -->
**What is the principal propertie of Primitives?** ::

**Primitives are immutable**: there is no way to change (or “mutate”) a primitive value.
Primitives are also compared by value: two values are the same only if they have the same value.

```
let person = 'Ernold'
let person = 'Ernold' 
person[0] = 'A' 
console.log(person) // output: Ernold

// we’re trying to mutate is a string, which is a primitive value — and all primitive values are immutable (unchangeable).
```

However, primitive values can’t change, but variables can!
Variables are not values, so the rules of mutability or immutability are not the same. **Variables just point to values.**

```
let person = 'Ernold' 
person = 'Arnold' 
console.log(person) // output: 'Ernold' 

// The code above works because we’re not mutating the string value, we’re not even touching it. Instead, we’re assigning a _new_ string value called `'Arnold'` to the `person` variable so it no longer references (points to) the `'Ernold'` string value.
```
<!-- basicblock-end -->

### Objects

Objects are not compared by value: **two distinct objects are not equal even if they have the same properties and values. And two distinct arrays are not equal even if they have the same elements in the same order**: 

Objects are different than primitives. First, they are mutable—their values can change: 

```
let o = { x: 1 }; // Start with an object o.x = 2; // Mutate it by changing the value of a property 

let o = {x: 1}, p = {x: 1}; // Two objects with the same properties 
o === p // => false: distinct objects are never equal let a = [], b = []; // Two distinct, empty arrays 
```

Objects are sometimes called reference types to distinguish them from JavaScript’s primitive types. Using this terminology, object values are references, and we say that objects are compared by reference: two object values are the same if and only if they refer to the same underlying object. 

```
let a = []; // The variable a refers to an empty array. 
let b = a; // Now b refers to the same array. 
b[0] = 1; // Mutate the array referred to by variable b. 
a[0] // => 1: the change is also visible through variable a. 
a === b // => true: a and b refer to the same object, so they are equal. 
```

## Number class

The **toString()** method defined by the **Number** class accepts an optional argument that specifies a radix, or base, for the conversion. If you do not specify the argument, the conversion is done in base 10. However, you can also convert numbers in other bases (between 2 and 36). 

For example: 
```
let n = 17; 
let binary = "0b" + n.toString(2); // binary == "0b10001"
```

The Number class defines three methods for these kinds of number-to-string conversions. 
- toFixed() converts a number to a string with a specified number of digits after the decimal point. It never uses exponential notation. 
- toExponential() converts a number to a string using exponential notation, with one digit before the decimal point and a specified number of digits after the decimal point (which means that the number of significant digits is one larger than the value you specify). 
- toPrecision() converts a number to a string with the number of significant digits you specify. It uses exponential notation

```
let n = 123456.789; 
n.toFixed(0) // => "123457" 
n.toFixed(2) // => "123456.79" 
n.toFixed(5) // => "123456.78900" 
n.toExponential(1) // => "1.2e+5" 
n.toExponential(3) // => "1.235e+5" 
n.toPrecision(4) // => "1.235e+5" 
n.toPrecision(7) // => "123456.8" 
n.toPrecision(10) // => "123456.7890"
```

## Object-to-primitive conversions

One reason for the complexity of JavaScript’s **object-to-primitive conversions** is that some types of objects have more than one primitive representation. Date objects, for example, can be represented as strings or as numeric timestamps. 

<!-- basicblock-start oid="Obsabs8ZP39nbo15UDjpRJoe" -->
**What are the 3 object-to-primitive conversions algorithms ?** ::

The JavaScript specification defines three fundamental algorithms for converting objects to primitive values: 
- **prefer-string**. This algorithm returns a primitive value, preferring a string value, if a conversion to string is possible. 
- **prefer-number.** This algorithm returns a primitive value, preferring a number, if such a conversion is possible. 
- **no-preference.** This algorithm expresses no preference about what type of primitive value is desired, and classes can define their own conversions. 

```
When an object needs to be converted to a string, JavaScript first converts it to a primitive using the prefer-string algorithm, then converts the resulting primitive value to a string, if necessary, — location.

When an object needs to be converted to a number, JavaScript first converts it to a primitive value using the prefer-number algorithm, then converts the resulting primitive value to a number, if necessary, following the rules.

Object-to-boolean conversions are trivial: all objects convert to true.
```

The + operator in JavaScript performs numeric addition and string concatenation. If either of its operands is an object, JavaScript converts them to primitive values using the no-preference algorithm. Once it has two primitive values, it checks their types. If either argument is a string, it converts the other to a string and concatenates the strings. Otherwise, it converts both arguments to numbers and adds them.

The other object conversion function is called **valueOf()**. The job of this method is less well defined: it is supposed to convert an object to a primitive value that represents the object, if any such primitive value exists. Objects are compound values, and most objects cannot really be represented by a single primitive value, so the default valueOf() method simply returns the object itself rather than returning a primitive.

```
let d = new Date(2010, 0, 1); // January 1, 2010, (Pacific time) 
d.valueOf() // => 1262332800000
```

With the toString() and valueOf() methods explained, we can now explain approximately how the three object-to-primitive algorithms work : 
- **The prefer-string algorithm** first tries the toString() method. If the method is defined and returns a primitive value, then JavaScript uses that primitive value (even if it is not a string!). If toString() does not exist or if it returns an object, then JavaScript tries the valueOf() method. If that method exists and returns a primitive value, then JavaScript uses that value. Otherwise, the conversion fails with a TypeError. 
- **The prefer-number** algorithm works like the prefer-string algorithm, except that it tries valueOf() first and toString() second. 
- **The no-preference algorithm** depends on the class of the object being converted. If the object is a Date object, then JavaScript uses the prefer-string algorithm. For any other object, JavaScript uses the prefer-number algorithm.
<!-- basicblock-end -->

## Const, Var and Let 

### Const

**Rule**: Declare everything with const, and then if we find that we do actually want to allow the value to vary, we switch the declaration to let. This may help prevent bugs by ruling out accidental changes to variables that we did not intend. 

It may seem surprising, but you can also use const to declare the loop “variables” for for/in and for/of loops, as long as the body of the loop does not reassign a new value. In this case, the const declaration is just saying that the value is constant for the duration of one loop iteration:

```
for(const datum of data) 
console.log(datum); 
```

### Var 
<!-- basicblock-start oid="Obs9MBHnKrKylbqZtvyHHRO9" -->
**What are the particularities of "Var"?**::

- **Variables declared with var do not have block scope**. Instead, they are scoped to the body of the containing function no matter how deeply nested they are inside that function. 
- One of the most unusual features of var declarations is known as **hoisting**. When a variable is declared with var, the declaration is lifted up (or “hoisted”) to the top of the enclosing function. The initialization of the variable remains where you wrote it, but the definition of the variable moves to the top of the function. So variables declared with var can be used, without error, anywhere in the enclosing function. 
<!-- basicblock-end -->

## Destructuring Assignment 

ES6 implements a kind of compound declaration and assignment syntax known as **destructuring assignment**

Here are simple destructuring assignments using arrays of values: 
```
let [x,y] = [1,2]; // Same as let x=1, y=2 
[x,y] = [x+1,y+1]; // Same as x = x + 1, y = y + 1
```

Notice how destructuring assignment makes it easy to work with functions that return arrays of values: 
```
// Convert [x,y] coordinates to [r,theta] polar coordinates 
function toPolar(x, y) { 
	return [Math.sqrt(x*x+y*y), Math.atan2(y,x)]; 
	} 

let [r,theta] = toPolar(1.0, 1.0); 
// r == Math.sqrt(2); theta == Math.PI/4
```

The number of variables on the left of a destructuring assignment does not have to match the number of array elements on the right. Extra variables on the left are set to undefined, and extra values on the right are ignored. 

```
let [x,y] = [1]; // x == 1; y == undefined 
[x,y] = [1,2,3]; // x == 1; y == 2
```

If you want to collect all unused or remaining values into a single variable when destructuring an array, use three dots (...)

```
let [x, ...y] = [1,2,3,4]; // y == [2,3,4] 
```
