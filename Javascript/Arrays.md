---
deck: Mastermind my memory::Javascript
---

## Strings 
**Strings are iterable**, so you can use a spread operator to turn any string into an array of single-character strings: 

```
let digits = [..."0123456789ABCDEF"]; 
digits // => ["0","1","2","3","4","5","6","7","8","9","A","B","C","D","E","F"]
```

<!-- basicblock-start oid="ObsiYFr9cdPwlWPWQciVDZqw" -->
**How to remove easily duplicate elements from an array ?** ::

Set objects are iterable and does not allowed duplication, so an easy way to remove duplicate elements from an array is to convert the array to a set and then immediately convert the set back to an array using the spread operator: 

```
let letters = [..."hello world"]; 
[...new Set(letters)] // => ["h","e","l","o"," ","w","r","d"]
```
<!-- basicblock-end -->

## Sparse array
<!-- basicblock-start oid="ObsVl6GqQiGCn5ECFx4mIMcX" -->
**What is a sparse array ?** ::

**A sparse array** is one in which the elements do not have contiguous indexes starting at 0. Normally, the length property of an array specifies the number of elements in the array. If the array is **sparse**, the value of the length property is greater than the number of elements

let a = new Array(5); // No elements, but a.length is 5.
a = []; // Create an array with no elements and length = 0. 
a[1000] = 0; // Assignment adds one element but sets length to 1001
<!-- basicblock-end -->

## forEach()

The **forEach()** method iterates through an array, invoking a function you specify for each element. As we’ve described, you pass the function as the first argument to forEach(). forEach() then invokes your function with three arguments: the value of the array element, the index of the array element, and the array itself.

```
data == [1,2,3,4,5]
// Now increment each array element 
data.forEach(function(v, i, a) { 
	a[i] = v + 1; 
}); 
// data == [2,3,4,5,6]
```

## map()

The **map()** method passes each element of the array on which it is invoked to the function you specify and returns an array containing the values returned by your function. 
```
For example: 
let a = [1, 2, 3]; 
a.map(x => x*x) 
// => [1, 4, 9]: the function takes input x and returns x*x
```

## filter()

The **filter()** method returns an array containing a subset of the elements of the array on which it is invoked. The function you pass to it should be **predicate**: a function that returns true or false. The predicate is invoked just as for forEach() and map(). If the return value is true, or a value that converts to true, then the element passed to the predicate is a member of the subset and is added to the array that will become the return value. 

```
let a = [5, 4, 3, 2, 1]; 
a.filter(x => x < 3) // => [2, 1]; values less than 3 
a.filter((x,i) => i%2 === 0) // => [5, 3, 1]; every other value
```

## find() and findIndex()

The **find()** and **findIndex()** methods are like filter() in that they iterate through your array looking for elements for which your predicate function returns a truthy value. Unlike filter(), however, these two methods stop iterating the first time the predicate finds an element. When that happens, find() returns the matching element, and findIndex() returns the index of the matching element.

## every()

<!-- basicblock-start oid="Obs3WFPTLR5k0xcg8DekYsD0" -->
**What the every() method does ?** ::
The **every()** method is like the mathematical “for all” quantifier ∀: it returns true if and only if your predicate function returns true for all elements in the array:

```
let a = [1,2,3,4,5]; 
a.every(x => x < 10) // => true: all values are < 10.
```
<!-- basicblock-end -->

## some()

<!-- basicblock-start oid="Obsl6mYOKc13ZYApGDa62EQj" -->
**What the some() method does ?** ::

The **some()** method is like the mathematical “there exists” quantifier ∃: it returns true if there exists at least one element in the array for which the predicate returns true and returns false if and only if the predicate returns false for all elements of the array:

```
let a = [1,2,3,4,5]; 
a.some(x => x%2===0) // => true; a has some even numbers. 
```
<!-- basicblock-end -->

## reduce() and reduceRight()

<!-- basicblock-start oid="Obs56FwRQ6S3BkQ5glYxXp84" -->
**What the reduce() and reduceRight() methods does ?** ::

The **reduce()** and **reduceRight()** methods combine the elements of an array, using the function you specify, to produce a single value. The second (optional) argument is an initial value to pass to the function. When you invoke reduce() with no initial value, it uses the first element of the array as the initial value.

