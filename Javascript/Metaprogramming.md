---
deck: Mastermind my memory::Javascript
---

## Introduction

JavaScript objects have an extensible attribute and object properties have writable, enumerable, and configurable attributes, as well as a value and a getter and/or setter attribute. You can use these attributes to “lock down” your objects in various ways, including creating “sealed” and “frozen” objects. 

## Data and Accessor property 

Every object property is either a **data property** or an **accessor property**. A data property has a value, which may or may not be writable, whereas an accessor property has a getter-setter pair of functions to set and retrieve the property value.

<!-- basicblock-start oid="ObszPJc9TMTP3WkT6e1cWv8p"-->
**What are the four attributes of an accessor property and a data property ?** ::
The four attributes of an accessor property are **get, set, enumerable, and configurable**.
The four attributes of a data property are **value, writable, enumerable, and configurable**.
<!-- basicblock-end -->

<!-- basicblock-start oid="ObswwYyzBItPelRlih5CBpk0"-->
**How to obtain the property descriptor for a named property of a specified object ?** ::
Call **getOwnPropertyDescriptor()** :

```
Object.getOwnPropertyDescriptor(): // Returns {value: 1, writable:true, enumerable:true, configurable:true} 
Object.getOwnPropertyDescriptor({x: 1}, "x"); // Here is an object with a read-only accessor property const random = { 
	get octet() { 
		return Math.floor(Math.random()*256); 
	}, 
}; 
// Returns { get: /*func*/, set:undefined, enumerable:true, configurable:true} 
```
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsXa6NXCDuIagYal30cbkzt"-->
**How to set the attributes of a property or to create a new property with the specified attributes ?** ::
Call **Object.defineProperty(),** passing the object to be modified, the name of the property to be created or altered, and the property descriptor object: 

```
let o = {}; // Start with no properties at all 
// Add a non-enumerable data property x with value 1. 

Object.defineProperty(o, "x", { value: 1, writable: true, enumerable: false, configurable: true }); 
```
<!-- basicblock-end -->

## Methods of Object

**Object.assign()** only copies enumerable properties, and property values, not property attributes.

The **extensible attribute** of an object specifies whether new properties can be added to the object or not. Ordinary JavaScript objects are extensible by default, but you can change that with the functions described in this section. To determine whether an object is extensible, pass it to **Object.isExtensible()**. To make an object non-extensible, pass it to **Object.preventExtensions()**.

**Object.seal()** works like Object.preventExtensions(), but in addition to making the object non-extensible, it also makes all of the own properties of that object nonconfigurable. 

**Object.freeze()** locks objects down even more tightly. In addition to making the object non-extensible and its properties nonconfigurable, it also makes all of the object’s own data properties read-only.

It is important to understand that Object.seal() and Object.freeze() affect only the object they are passed: they have no effect on the prototype of that object. If you can query the prototype of any object by passing that object to Object.getPrototypeOf(): 

```
Object.getPrototypeOf({}) // => Object.prototype 
Object.getPrototypeOf([]) // => Array.prototype 
Object.getPrototypeOf(()=>{}) // => Function.prototype
```

To determine whether one object is the prototype of (or is part of the prototype chain of) another object, use the isPrototypeOf() method: 

```
let p = {x: 1}; // Define a prototype object. 
let o = Object.create(p); // Create an object with that prototype. 
p.isPrototypeOf(o) // => true: o inherits from p 
```

You can change the prototype of an object with Object.setPrototypeOf(): 

```
let o = {x: 1}; 
let p = {y: 2}; 
Object.setPrototypeOf(o, p); // Set the prototype of o to p 
o.y // => 2: o now inherits the property y
```

## Symbol 

<!-- basicblock-start oid="ObseJtREx2t4nQFfJn9NQRhj"-->
**What is the primary use of Symbol in term of Metaprogramming ?** ::
The **Symbol** type was added to JavaScript in ES6, and one of the primary reasons for doing so was to safely add extensions to the language without breaking compatibility with code already deployed on the web.
<!-- basicblock-end -->

The Symbol.iterator and Symbol.asyncIterator Symbols allow objects or classes to make themselves iterable or asynchronously iterable. 

## Template literals 

Strings within backticks are known as “**template literals**”. When an expression whose value is a function is followed by a template literal, it turns into a function invocation, and we call it a “**tagged template literal**.”

## Reflect object 

<!-- basicblock-start oid="ObsrWrcBiaMfhqLEyE0bhGwD"-->
**What is the Reflect object ?**:: 
The **Reflect object** defines a convenient set of functions, all in a single namespace, that mimic the behavior of core language syntax and duplicate the features of various pre-existing Object functions.
Although the Reflect functions do not provide any new features, they do group the features together in **one convenient API**. And, importantly, the set of Reflect functions maps one-to-one with the set of Proxy handler methods

```
Reflect.apply(f, o, args) // This function invokes the function f as a method of o (or invokes it as a function with no this value if o is null) and passes the values in the args array as arguments. It is equivalent to f.apply(o, args). 
```
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsFvLLs4jivEUUdeYPWX97o"-->
**What is the purpose of Proxy class ?** ::
The **Proxy class**, available in ES6 and later, is JavaScript’s most powerful metaprogramming feature. It allows us to write code that alters the fundamental behavior of JavaScript objects. When we create a Proxy object, we specify two other objects, the target object and the handlers object: 

```
let proxy = new Proxy(target, handlers); 
```

The resulting Proxy object has no state or behavior of its own. Whenever you perform an operation on it (read a property, write a property, define a new property, look up the prototype, invoke it as a function), **it dispatches those operations to the handlers object or to the target object**.

Proxies work this way for all of the fundamental operations: if an appropriate method exists on the handlers object, it invokes that method to perform the operation. 

And if that method does not exist on the handlers object, then the Proxy performs the fundamental operation on the target object. This means that a Proxy can obtain its behavior from the target object or from the handlers object. If the handlers object is empty, then the proxy is essentially a transparent wrapper around the target object: 

```
let t = { x: 1, y: 2 }; 
let p = new Proxy(t, {}); 
p.x // => 1 
delete p.y // => true: delete property y of the proxy 
t.y // => undefined: this deletes it in the target, too 
p.z = 3; // Defining a new property on the proxy 
t.z // => 3: defines the property on the target 
```

The following code, for example, uses Proxy to create a read-only wrapper for a target object. When code tries to read values from the object, those reads are forwarded to the target object normally. But if any code tries to modify the object or its properties, methods of the handler object throw a TypeError.

```
function readOnlyProxy(o) { 
	function readonly() { 
		throw new TypeError("Readonly"); 
		} 
	return new Proxy(o, { set: readonly, defineProperty: readonly, deleteProperty: readonly, setPrototypeOf: readonly, 
	}); 
} 
let o = { x: 1, y: 2 }; // Normal writable object 
let p = readOnlyProxy(o); // Readonly version of it 
p.x // => 1: reading properties works 
p.x = 2; // !TypeError: can't change properties 
delete p.y; // !TypeError: can't delete properties 
p.z = 3; // !TypeError: can't add properties p.__proto__ = {}; // !TypeError: can't change the prototype 
```
<!-- basicblock-end -->