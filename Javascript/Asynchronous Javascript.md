12.5 Summary In this chapter, you have learned: The for/of loop and the ... spread operator work with iterable objects. An object is iterable if it has a method with the symbolic name [Symbol.iterator] that returns an iterator object. An iterator object has a next() method that returns an iteration result object. An iteration result object has a value property that holds the next iterated value, if there is one. If the iteration has completed, then the result object must have a done property set to true. You can implement your own iterable objects by defining a [Symbol.iterator]() method that returns an object with a next() method that returns iteration result objects. You can also implement functions that accept iterator arguments and return iterator values. Generator functions (functions defined with — location: [16772]() ^ref-4132


At its most fundamental level, asynchronous programming in JavaScript is done with callbacks. A callback is a function that you write and then pass to some other function. That other function then invokes (“calls back”) your function when some condition is met or some (asynchronous) event occurs. The invocation of the callback function you provide notifies you of the condition or event, and sometimes, the invocation will include function arguments that provide additional details. — location: [16822]() ^ref-59576

---
One of the simplest kinds of asynchrony is when you want to run some code after a certain amount of time has elapsed. — location: [16832]() ^ref-32212

---
setTimeout(checkForUpdates, 60000); The first argument to setTimeout() is a function and the second is a time interval measured in milliseconds. — location: [16839]() ^ref-57704

---
Client-side JavaScript programs are almost universally event driven: rather than running some kind of predetermined computation, they typically wait for the user to do something and then respond to the user’s actions. The web browser generates an event when the user presses a key on the keyboard, moves the mouse, clicks a mouse button, or touches a touchscreen device. Event-driven JavaScript programs register callback functions for specified types of events in specified contexts, and the web browser invokes those functions whenever the specified events occur. These callback functions are called event handlers or event listeners, and they are registered with addEventListener(): — location: [16859]() ^ref-40480

---
let okay = document.querySelector('#confirmUpdateDialog button.okay'); — location: [16872]() ^ref-28752

---
okay.addEventListener('click', applyUpdate); — location: [16876]() ^ref-6008

---
Another common source of asynchrony in JavaScript programming is network requests. JavaScript running in the browser can fetch data from a web server — location: [16886]() ^ref-10619

---
A Promise is an object that represents the result of an asynchronous computation. That result may or may not be ready yet, and the Promise API is intentionally vague about this: there is no way to synchronously get the value of a Promise; you can only ask the Promise to call a callback function when the value is ready — location: [17028]() ^ref-10093

---
getJSON(url).then(jsonData => { // This is a callback function that will be asynchronously // invoked with the parsed JSON value when it becomes available. }); getJSON() starts an asynchronous HTTP request for the URL you specify and then, while that request is pending, it returns a Promise object. The Promise object defines a then() instance method. Instead of passing our callback function directly to getJSON(), we instead pass it to the then() method. When the HTTP response arrives, the body of that response is parsed as JSON, and the resulting parsed value is passed to the function that we passed to then(). — location: [17067]() ^ref-669

---
You can think of the then() method as a callback registration method like the addEventListener() method used for registering event handlers in client-side JavaScript. — location: [17076]() ^ref-33123

---
Asynchronous operations, particularly those that involve networking, can typically fail in a number of ways, and robust code has to be written to handle the errors that will inevitably occur. For Promises, we can do this by passing a second function to the then() method: getJSON("/api/user/profile").then(displayUserProfile, handleProfileError); — location: [17097]() ^ref-59937

---
When something goes wrong in a synchronous computation, it throws an exception that propagates up the call stack until there is a catch clause to handle it. — location: [17112]() ^ref-13298

---
Instead, Promise-based asynchronous computations pass the exception (typically as an Error object of some kind, though this is not required) to the second function passed to then(). — location: [17115]() ^ref-56850

---
We say that the promise has been fulfilled if and when the first callback is called. And we say that the Promise has been rejected if and when the second callback is called. If a Promise is neither fulfilled nor rejected, then it is pending. And once a promise is fulfilled or rejected, we say that it is settled — location: [17146]() ^ref-35097

---
One of the most important benefits of Promises is that they provide a natural way to express a sequence of asynchronous operations as a linear chain of then() method invocations, without having to nest each operation within the callback of the previous one. Here, for example, is a hypothetical Promise chain: fetch(documentURL) // Make an HTTP request .then(response => response.json()) // Ask for the JSON body of the response .then(document => { // When we get the parsed JSON return render(document); // display the document to the user }) .then(rendered => { // When we get the rendered document — location: [17164]() ^ref-27900

---
cacheInDatabase(rendered); // cache it in the local database. }) .catch(error => handle(error)); // Handle any errors that occur — location: [17183]() ^ref-13121

---
fetch().then().then() When more than one method is invoked in a single expression like this, we call it a method chain — location: [17231]() ^ref-63660

---
.catch() method of a Promise is simply a shorthand — location: [17369]() ^ref-57583

---
way to call .then() with null as the first argument and an error-handling callback as the second argument. Given any Promise p and a callback c, the following two lines are equivalent: p.then(null, c); p.catch(c); — location: [17369]() ^ref-8855

---
The .catch() shorthand is preferred because it is simpler and because the name matches the catch clause in a try/catch exception-handling statement — location: [17376]() ^ref-47613

---
In ES2018, Promise objects also define a .finally() method whose purpose is similar to the finally clause in a try/catch/finally statement. If you add a .finally() invocation to your Promise chain, then the callback you pass to .finally() will be invoked when the Promise you called it on settles. Your callback will be invoked if the Promise fulfills or rejects, and it will not be passed any arguments, so you can’t find out whether it fulfilled or rejected. — location: [17382]() ^ref-45253

---
suppose that transient network load issues are causing this to fail about 1% of the time. A simple solution might be to retry the query with a .catch() call: queryDatabase() .catch(e => wait(500).then(queryDatabase)) // On failure, wait and retry .then(displayTable) .catch(displayDatabaseError); If the hypothetical failures are truly random, then adding this one line of code should reduce your error rate from 1% to .01%. — location: [17509]() ^ref-10652

---
We’ve spent a lot of time talking about Promise chains for sequentially running the asynchronous steps of a larger asynchronous operation. Sometimes, though, we want to execute a number of asynchronous operations in parallel. The function Promise.all() can do this. Promise.all() takes an array of Promise objects as its input and returns a Promise. The returned Promise will be rejected if any of the input Promises are rejected. Otherwise, it will be fulfilled with an array of the — location: [17559]() ^ref-53528

---
fulfillment values of each of the input Promises. — location: [17568]() ^ref-13680

---
Promise.allSettled() takes an array of input Promises and returns a Promise, just like Promise.all() does. But Promise.allSettled() never rejects the returned Promise, and it does not fulfill that Promise until all of the input Promises have settled. — location: [17591]() ^ref-52028

---
ES2017 introduces two new keywords—async and await—that represent a paradigm shift in asynchronous JavaScript programming. These new keywords dramatically simplify the use of Promises and allow us to write Promise-based, asynchronous code that looks like synchronous code that blocks while waiting for network responses or other asynchronous events. — location: [17896]() ^ref-63438

---
The await keyword takes a Promise and turns it back into a return value or a thrown exception. Given a Promise object p, the expression await p waits until p settles. If p fulfills, then the value of await p is the fulfillment value of p. On the other hand, if p is rejected, then the await p expression throws the rejection value of p. — location: [17915]() ^ref-29588

---
async function getHighScore() { let response = await fetch("/api/user/profile"); let profile = await response.json(); return profile.highScore; } — location: [17936]() ^ref-52599

---
displayHighScore(await getHighScore()); — location: [17950]() ^ref-21711

---
getHighScore().then(displayHighScore).catch(console.error); — location: [17958]() ^ref-9035

---
Suppose that we’ve written our getJSON() function using async: async function getJSON(url) { let response = await fetch(url); let body = await response.json(); return body; } And now suppose that we want to fetch two JSON values with this function: let value1 = await getJSON(url1); let value2 = await getJSON(url2); — location: [17967]() ^ref-11703

---
In order to await a set of concurrently executing async functions, we use Promise.all() just as we would if working with Promises directly: let [value1, value2] = await Promise.all([getJSON(url1), getJSON(url2)]); — location: [17984]() ^ref-10265

---
Suppose you have an array of URLs: const urls = [url1, url2, url3]; You can call fetch() on each URL to get an array of Promises: const promises = urls.map(url => fetch(url)); We saw earlier in the chapter that we could now use Promise.all() to wait for all the Promises in the array to be fulfilled. But suppose we want the results of the first fetch as soon as they become available and don’t want to — location: [18058]() ^ref-64383

---
wait for all the URLs to be fetched. (Of course, the first fetch might take longer than any of the others, so this is not necessarily faster than using Promise.all().) Arrays are iterable, so we can iterate through the array of promises with a regular for/of loop: for(const promise of promises) { response = await promise; handle(response); } This example code uses a regular for/of loop with a regular iterator. But because this iterator returns Promises, we can also use the new for/await for slightly simpler code: for await (const response of promises) { handle(response); } In this case, the for/await loop just builds the await call into the loop and makes our code slightly more compact, but the two examples do exactly the same thing. Importantly, both examples will only work if they are within functions declared async; — location: [18068]() ^ref-30148

---
13.5 Summary In this chapter, you have learned: Most real-world JavaScript programming is asynchronous. Traditionally, asynchrony has been handled with events and callback functions. This can get complicated, however, because you can end up with multiple levels of callbacks nested inside other callbacks, and because it is difficult to do robust error handling. Promises provide a new way of structuring callback functions. If used correctly (and unfortunately, Promises are easy to use incorrectly), they can convert asynchronous code that would have been nested into linear chains of then() calls where one asynchronous step of a computation follows another. Also, Promises allow you to centralize your error-handling code into a single catch() call at the end of a chain of then() calls. The async and await keywords allow us to write asynchronous code that is Promise-based under the hood but that looks like synchronous code. This — location: [18337]() ^ref-50029

---
makes the code easier to understand and reason about. If a function is declared async, it will implicitly return a Promise. Inside an async function, you can await a Promise (or a function that returns a Promise) as if the Promise value was synchronously computed. Objects that are asynchronously iterable can be used with a for/await loop. You can create asynchronously iterable objects by implementing a [Symbol.asyncIterator]() method or by invoking an async function * generator function. Asynchronous iterators provide an alternative to “data” events on streams in Node and can be used to represent a stream of user input events in client-side JavaScript — location: [18347]() ^ref-37324

---
This chapter covers a number of advanced JavaScript features that are not commonly used in day-to-day programming but that may be valuable to programmers writing reusable libraries and of interest to anyone who wants to tinker with the details about how JavaScript objects behave. Many of the features described here can loosely be described as “metaprogramming”: if regular programming is writing code to manipulate data, then metaprogramming is writing code to manipulate other code. — location: [18372]() ^ref-27783