```
let a = [1,2,3,4,5];
a.reduce((x,y) => x+y, 0) // => 15; the sum of the values 
a.reduce((x,y) => x*y, 1) // => 120; the product of the values 
a.reduce((x,y) => (x > y) ? x : y) // => 5; the largest of the values
```

**reduceRight()** works just like reduce(), except that it processes the array from highest index to lowest (right-to-left), rather than from lowest to highest.
<!-- basicblock-end -->

## flat() and flatMap()

<!-- basicblock-start oid="ObsDTuOzFNe0V3tYg4EgaDzp" -->
**What the flat() and flatMap() methods does ?** ::

In ES2019, **the flat()** method creates and returns a new array that contains the same elements as the array it is called on, except that any elements that are themselves arrays are “flattened” into the returned array. 

```
[1, [2, 3]].flat() // => [1, 2, 3]
```

If you want to flatten more levels, pass a number to flat(): 

```
let a = [1, [2, [3, [4]]]]; 
a.flat(1) // => [1, 2, [3, [4]]] 
a.flat(2) // => [1, 2, 3, [4]] 
a.flat(3) // => [1, 2, 3, 4] 
a.flat(4) // => [1, 2, 3, 4] 
```

The **flatMap()** method works just like the map() method (see “map()”) except that the returned array is automatically flattened as if passed to flat(). 
<!-- basicblock-end -->

## concat()

<!-- basicblock-start oid="Obs8mVYOT66N2ZcRjt7LqIhJ" -->
**What the concat() method does ?** ::

The **concat()** method creates and returns a new array that contains the elements of the original array on which concat() was invoked, followed by each of the arguments to concat() 

```
let a = [1,2,3]; 
---
a.concat(4, 5) // => [1,2,3,4,5] 
a.concat([4,5],[6,7]) // => [1,2,3,4,5,6,7]; 

arrays are flattened 
a.concat(4, [5,[6,7]]) // => [1,2,3,4,5,[6,7]]; 
but not nested arrays a // => [1,2,3]; 
```
<!-- basicblock-end -->

## push(), pop(), unshift(), shift()

<!-- basicblock-start oid="ObseoNddG6EQzxBlmFKuiTlQ" -->
**What the push(), pop(), unshift() and shift() methods does ?** ::

The **push()** method appends one or more new elements to the end of an array and returns the new length of the array. Unlike concat(), push() **does not flatten** array arguments. The **pop()** method does the reverse: it deletes the last element of an array, decrements the array length, and returns the value that it removed. 

The **unshift()** and **shift()** methods behave much like push() and pop(), except that they insert and remove elements from the beginning of an array rather than from the end. unshift() adds an element or elements to the beginning of the array, shifts the existing array elements up to higher indexes to make room, and returns the new length of the array.

```
let q = []; // q == [] 
q.push(1,2); // q == [1,2] 
q.shift(); // q == [2]; returns 1 
q.push(3) // q == [2, 3] 
q.shift() // q == [3]; returns 2 
q.shift() // q == []; returns 3 

let a = []; // a == [] 
a.unshift(1) // a == [1] 
a.unshift(2) // a == [2, 1] 
a = []; // a == [] 
a.unshift(1,2) // a == [1, 2] — 
```
<!-- basicblock-end -->

## slice() and splice()

<!-- basicblock-start oid="ObsSigiym8ZNwEOYTj5d2fRg" -->
**What the slice() and splice() method does ?** ::

The **slice()** method returns a slice, or subarray, of the specified array. Its two arguments specify the start and end of the slice to be returned. The returned array contains 

```
let a = [1,2,3,4,5]; 
a.slice(0,3); // Returns [1,2,3] 
a.slice(3); // Returns [4,5] 
a.slice(1,-1); // Returns [2,3,4] 
a.slice(-3,-2); // Returns [3]
```

**splice()** can delete elements from an array, insert new elements into an array, or perform both operations at the same time 

The first argument to splice() specifies the array position at which the insertion and/or deletion is to begin. The second argument specifies the number of elements that should be deleted from (spliced out of) the array.

