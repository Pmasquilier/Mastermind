---
deck: Mastermind my memory::ReactJS
---

<!-- basicblock-start oid="Obsb6v4aR0pI7yQOClsNh5bN" -->

**What is a Side Effect ?**:: 
A "side effect" is anything that affects something outside the scope of the function being executed. 

**More :**
These can be, say, a network request, which has your code communicating with a third party (and thus making the request, causing logs to be recorded, caches to be saved or updated, all sorts of effects that are outside the function.

There are more subtle side effects, too. 
 - Changing the value of a closure-scoped variable is a side effect. 
 - Pushing a new item onto an array that was passed in as an argument is a side effect. 

Functions that execute without side effects are called "pure" functions: they take in arguments, and they return values. Nothing else happens upon executing the function. This makes the easy to test, simple to reason about, and functions that meet this description have all sorts of useful properties when it comes to optimization or refactoring.

Pure functions are deterministic (meaning that, given an input, they always return the same output), but that doesn't mean that all impure functions have side effects. 

Generating a random value within a function makes it impure, but isn't a side effect, for example. React is all about pure functions, and asks that you keep several lifecycle methods pure, so these are good questions to be asking.

<!-- basicblock-end -->