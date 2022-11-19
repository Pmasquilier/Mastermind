---
deck: Mastermind my memory::Javascript
---
## JS object
<!-- basicblock-start oid="Obs7TxtlnwZK15j6hYzplC9D" -->

**What is a JS object ?** ::

An object is more than a simple **string-to-value map**. 

Ojects are **mutable** and **manipulated by reference** rather than by value. 

> If the variable x refers to an object and the code let y = x; is executed, the variable y holds a reference to the same object, not a copy of that object. Any modifications made to the object through the variable y are also visible through the variable x.

In addition to its name and value, each property has three property attributes: 
- The **writable** attribute specifies whether the value of the property can be set. 
- The **enumerable** attribute specifies whether the property name is returned by a for/in loop. 
- The **configurable** attribute specifies whether the property can be deleted and whether its attributes can be altered. 

JavaScript object also inherits the properties of another object, known as its “**prototype**.”
<!-- basicblock-end -->

## Prototype 

In addition to maintaining its own set of properties, a JavaScript object also inherits the properties of another object, known as its “**prototype**.” The methods of an object are typically inherited properties, and this **“prototypal inheritance**” is a key feature of JavaScript. 

We distinguish properties defined directly on an object and those that are inherited from a prototype object. JavaScript uses the term **own property** to refer to non-inherited properties.

Almost every JavaScript object has a second JavaScript object associated with it. This second object is known as a **prototype**, and the first object inherits properties from the prototype.

All objects created by object literals have the same prototype object, and we can refer to this prototype object in JavaScript code as **Object.prototype**.

### Object created with the new keyword

Objects created using the new keyword and a constructor invocation use the value of the prototype property of the constructor function as their prototype. 

> So the object created by new Object() inherits from Object.prototype, just as the object created by {} does. Similarly, the object created by new Array() uses Array.prototype as its prototype, and the object created by new Date() uses Date.prototype as its prototype. 

This can be confusing when first learning JavaScript. Remember: **almost all objects have a prototype, but only a relatively small number of objects have a prototype property. It is these objects with prototype properties that define the prototypes for all the other objects.** 

## Object.prototype

<!-- basicblock-start oid="ObsYUn2SdbrQx6v373lRs0VO" -->
**What is the specificity of Object.prototype ?**::

Object.prototype is one of the rare objects that has no prototype: it does not inherit any properties. Other prototype objects are normal objects that do have a prototype. Most built-in constructors (and most user-defined constructors) have a prototype that inherits from Object.prototype. 

> For example, Date.prototype inherits properties from Object.prototype, so a Date object created by new Date() inherits properties from both Date.prototype and Object.prototype. 
<!-- basicblock-end -->

<!-- basicblock-start oid="Obs5hSJK2bfhErzTLKrz2VWy" -->
**Name few universal object methods that are defined on Object.prototype** ::

- The **toString()** method takes no arguments; it returns a string that somehow represents the value of the object on which it is invoked. Because this default method does not display much useful information, many classes define their own versions of toString(). 
```
let s = { x: 1, y: 1 }.toString(); // s == "[object Object]" 
```

- **toLocaleString().** The purpose of this method is to return a localized string representation of the object. The default toLocaleString() method defined by Object doesn’t do any localization itself: it simply calls toString() and returns that value. The Date and Number classes define customized versions of toLocaleString() that attempt to format numbers, dates, and times according to local conventions. 

- The **valueOf()** method is much like the toString() method, but it is called when JavaScript needs to convert an object to some primitive type other than a string—typically, a number.

- There is also: **hasOwnProperty**, **isPrototypeOf** and **propertyIsEnumerable**
<!-- basicblock-end -->

## Prototype chain

This linked series of prototype objects is known as a **prototype chain**. 

JavaScript objects have a set of “own properties,” and they also inherit a set of properties from their prototype object. 

> Suppose you query the property x in the object o. If o does not have an own property with that name, the prototype object of o1 is queried for the property x. If the prototype object does not have an own property by that name, but has a prototype itself, the query is performed on the prototype of the prototype. This continues until the property x is found or until an object with a null prototype is searched.


## Get property of an object

<!-- basicblock-start oid="Obsamvf5ZRNWTAbeTJgnIdbk" -->
**Name four functions you can use to get an array of property names** ::

There are four functions you can use to get an array of property names: 
- **Object.keys()** returns an array of the names of the enumerable own properties of an object. It does not include non-enumerable properties, inherited properties, or properties whose name is a Symbol
- **Object.getOwnPropertyNames()** works like Object.keys() but returns an array of the names of non-enumerable own properties as well, as long as their names are strings. 
- **Object.getOwnPropertySymbols()** returns own properties whose names are Symbols, whether or not they are enumerable. 
- **Reflect.ownKeys()** returns all own property names, both enumerable and non-enumerable, and both string and Symbol.
<!-- basicblock-end -->

## Copy object 

<!-- basicblock-start oid="ObsVpMHwVGL0kzRFy3uEZlCA" -->
**How to copy the properties of one object to another object ?** ::

A common operation in JavaScript programs is needing to copy the properties of one object to another object. It is easy to do that with code like this: 

```
Object.assign(o, defaults); // overwrites everything in o with defaults 

Instead, what you can do is to create a new object, copy the defaults into it, and then override those defaults with the properties in o: 
o = Object.assign({}, defaults, o);

you can also express this object copy-and-override operation using the ... spread operator like this: 
o = {...defaults, ...o}; 
```
<!-- basicblock-end -->

## Object serialization 

<!-- basicblock-start oid="Obs1m13oDYfFrZ3HLhlzXCQS" -->
**What is object serialization ? How to serialize and restore JavaScript objects** ::
**Object serialization** is the process of converting an object’s state to a string from which it can later be restored. The functions **JSON.stringify()** and **JSON.parse()** serialize and restore JavaScript objects. These functions use the JSON data interchange format. **JSON stands for “JavaScript Object Notation”**, and its syntax is very similar to that of JavaScript object and array literals:

```
let o = {x: 1, y: {z: [false, null, ""]}}; // Define a test object 
let s = JSON.stringify(o); // s == '{"x":1,"y":{"z":[false,null,""]}}' 
let p = JSON.parse(s); // p == {x: 1, y: {z: [false, null, ""]}} 
```

JSON syntax is a subset of JavaScript syntax, and it cannot represent all JavaScript values.

> Objects, arrays, strings, finite numbers, true, false, and null are supported and can be serialized and restored. NaN, Infinity, and -Infinity are serialized to null. Date objects are serialized to ISO-formatted date strings (see the Date.toJSON() function), but JSON.parse() leaves these in string form and does not restore the original Date object. Function, RegExp, and Error objects and the undefined value cannot be serialized or restored. 

<!-- basicblock-end -->