```
let a = [1,2,3,4,5,6,7,8]; 
a.splice(4) // => [5,6,7,8]; a is now [1,2,3,4] 
a.splice(1,2) // => [2,3]; a is now [1,4] 
a.splice(1,1) // => [4]; a is now [1]
```
<!-- basicblock-end -->

## fill()
<!-- basicblock-start oid="Obs1ZaAtAA5rOjNtJl85JpF5" -->
**What the fill() method does ?** ::

The **fill()** method sets the elements of an array, or a slice of an array, to a specified value. It mutates the array it is called on, and also returns the modified array:

```
let a = new Array(5); // Start with no elements and length 5 
a.fill(0) // => [0,0,0,0,0]; fill the array with zeros 
a.fill(9, 1) // => [0,9,9,9,9]; fill with 9 starting at index 1 
a.fill(8, 2, -1) // => [0,9,8,8,9]; fill with 8 at indexes 2, 3
```
<!-- basicblock-end -->

## copyWithin()

<!-- basicblock-start oid="ObsIkZOmFMHho9kuKsIQTvNG" -->
**What the copyWithin() method does ?** ::

**copyWithin()** copies a slice of an array to a new position within the array. It modifies the array in place and returns the modified array, but it will not change the length of the array. The first argument specifies the destination index to which the first element will be copied. The second argument specifies the index of the first element to be copied. If this second argument is omitted, 0 is used. The third argument specifies the end of the slice of elements to be copied. If omitted, the length of the array is used.
 
 ```
 let a = [1,2,3,4,5]; 
 a.copyWithin(1) // => [1,1,2,3,4]: copy array elements up one 
 a.copyWithin(2, 3, 5) // => [1,1,3,4,4]: copy last 2 elements to index 2 
 a.copyWithin(0, -2) // => [4,4,3,4,4]: negative offsets work, too
```
<!-- basicblock-end -->

## indexOf(), lastIndexOf() and includes()

<!-- basicblock-start oid="ObsT6jukhDwnf2TTfLQCa5ad" -->
**What the indexOf(), lastIndexOf() and includes() method does ?** ::

**indexOf()** and **lastIndexOf()** search an array for an element with a specified value and return the index of the first such element found, or -1 if none is found. indexOf() searches the array from beginning to end, and lastIndexOf() searches from end to beginning: 

```
let a = [0,1,2,1,0]; 
a.indexOf(1) // => 1: a[1] is 1 
a.lastIndexOf(1) // => 3: a[3] is 1 
a.indexOf(3) // => -1: no element has value 3
```
---
indexOf() and lastIndexOf() take an optional second argument that specifies the array index at which to begin the search. If this argument is omitted, indexOf() starts at the beginning and lastIndexOf() starts at the end

The ES2016 **includes()** method takes a single argument and returns true if the array contains that value or false otherwise. It does not tell you the index of the value, only whether it exists. 
<!-- basicblock-end -->

## sort() 

<!-- basicblock-start oid="ObsiF2tX50euloNpGlW1hFVr" -->
**What the sort() method does ?** ::

**sort()** sorts the elements of an array in place and returns the sorted array. When sort() is called with no arguments, it sorts the array elements in alphabetical order (temporarily converting them to strings to perform the comparison, if necessary): 

```
let a = ["banana", "cherry", "apple"]; 
a.sort(); // a == ["apple", "banana", "cherry"]
```

To sort an array into some order other than alphabetical, you must pass a comparison function as an argument to sort() 

```
let a = [33, 4, 1111, 222]; 
a.sort(); // a == [1111, 222, 33, 4]; alphabetical order 
a.sort(function(a,b) { 
	// Pass a comparator 
	function return a-b; 
	// Returns < 0, 0, or > 0, depending on order 
}); 
// a == [4, 33, 222, 1111]
```
<!-- basicblock-end -->

## reverse() 

<!-- basicblock-start oid="undefined" -->
**What the reverse() method does ?** ::

The **reverse()** method reverses the order of the elements of an array and returns the reversed array. It does this in place; in other words, it doesn’t create a new array with the elements rearranged but instead rearranges them in the already existing array: 

```
let a = [1,2,3]; 
a.reverse(); // a == [3,2,1] 
```
<!-- basicblock-end -->