---
deck: Mastermind my memory::Javascript
---

## Definition

<!-- basicblock-start oid="Obs7hgDV255fssrsKg42RsMV" -->
**What is the definition of a JS class ? how to know if an object is an instance of a class ?** ::

In JavaScript, a **class** is a set of objects that inherit properties from the same prototype object. **two objects are instances of the same class if and only if they inherit from the same prototype**.

```
let F = function() {}; // This is a function object. 
let p = F.prototype; // This is the prototype object associated with F. 
let c = p.constructor; // This is the function associated with the prototype. 
c === F // => true: F.prototype.constructor === F for any F 
```

The critical feature of constructor invocations is that the prototype property of the constructor is used as the prototype of the new object. 

If we have an object r and want to know if it is a Range object, we can write: 
```
r instanceof Range // => true: r inherits from Range.prototype
```

Exemple : A Range class using a constructor, old way

```
// This is a constructor function that initializes new Range objects. 
// Note that it does not create or return the object. It just initializes this. 

function Range(from, to) { 
	// Store the start and end points (state) of this new range object. 
	// These are noninherited properties that are unique to this object. 
	this.from = from; 
	this.to = to; 
} 
// All Range objects inherit from this object. 

Range.prototype = {
	includes:function(x) { 
		return this.from <= x && x <= this.to; 
	}, 

	// A generator function that makes instances of the class iterable. 
	// Note that it only works for numeric ranges. 
	[Symbol.iterator]: function*() { 
			for(let x = Math.ceil(this.from); x <= this.to; x++) yield x; 
		}, 
	// Return a string representation of the range toString: 
	function() { 
		return "(" + this.from + "..." + this.to + ")"; 
	} 
}; 

// Here are example uses of this new Range class 
let r = new Range(1,3); // Create a Range object; note the use of new 
r.includes(2) // => true: 2 is in the range 
r.toString() // => "(1...3)" [...r] // => [1, 2, 3]; convert to an array via iterator 

```
<!-- basicblock-end -->

## ES6 classes way 

Classes have been part of JavaScript since the very first version of the language, but in ES6, they finally got their own syntax with the introduction of the **class keyword**.

```
class Buffer { 
	constructor() { 
		this.size = 0; 
		this.capacity = 4096; 
		this.buffer = new Uint8Array(this.capacity); 
	} 
} 
	
//With the new instance field syntax that is likely to be standardized, you could instead write: class Buffer { 
	size = 0; 
	capacity = 4096; 
	buffer = new Uint8Array(this.capacity); 
}
```

You can define a static method within a class body by prefixing the method declaration with the static keyword. 
**Static methods** are defined as properties of the constructor function rather than properties of the prototype object.

### # syntax 

<!-- basicblock-start oid="ObsuUOUPrcLXGMhJueQ4xtvc" -->
**How to make a field invisible and inacessible to any code outside of a body class ?** ::

If you use the instance field initialization syntax shown in the previous example to define a field whose name begins with # (which is not normally a legal character in JavaScript identifiers), that field will be usable (with the # prefix) within the class body but will be invisible and inaccessible (and therefore immutable) to any code outside of the class body. If, for the preceding hypothetical Buffer class, you wanted to ensure that users of the class could not inadvertently modify the size field of an instance, you could use a private #size field instead, then define a getter function to provide read-only access to the value: 

```
class Buffer { 
	#size = 0; 
	
	get size() { 
		return this.#size; 
	} 
}
```
<!-- basicblock-end -->

## Superclass and subclass 

<!-- basicblock-start oid="ObsbTo2wjS7QPE6HmviEOT0N" -->
**How to create a subclass A of a class B without using extends ?** ::

```
A.prototype = Object.create(B.prototype);
```

In object-oriented programming, a class B can extend or subclass another class A. We say that A is the **superclass** and B is the **subclass**. Instances of B inherit the methods of A. The class B can define its own methods, some of which may override methods of the same name defined by class A. If a method of B overrides a method of A, the overriding method in B often needs to invoke the overridden method in A. Similarly, the subclass constructor B() must typically invoke the superclass constructor A() in order to ensure that instances are completely initialized. 

In order to make Span a subclass of Range, we need to arrange for Span.prototype to inherit from Range.prototype. The key line of code in the preceding example is this one, and if it makes sense to you, you understand how subclasses work in JavaScript: 

```
Span.prototype = Object.create(Range.prototype);
```

```
// A trivial Array subclass that adds getters for the first and last elements. 

class EZArray extends Array { 
	get first() { 
		return this[0]; 
	} 
	
	get last() { 
		return this[this.length-1]; 
	} 
} 

let a = new EZArray(); 
a instanceof EZArray // => true: a is subclass instance 
a instanceof Array // => true: a is also a superclass instance. 
a.push(1,2,3,4); // a.length == 4; we can use inherited methods 
a.pop() // => 4: another inherited method 
a.first // => 1: first getter defined by subclass 
a.last // => 3: last getter defined by subclass 
a[1] // => 2: regular array access syntax still works. 
Array.isArray(a) // => true: subclass instance really is an array 
EZArray.isArray(a) // => true: subclass inherits static methods, too!
```

<!-- basicblock-end -->

## ES6 subclass way

The **extends** keyword makes it easy to create subclasses. But that does not mean that you should create lots of subclasses. If you want to write a class that shares the behavior of some other class, you can try to inherit that behavior by creating a subclass. But it is often easier and more flexible to get that desired behavior into your class by having your class create an instance of the other class and simply delegating to that instance as needed. You create a new class not by subclassing, but instead by wrapping or “composing” other classes. 

## Composition 

This delegation approach is often called “**composition**,” and it is an oft-quoted maxim of object-oriented programming that one should “favor composition over inheritance.