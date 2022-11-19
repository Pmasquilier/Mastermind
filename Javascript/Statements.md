---
deck: Mastermind my memory::Javascript
---

## Introduction

This chapter covers a wide variety of topics, and there is lots of reference material here that you may want to reread in the future as you continue to learn JavaScript. Some key points to remember, however, are these: Expressions are the phrases of a JavaScript program. Any expression can be evaluated to a JavaScript value. Expressions can also have side effects (such as variable assignment) in addition to producing a value. Simple expressions such as literals, variable references, and property accesses can be combined with operators to produce larger expressions. JavaScript defines operators for arithmetic, comparisons, Boolean logic, assignment, and bit manipulation, along with some miscellaneous operators, including the ternary conditional operator. The JavaScript + operator is used to both add numbers and concatenate strings. The logical operators && and || have special “short-circuiting” behavior and sometimes only evaluate one of their arguments. Common JavaScript idioms require you to understand the special behavior of these operators.

## Iterable objects
ES6 defines a new loop statement: for/of. The for/of loop works with iterable objects. Arrays, strings, sets, and maps are iterable: they represent a sequence or set of elements that you can loop or iterate through using a for/of loop. 
Objects are not (by default) iterable. Attempting to use for/of on a regular object throws a TypeError at runtime.

<!-- basicblock-start oid="ObsfXVfhZWs1kQJbD8ioZYoO" -->
**What are the 3 way to iterate through the properties of an iterable object ? ::**
If you want to iterate through the properties of an object, you can use 
- the **for/in** loop, 
- use **for/of with the Object.keys()** method: This works because Object.keys() returns an array of property names for an object, and arrays are iterable with for/of. 
- And if you are interested in both the keys and the values of an object’s properties, you can use **for/of with Object.entries()** and destructuring assignment:

```
let pairs = ""; 
for(let [k, v] of Object.entries(o)) { 
	pairs += k + v; 
} 
pairs // => "x1y2z3" — 
```
<!-- basicblock-end -->

### Strings are iterable 

Strings are iterable character-by-character in ES6: 

```
let frequency = {}; 
for(let letter of "mississippi") { 
if (frequency[letter]) { 
	frequency[letter]++; 
} else { 
	frequency[letter] = 1; 
	} 
} 
frequency // => {m: 1, i: 4, s: 4, p: 2}
```

Note that strings are iterated by Unicode codepoint, not by UTF-16 character. The string “I ❤ ” has a .length of 5 (because the two emoji characters each require two UTF-16 characters to represent). But if you iterate that string with for/of, the loop body will run three times, once for each of the three code points “I”, “❤”, and “.”.

### Set And Map are iterables

The built-in ES6 Set and Map classes are iterable. When you iterate a Set with for/of, the loop body runs once for each element of the set. You could use code like this to print the unique words in a string of text: 

```
let text = "Na na na na na na na na Batman!"; 
let wordSet = new Set(text.split(" ")); 
let unique = []; 
for(let word of wordSet) { 
	unique.push(word); 
} 
unique // => ["Na", "na", "Batman!"] 
```

Maps are an interesting case because the iterator for a Map object does not iterate the Map keys, or the Map values, but key/value pairs. Each time through the iteration, the iterator returns an array whose first element is a key and whose second element is the corresponding value. Given a Map m, you could iterate and destructure its key/value pairs like this: 

```
let m = new Map([[1, "one"]]); 
for(let [key, value] of m) { 
	key // => 1 
	value // => "one" 
}
```

### Asynchronous iterator

ES2018 introduces a new kind of iterator, known as an asynchronous iterator, and a variant on the for/of loop, known as the for/await loop that works with asynchronous iterators. 

Read chunks from an asynchronously iterable stream and print them out 

```
async function printStream(stream) { 
	for await (let chunk of stream) { 
		console.log(chunk); 
		} 
	} 
```

## break; continue; yield;

The break statement, used alone, causes the innermost enclosing loop or switch statement to exit immediately. Its syntax is simple: break; 

for(let i = 0; i < a.length; i++) { 
	if (a[i] === target) 
	break; 
} 

JavaScript also allows the break keyword to be followed by a statement label (just the identifier, with no colon): break labelname; 
When break is used with a label, it jumps to the end of, or terminates, the enclosing statement that has the specified label. It is a syntax error to use break in this form if there is no enclosing statement with the specified label. 
With this form of the break statement, the named statement need not be a loop or switch: 

