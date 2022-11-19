### SPA Architectural Behaviors

Because the backend no longer has rendering logic, all document requests (the first request a user makes when they enter our URL) are served by a static file server
![[Pasted image 20221017212924.png]]

### Client-side Navigation

![[Pasted image 20221017213020.png]]

### SPA Pros and cons

By far the biggest pro here is the **developer experience**. That was the original driving force for the transition from PEMPAs to SPAs in the first place. Not having code duplication was an enormous benefit.

To make matters worse, SPAs also introduced several new problems:

1.  Bundle size - It kinda exploded. 
2.  Waterfalls - Because all the code for fetching data now lives within the JavaScript bundle, we have to wait for that to be downloaded before we can fetch the data. 
3.  Runtime performance - With so much client-side JavaScript to run, some lower-powered devices struggle to keep up.
4.  State management - This became a huge problem. As evidence for this, I offer the number of libraries available for solving this problem 😩. Before, the MPA would render our state in the DOM and we’d just reference/mutate that. Now we’re just getting JSON and we have to not only let the backend know when data has been updated, but keep the in-memory representation of that state up-to-date. This has all the marks of the challenges of caching (because that’s what it is), which is one of the hardest problems in software. In a typical SPA, state management represents 30-50% of the code people work on.

