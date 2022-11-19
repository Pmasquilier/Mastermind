---
deck: Mastermind my memory::Javascript
---

There are three separate types that you need to understand to understand iteration in JavaScript. First, there are the iterable objects: these are types like Array, Set, and Map that can be iterated. Second, there is the iterator object itself, which performs the iteration. And third, there is the iteration result object that holds the result of each step of the iteration.

<!-- basicblock-start oid="Obs4gQHUrNnXrqGXWJOQSFuA"-->
**What is an iterable object, an iterator and an interation** ? ::
**An iterable object** is any object with a special iterator method that returns an iterator object. 
An **iterator** is any object with a next() method that returns an iteration result object. The most common iterator in JavaScript is the Array iterator, which returns each value in the associated array in sequence.
And an **iteration** result object is an object with properties named value and done. 

To iterate an iterable object, you first call its iterator method to get an iterator object. Then, you call the next() method of the iterator object repeatedly until the returned value has its done property set to true.
<!-- basicblock-end -->

<!-- basicblock-start oid="Obs02JryAv4nnSVdMzDecmwj"-->
**What is a generator ?** ::
**Generator** is a kind of iterator defined with powerful new ES6 syntax; it’s particularly useful when the values to be iterated are not the elements of a data structure, but the result of a computation. To create a generator, you must first define a generator function. A generator function is syntactically like a regular JavaScript function but is defined with the keyword function* rather than function. 

When you invoke a generator function, it does not actually execute the function body, but instead returns a generator object. This generator object is an iterator. Calling its next() method causes the body of the generator function to run from the start (or whatever its current position is) until it reaches a yield statement. yield is new in ES6 and is something like a return statement. The value of the yield statement becomes the value returned by the next() call on the iterator.

```
// A generator function that yields the set of one digit (base-10) primes. 

function* oneDigitPrimes() { 
	// Invoking this function does not run the code 
	yield 2; 
	// but just returns a generator object. Calling 
	yield 3; // the next() method of that generator runs 
	yield 5; // the code until a yield statement provides 
	yield 7; // the return value for the next() method. 
} 

// When we invoke the generator function, we get a generator 
let primes = oneDigitPrimes(); // A generator is an iterator object that iterates the yielded values primes.next().value // => 2 
primes.next().value // => 3 
primes.next().value // => 5 
primes.next().value // => 7
```
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsmsTJCKELRJyistgzQpVQn"-->
**What is the fundamental feature of generators ?** ::
The most common use of generator functions is to create iterators, but the fundamental feature of generators is that they allow us **to pause a computation, yield intermediate results, and then resume the computation later**. 
It is possible to use generators to mask asynchronous parts of your program so that your code appears sequential and synchronous, even though some of your function calls are actually asynchronous and depend on events from the network. 
<!-- basicblock-end -->

<!-- basicblock-start oid="Obs192ad4mfstpkauhgIlnCB"-->
**What is the return value of a the next() function of a generator ?** ::
The return value of the next() function is an object that has a value **property and/or a done property**. With typical iterators and generators, if the value property is defined, then the done property is undefined or is false. And if done is true, then value is undefined. But in the case of a generator that returns a value, the final call to next returns an object that has both value and done defined. The value property holds the return value of the generator function, and the done property is true, indicating that there are no more values to iterate.

```
function *oneAndDone() { 
	yield 1;
	return "done"; 
} 
// The return value does not appear in normal iteration. 
[...oneAndDone()] // => [1] // But it is available if you explicitly call next() 
let generator = oneAndDone(); 
generator.next() // => { value: 1, done: false} 
generator.next() // => { value: "done", done: true } // If the generator is already done, the return value is not returned again 
generator.next() // => { value: undefined, done: true }
```
<!-- basicblock-end -->