```
let matrix = getData(); // Get a 2D array of numbers from somewhere 

// Now sum all the numbers in the matrix. 
let sum = 0, success = false; // Start with a labeled statement that we can break out of if errors occur 
computeSum: if (matrix) { 
	for(let x = 0; x < matrix.length; x++) { 
		let row = matrix[x]; 
		if (!row) break computeSum; 
	for(let y = 0; y < row.length; y++) { 
		let cell = row[y]; 
		if (isNaN(cell)) break computeSum; 
		sum += cell; 
		} 
	} 
success = true; 
} 
// The break statements jump here. 
If we arrive here with success == false // then there was something wrong 
```

The **continue statement** is similar to the break statement. Instead of exiting a loop, however, continue restarts a loop at the next iteration.
The continue statement can also be used with a label: continue labelname 
The continue statement, in both its labeled and unlabeled forms, can be used only within the body of a loop. 
Using it anywhere else causes a syntax error.
Like the break statement, the continue statement can be used in its labeled form within nested loops when the loop to be restarted is not the immediately enclosing loop. 

**The yield statement** is much like the return statement but is used only in ES6 generator functions to produce the next value in the generated sequence of values without actually returning.
In order to understand yield, you must understand iterators and generators.

## Error management 

**An exception** is a signal that indicates that some sort of exceptional condition or error has occurred. **To throw** an exception is to signal such an error or exceptional condition. **To catch** an exception is to handle it.

**An Error object** has a name property that specifies the type of error and a message property that holds the string passed to the constructor function. 

When an exception is thrown, the JavaScript interpreter immediately stops normal program execution and jumps to the nearest exception handler. 

Exception handlers are written using the catch clause of the **try/catch/finally statement**.
If an exception is thrown in a function that does not contain a try/catch/finally statement to handle it, the exception **propagates** up to the code that invoked the function. In this way, exceptions propagate up through the lexical structure of JavaScript methods and up the call stack. If no exception handler is ever found, the exception is treated as an error and is reported to the user. 

## the with statement 

**The with statement** runs a block of code as if the properties of a specified object were variables in scope for that code. It has the following syntax: with (object) statement 
This statement creates a temporary scope with the properties of object as variables and then executes statement within that scope. The with statement is forbidden in strict mode and should be considered deprecated in non-strict mode: **avoid using it whenever possible**.

The common use of the with statement is to make it easier to work with deeply nested object hierarchies. In client-side JavaScript, for example, you may have to type expressions like this one to access elements of an HTML form: document.forms[0].address.value.
If you need to write expressions like this a number of times, you can use the with statement to treat the properties of the form object like variables: 

```
with(document.forms[0]) { 
	// Access form elements directly here. For example: 
	name.value = ""; 
	address.value = ""; 
	email.value = ""; 
} 
This reduces the amount of typing you have to do: you no longer need to prefix each form property name with document.forms[0]. 

It is just as simple, of course, to avoid the with statement and write the preceding code like this: 
let f = document.forms[0]; 
f.name.value = ""; 
f.address.value = ""; 
f.email.value = "";
```

### use strict 

**"use strict"** is a directive introduced in ES5. 
The purpose of a "use strict" directive is to indicate that the code that follows (in the script or function) is strict code. 
Strict mode is a restricted subset of the language that fixes important language deficiencies and provides stronger error checking and increased security. 

- The with statement is not allowed in strict mode. In strict mode, all variables must be declared.
- In strict mode, assignments to nonwritable properties and attempts to create new properties on non-extensible objects throw a TypeError. 
- In strict mode, code passed to eval() cannot declare variables or define functions in the caller’s scope as it can in non-strict mode. Instead, variable and function definitions live in a new scope created for the eval(). This scope is discarded when the eval() returns. 
- In strict mode, the Arguments object in a function holds a static copy of the values passed to the function. 
- In strict mode, a SyntaxError is thrown if the delete operator is followed by an unqualified identifier such as a variable, function, or function parameter. (In nonstrict mode, such a delete expression does nothing and evaluates to false.) 
- In strict mode, an attempt to delete a nonconfigurable property throws a TypeError. (In non-strict mode, the attempt fails and the delete expression evaluates to false.) 
- In strict mode, it is a syntax error for an object literal to define two or more properties by the same name. (In non-strict mode, no error occurs.)
- In strict mode, it is a syntax error for a function declaration to have two or more parameters with the same name. (In non-strict mode, no error occurs.) In strict mode, octal integer literals (beginning with a 0 that is not followed by an x) are not allowed. (In non-strict mode, some implementations allow octal literals.) 
- In strict mode, the identifiers eval and arguments are treated like keywords, and you are not allowed to change their value. You cannot assign a value to these identifiers, declare them as variables, use them as function names, use them as function parameter names, or use them as the identifier of a catch block. 
- In strict mode, the ability to examine the call stack is restricted. arguments.caller and arguments.callee both throw a TypeError within a strict mode function. 