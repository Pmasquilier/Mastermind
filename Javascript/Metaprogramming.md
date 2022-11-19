The properties of a JavaScript object have names and values, of course, but each property also has three associated attributes that specify how that property behaves and what you can do with it: The writable attribute specifies whether or not the value of a property can change. The enumerable attribute specifies whether the property is enumerated by the for/in loop and the Object.keys() method. The configurable attribute specifies whether a property can be deleted and also whether the property’s attributes can be changed. — location: [18396]() ^ref-5677

---
Recall from §6.10.6 that, while “data properties” have a value, “accessor properties” have a getter and/or a setter method instead — location: [18413]() ^ref-59720

---
the four attributes of an accessor property are get, set, enumerable, and configurable. — location: [18420]() ^ref-63514

---
The four attributes of a data property are value, writable, enumerable, and configurable. — location: [18417]() ^ref-20446

---
To obtain the property descriptor for a named property of a specified object, call Object.getOwnPropertyDescriptor(): // Returns {value: 1, writable:true, enumerable:true, configurable:true} Object.getOwnPropertyDescriptor({x: 1}, "x"); // Here is an object with a read-only accessor property const random = { get octet() { return Math.floor(Math.random()*256); }, }; // Returns { get: /*func*/, set:undefined, enumerable:true, configurable:true} Object.getOwnPropertyDescriptor(random, "octet"); — location: [18432]() ^ref-49071

---
To set the attributes of a property or to create a new property with the specified attributes, call Object.defineProperty(), passing the object to be modified, the name of the property to be created or altered, and the property descriptor object: let o = {}; // Start with no properties at all // Add a non-enumerable data property x with value 1. Object.defineProperty(o, "x", { value: 1, writable: true, enumerable: false, configurable: true }); — location: [18457]() ^ref-25117

---
Object.assign() only copies enumerable properties, and property values, not property attributes. — location: [18556]() ^ref-10876

---
The extensible attribute of an object specifies whether new properties can be added to the object or not. Ordinary JavaScript objects are extensible by default, but you can change that with the functions described in this section. To determine whether an object is extensible, pass it to Object.isExtensible(). To make an object non-extensible, pass it to Object.preventExtensions(). — location: [18628]() ^ref-19308

---
Object.seal() works like Object.preventExtensions(), but in addition to making the object non-extensible, it also makes all of the own properties of that object nonconfigurable. — location: [18650]() ^ref-63320

---
Object.freeze() locks objects down even more tightly. In addition to making the object non-extensible and its properties nonconfigurable, it also makes all of the object’s own data properties read-only. — location: [18654]() ^ref-5234

---
It is important to understand that Object.seal() and — location: [18658]() ^ref-36644

---
Object.freeze() affect only the object they are passed: they have no effect on the prototype of that object. If — location: [18659]() ^ref-24868

---
You can query the prototype of any object by passing that object to Object.getPrototypeOf(): Object.getPrototypeOf({}) // => Object.prototype Object.getPrototypeOf([]) // => Array.prototype Object.getPrototypeOf(()=>{}) // => Function.prototype — location: [18693]() ^ref-55945

---
To determine whether one object is the prototype of (or is part of the prototype chain of) another object, use the — location: [18702]() ^ref-2732

---
isPrototypeOf() method: let p = {x: 1}; // Define a prototype object. let o = Object.create(p); // Create an object with that prototype. p.isPrototypeOf(o) // => true: o inherits from p — location: [18703]() ^ref-7167

---
You can, however, change the prototype of an object with Object.setPrototypeOf(): let o = {x: 1}; let p = {y: 2}; Object.setPrototypeOf(o, p); // Set the prototype of o to p o.y // => 2: o now inherits the property y — location: [18720]() ^ref-10379

---
The Symbol type was added to JavaScript in ES6, and one of the primary reasons for doing so was to safely add extensions to the language without breaking compatibility with code already deployed on the web. — location: [18757]() ^ref-40685

---
The Symbol.iterator and Symbol.asyncIterator Symbols allow objects or classes to make themselves iterable or asynchronously iterable. — location: [18770]() ^ref-17491

---
Strings within backticks are known as “template literals” — location: [19145]() ^ref-10039

---
When an expression whose value is a function is followed by a template literal, it turns into a function invocation, and we call it a “tagged template literal.” Defining a new tag function for use with tagged template literals can be thought of as metaprogramming, because tagged templates are often used to define DSLs—domain-specific languages—and defining a new tag function is like adding new syntax to JavaScript. Tagged template literals have been adopted by a number of frontend JavaScript packages. The GraphQL query language uses a gql`` tag function to allow queries to be embedded within JavaScript code. And the Emotion library uses a css`` tag function to enable CSS styles to be embedded in JavaScript. This section demonstrates how to write your own tag functions like these. — location: [19151]() ^ref-48544

