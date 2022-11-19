11.11 Summary Learning a programming language is not just about mastering the grammar. It is equally important to study the standard library so that you are familiar with all the tools that are shipped with the language. This chapter has documented JavaScript’s standard library, which includes: Important data structures, such as Set, Map, and typed arrays. The Date and URL classes for working with dates and URLs. JavaScript’s regular expression grammar and its RegExp class for textual pattern matching. JavaScript’s internationalization library for formatting dates, time, and numbers and for sorting strings. The JSON object for serializing and deserializing simple data structures and the console object for logging messages. — location: [16070]() ^ref-37083


There are three separate types that you need to understand to understand iteration in JavaScript. First, there are the iterable objects: these are types like Array, Set, and Map that can be iterated. Second, there is the iterator object itself, which performs the iteration. And third, there is the iteration result object that holds the result of each step of the iteration. — location: [16173]() ^ref-13700

---
An iterable object is any object with a special iterator method that returns an iterator object. An iterator is any object with a next() method that returns an iteration result object. And an iteration result object is an object with properties named value and done. To iterate an iterable object, you first call its iterator method to get an iterator object. Then, you call the next() method of the iterator object repeatedly until the returned value has its done property set to true. — location: [16176]() ^ref-50564

---
generator is a kind of iterator defined with powerful new ES6 syntax; it’s particularly useful when the values to be iterated are not the elements of a data structure, but the result of a computation. To create a generator, you must first define a generator function. A generator function is syntactically like a regular JavaScript function but is defined with the keyword function* rather than function. — location: [16406]() ^ref-15513

---
invoke a generator function, it does not actually execute the function body, but instead returns a generator object. This generator object is an iterator. Calling its next() method causes the body of the generator function to run from the start (or whatever its current position is) until it reaches a yield statement. yield is new in ES6 and is something like a return statement. The value of the yield statement becomes the value returned by the next() call on the iterator. An example makes this clearer: // A generator function that yields the set of one digit (base-10) primes. function* oneDigitPrimes() { // Invoking this function does not run the code yield 2; // but just returns a generator object. Calling yield 3; // the next() method of that generator runs yield 5; // the code until a yield statement provides yield 7; // the return value for the next() method. } // When we invoke the generator function, we get a generator let primes = oneDigitPrimes(); // A generator is an iterator object that iterates the yielded values primes.next().value // => 2 primes.next().value // => 3 primes.next().value // => 5 primes.next().value // => 7 — location: [16419]() ^ref-48559

---
The most common use of generator functions is to create — location: [16630]() ^ref-47286

---
iterators, but the fundamental feature of generators is that they allow us to pause a computation, yield intermediate results, and then resume the computation later. — location: [16630]() ^ref-19688

---
The return value of the next() function is an object that has a value property and/or a done property. With typical iterators and generators, if the value property is defined, then the done property is undefined or is false. And if done is true, then value is undefined. But in the case of a generator that returns a value, the final call to next returns an object that has both value and done defined. The value property holds the return value of the generator function, and the done property is true, indicating that there are no more values to iterate. — location: [16639]() ^ref-52462

---
function *oneAndDone() { yield 1; — location: [16650]() ^ref-3205

---
return "done"; } // The return value does not appear in normal iteration. [...oneAndDone()] // => [1] // But it is available if you explicitly call next() let generator = oneAndDone(); generator.next() // => { value: 1, done: false} generator.next() // => { value: "done", done: true } // If the generator is already done, the return value is not returned again generator.next() // => { value: undefined, done: true } — location: [16652]() ^ref-23195

---
function* smallNumbers() { console.log("next() invoked the first time; argument discarded"); let y1 = yield 1; // y1 == "b" console.log("next() invoked a second time with argument", y1); let y2 = yield 2; // y2 == "c" console.log("next() invoked a third time with argument", y2); let y3 = yield 3; // y3 == "d" console.log("next() invoked a fourth time with argument", y3); return 4; } let g = smallNumbers(); console.log("generator created; no code runs yet"); let n1 = g.next("a"); // n1.value == 1 console.log("generator yielded", n1.value); let n2 = g.next("b"); // n2.value == 2 console.log("generator yielded", n2.value); let n3 = g.next("c"); // n3.value == 3 console.log("generator yielded", n3.value); let n4 = g.next("d"); // n4 == { value: 4, done: true } console.log("generator returned", n4.value); — location: [16679]() ^ref-52990

---
When this code runs, it produces the following output that demonstrates the back-and-forth between the two blocks of code: generator created; no code runs yet next() invoked the first time; argument discarded generator yielded 1 next() invoked a second time with argument b generator yielded 2 next() invoked a third time with argument c generator yielded 3 next() invoked a fourth time with argument d generator returned 4 — location: [16720]() ^ref-10890

---
Generators are a very powerful generalized control structure. They give us the ability to pause a computation with yield and restart it again at some arbitrary later time with an arbitrary input value. It is possible to use generators to create a kind of cooperative threading system within single-threaded JavaScript code. And it is possible to use generators to mask asynchronous parts of your program so that your code appears sequential and synchronous, even though some of your function calls are actually asynchronous and depend on events from the network. — location: [16760]() ^ref-36067

---
Trying to do these things with generators leads to code that is mind-bendingly hard to understand or to explain. It has been done, however, and the only really practical use — location: [16766]() ^ref-23424

---
case has been for managing asynchronous code. JavaScript now has async and await keywords (see Chapter 13) for this very purpose, however, and there is no longer any reason to abuse generators in this way. — location: [16767]() ^ref-1021

---
The for/of loop and the ... spread operator work with iterable objects. An object is iterable if it has a method with the symbolic name [Symbol.iterator] that returns an iterator object. An iterator object has a next() method that returns an iteration result object. An iteration result object has a value property that holds the next iterated value, if there is one. If the iteration has completed, then the result object must have a done property set to true. You can implement your own iterable objects by defining a [Symbol.iterator]() method that returns an object with a next() method that returns iteration result objects. You can also implement functions that accept iterator arguments and return iterator values. Generator functions (functions defined with — location: [16773]() ^ref-36487

---
function* instead of function) are another way to define iterators. When you invoke a generator function, the body of the function does not run right away; instead, the return value is an iterable iterator object. Each time the next() method of the iterator is called, another chunk of the generator function runs. Generator functions can use the yield operator to specify the values that are returned by the iterator. Each call to next() causes the generator function to run up to the next yield expression. The value of that yield expression then becomes the value returned by the iterator. When there are no more yield expressions, then the generator function returns, and the iteration is complete. — location: [16783]() ^ref-16039