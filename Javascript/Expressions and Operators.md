---
deck: Mastermind my memory::Javascript
---

## Equality operator

The === operator is known as the strict equality operator (or sometimes the identity operator), and it checks whether its two operands are “identical” using a strict definition of sameness. The == operator is known as the equality operator; it checks whether its two operands are “equal” using a more relaxed definition of sameness that allows type conversions. 

The == operator is a legacy feature of JavaScript and is widely considered to be a source of bugs. You should almost always use === instead of ==

## Eval

eval() expects one argument. If you pass any value other than a string, it simply returns that value. If you pass a string, it attempts to parse the string as JavaScript code, throwing a SyntaxError if it fails. If it successfully parses the string, then it evaluates the code and returns the value of the last expression or statement in the string or undefined if the last expression or statement had no value. If the evaluated string throws an exception, that exception propogates from the call to eval(). 

```
eval("function f() { return x+1; }"); 
```

## The first-defined operator

<!-- basicblock-start oid="ObsNDEa5FQtGgMsGt6DA5Rt3" -->
**How to write the first defined operator and how is it working ?** ::
The first-defined operator ?? evaluates to its first defined operand: if its left operand is not null and not undefined, it returns that value. Otherwise, it returns the value of the right operand. 

```
If maxWidth is defined, use that. Otherwise, look for a value in // the preferences object. If that is not defined, use a hardcoded constant. 
let max = maxWidth ?? preferences.maxWidth ?? 500; 
```
<!-- basicblock-end -->

## Delete operator 

delete is a unary operator that attempts to delete the object property or array element specified as its operand. 
```
let o = { x: 1, y: 2}; // Start with an object 
delete o.x; // Delete one of its properties 
```

## void 

void is a unary operator that appears before its single operand, which may be of any type. This operator is unusual and infrequently used; it evaluates its operand, then discards the value and returns undefined. 

```
let counter = 0; 
const increment = () => void counter++; increment() // => undefined 
counter // => 1
```