---
As an example of a template tag function that returns a string, consider the following html`` template, which is useful when you want to safely interpolate values into a string of HTML. The tag performs HTML escaping on each of the values before using it to build the final string: function html(strings, ...values) { // Convert each value to a string and escape special HTML characters let escaped = values.map(v => String(v) .replace("&", "&amp;") .replace("<", "&lt;") .replace(">", "&gt;") .replace('"', "&quot;") .replace("'", "&#39;")); // Return the concatenated strings and escaped values let result = strings[0]; for(let i = 0; i < escaped.length; i++) { result += escaped[i] + strings[i+1]; } return result; } let operator = "<"; html`<b>x ${operator} y</b>` // => "<b>x &lt; y</b>" let kind = "game", name = "D&D"; — location: [19172]() ^ref-38284

---
html`<div class="${kind}">${name}</div>` // =>'<div class="game">D&amp;D</div>' — location: [19209]() ^ref-42294

---
The Reflect object is not a class; like the Math object, its properties simply define a collection of related functions. These functions, added in ES6, define an API for “reflecting upon” objects and their properties. There is little new functionality here: the Reflect object defines a convenient set of functions, all in a single namespace, that mimic the behavior of core language syntax and duplicate the features of various pre-existing Object functions. — location: [19254]() ^ref-62810

---
Although the Reflect functions do not provide any new — location: [19259]() ^ref-13598

---
features, they do group the features together in one convenient API. And, importantly, the set of Reflect functions maps one-to-one with the set of Proxy handler methods — location: [19260]() ^ref-13713

---
Reflect.apply(f, o, args) This function invokes the function f as a method of o (or invokes it as a function with no this value if o is null) and passes the values in the args array as arguments. It is equivalent to f.apply(o, args). — location: [19264]() ^ref-56272

---
The Proxy class, available in ES6 and later, is JavaScript’s most powerful metaprogramming feature. It allows us to write code that alters the fundamental behavior of JavaScript objects. — location: [19339]() ^ref-20741

---
The Reflect API described in §14.6 is a set of functions that gives us direct access to a set of fundamental operations on JavaScript objects. What the Proxy class does is allows us a way to implement those fundamental operations ourselves and create objects that behave in ways that are not possible for ordinary objects. When we create a Proxy object, we specify two other objects, the target object and the handlers object: let proxy = new Proxy(target, handlers); The resulting Proxy object has no state or behavior of its own. Whenever you perform an operation on it (read a property, write a property, define a new property, look up the prototype, invoke it as a function), it dispatches those operations to the handlers object or to the target object. — location: [19342]() ^ref-17583

---
Proxies work this way for all of the fundamental operations: if an appropriate method exists on the handlers object, it invokes that method to perform the operation. — location: [19357]() ^ref-48282

---
And if that method does not exist on the handlers object, then the Proxy performs the fundamental operation on the target object. This means that a Proxy can obtain its behavior from the target object or from the handlers object. If the handlers object is empty, then the proxy is essentially a transparent wrapper around the target object: let t = { x: 1, y: 2 }; let p = new Proxy(t, {}); p.x // => 1 delete p.y // => true: delete property y of the proxy t.y // => undefined: this deletes it in the target, too p.z = 3; // Defining a new property on the proxy t.z // => 3: defines the property on the target — location: [19360]() ^ref-45785

---
The following code, for example, uses Proxy to create a read-only wrapper for a target object. When code tries to read values from the object, those reads are forwarded to the target object normally. But if any code tries to modify the object or its properties, methods of the handler object throw a TypeError. — location: [19463]() ^ref-15715

---
function readOnlyProxy(o) { function readonly() { throw new TypeError("Readonly"); } return new Proxy(o, { set: readonly, defineProperty: readonly, deleteProperty: readonly, setPrototypeOf: readonly, }); } let o = { x: 1, y: 2 }; // Normal writable object let p = readOnlyProxy(o); // Readonly version — location: [19469]() ^ref-8179

---
of it p.x // => 1: reading properties works p.x = 2; // !TypeError: can't change properties delete p.y; // !TypeError: can't delete properties p.z = 3; // !TypeError: can't add properties p.__proto__ = {}; // !TypeError: can't change the prototype — location: [19486]() ^ref-56849

---
The readOnlyProxy() function defined earlier creates Proxy objects that are effectively frozen: any attempt to alter a property value or property attribute or to add or remove properties will throw an exception. — location: [19644]() ^ref-53434

---
readOnlyProxy() creates objects in an inconsistent state — location: [19649]() ^ref-34175

---
In this chapter, you have learned: JavaScript objects have an extensible attribute and object properties have writable, enumerable, and configurable attributes, as well as a value and a getter and/or setter attribute. You can use these attributes to “lock down” your objects in various ways, including creating “sealed” and “frozen” objects. — location: [19685]() ^ref-60491

---
JavaScript defines functions that allow you to traverse the prototype chain of an object and even to change the prototype of an object (though doing this can make your code slower). The properties of the Symbol object have values that are “well-known Symbols,” which you can use as property or method names for the objects and classes that you define. Doing so allows you to control how your object interacts with JavaScript language features and with the core library. For example, well-known Symbols allow you to make your classes iterable and control the string that is displayed when an instance is passed to Object.prototype.toString(). Prior to ES6, this kind of customization was available only to the native classes that were built in to an implementation. Tagged template literals are a function invocation syntax, and defining a new tag function is kind of like adding a new literal syntax to the language. Defining a tag function that parses its template string argument allows you to embed DSLs within JavaScript code. Tag functions also provide access to a raw, unescaped form of string literals where backslashes have no special meaning. The Proxy class and the related Reflect API allow low-level control over the fundamental behaviors of JavaScript objects. Proxy objects can be used as — location: [19690]() ^ref-15252

---
optionally revocable wrappers to improve code encapsulation, and they can also be used to implement nonstandard object behaviors (like some of the special case APIs defined by early web browsers). — location: [19700]() ^ref-36058

---
The JavaScript language was created in 1994 with the express purpose of enabling dynamic behavior in the documents displayed by web browsers. The language has evolved significantly since then, and at the same time, the scope and capabilities of the web platform have grown explosively. Today, JavaScript programmers can think of the web as a full-featured platform for application development. Web browsers specialize in the display of formatted text and images, but, like native operating systems, browsers also provide other services, including graphics, video, audio, networking, storage, and threading. JavaScript is the language that enables web applications to use the services provided by the web platform, and this chapter demonstrates how you can use the most important of these services. — location: [19710]() ^ref-55937