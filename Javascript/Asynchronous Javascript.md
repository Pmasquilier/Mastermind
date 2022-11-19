---
deck: Mastermind my memory::Javascript
---

## Introduction

At its most fundamental level, asynchronous programming in JavaScript is done with callbacks. A callback is a function that you write and then pass to some other function. That other function then invokes (“calls back”) your function when some condition is met or some (asynchronous) event occurs. The invocation of the callback function you provide notifies you of the condition or event, and sometimes, the invocation will include function arguments that provide additional details.

One of the simplest kinds of asynchrony is when you want to run some code after a certain amount of time has elapsed.

```
setTimeout(checkForUpdates, 60000); // The first argument to setTimeout() is a function and the second is a time interval measured in milliseconds.
```

## Event driven JS 

Client-side JavaScript programs are almost universally event driven: rather than running some kind of predetermined computation, they typically wait for the user to do something and then respond to the user’s actions. The web browser generates an event when the user presses a key on the keyboard, moves the mouse, clicks a mouse button, or touches a touchscreen device. Event-driven JavaScript programs register callback functions for specified types of events in specified contexts, and the web browser invokes those functions whenever the specified events occur. These callback functions are called **event handlers** or **event listeners**, and they are registered with addEventListener(): 

```
let okay = document.querySelector('#confirmUpdateDialog button.okay');
okay.addEventListener('click', applyUpdate); 
```

Another common source of asynchrony in JavaScript programming is network requests. JavaScript running in the browser can fetch data from a web server.

## Promise 

A **Promise** is an object that represents the result of an asynchronous computation. That result may or may not be ready yet, and the Promise API is intentionally vague about this: there is no way to synchronously get the value of a Promise; you can only ask the Promise to call a callback function when the value is ready 

```
getJSON(url).then(jsonData => { 
	// This is a callback function that will be asynchronously 
	// invoked with the parsed JSON value when it becomes available. 
});
```

getJSON() starts an asynchronous HTTP request for the URL you specify and then, while that request is pending, it returns a Promise object. The Promise object defines a then() instance method. Instead of passing our callback function directly to getJSON(), we instead pass it to the then() method. When the HTTP response arrives, the body of that response is parsed as JSON, and the resulting parsed value is passed to the function that we passed to then().

You can think of the then() method as a callback registration method like the addEventListener() method used for registering event handlers in client-side JavaScript. 

Asynchronous operations, particularly those that involve networking, can typically fail in a number of ways, and robust code has to be written to handle the errors that will inevitably occur. For Promises, we can do this by passing a second function to the then() method: 

```
getJSON("/api/user/profile").then(displayUserProfile, handleProfileError);
```

When something goes wrong in a synchronous computation, it throws an exception that propagates up the call stack until there is a catch clause to handle it.

Instead, Promise-based asynchronous computations pass the exception (typically as an Error object of some kind, though this is not required) to the second function passed to then(). 

We say that the promise has been fulfilled if and when the first callback is called. And we say that the Promise has been rejected if and when the second callback is called. If a Promise is neither fulfilled nor rejected, then it is pending. And once a promise is fulfilled or rejected, we say that it is **settled**.

One of the most important benefits of Promises is that they provide a natural way to express a sequence of asynchronous operations as a linear chain of then() method invocations, without having to nest each operation within the callback of the previous one. Here, for example, is a hypothetical Promise chain: 

```
fetch(documentURL) // Make an HTTP request 
.then(response => response.json()) // Ask for the JSON body of the response 
.then(document => { // When we get the parsed JSON return render(document); 
	// display the document to the user 
}) 
.then(rendered => { 
	// When we get the rendered document 
	cacheInDatabase(rendered); // cache it in the local database. 
}) 
.catch(error => handle(error)); // Handle any errors that occur 
```

In ES2018, Promise objects also define a **.finally()** method whose purpose is similar to the finally clause in a try/catch/finally statement. If you add a .finally() invocation to your Promise chain, then the callback you pass to .finally() will be invoked when the Promise you called it on settles. Your callback will be invoked if the Promise fulfills or rejects, and it will not be passed any arguments, so you can’t find out whether it fulfilled or rejected.

<!-- basicblock-start oid="Obs7h2bDSNuJrpEVqUbdWDX6"-->
**What is the difference between Promise.all() and Promise.allSettled() ?** ::

Sometimes, we want to execute a number of asynchronous operations in parallel. The function **Promise.all()** can do this. Promise.all() takes an array of Promise objects as its input and returns a Promise. The returned Promise will be rejected if any of the input Promises are rejected. Otherwise, it will be fulfilled with an array of the fulfillment values of each of the input Promises.

**Promise.allSettled()** takes an array of input Promises and returns a Promise, just like Promise.all() does. But Promise.allSettled() never rejects the returned Promise, and it does not fulfill that Promise until all of the input Promises have settled. 
<!-- basicblock-end -->

ES2017 introduces two new keywords—**async** and **await**—that represent a paradigm shift in asynchronous JavaScript programming. These new keywords dramatically simplify the use of Promises and allow us to write Promise-based, asynchronous code that looks like synchronous code that blocks while waiting for network responses or other asynchronous events. 

The **await** keyword takes a Promise and turns it back into a return value or a thrown exception.

```
async function getHighScore() { 
	let response = await fetch("/api/user/profile"); 
	let profile = await response.json(); 
	return profile.highScore; 
}
displayHighScore(await getHighScore()); 
getHighScore().then(displayHighScore).catch(console.error); 
```

In order to await a set of concurrently executing async functions, we use Promise.all() just as we would if working with Promises directly: 

```
let [value1, value2] = await Promise.all([getJSON(url1), getJSON(url2)]);

// Suppose you have an array of URLs: 
const urls = [url1, url2, url3]; 

// You can call fetch() on each URL to get an array of Promises:
const promises = urls.map(url => fetch(url)); 
```

Arrays are iterable, so we can iterate through the array of promises with a regular for/of loop: 

```
for await (const response of promises) {
	handle(response); 
}
```
