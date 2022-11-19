---
deck: Mastermind my memory::ReactJS
---
<!-- basicblock-start oid="ObsSc3787kqMmv0XBQQEM7Om" -->
### What is Error Boundaries?:: 
Error boundaries are React components that **catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI** instead of the component tree that crashed. 

**As of React 16, errors that were not caught by any error boundary will result in unmounting of the whole React component tree.**
<!-- basicblock-end -->

<!-- basicblock-start oid="Obs29113zoxEQ9Bigo6L0D8v" -->
### How to create Error Boundaries Component?::
A class component becomes an error boundary if it defines either (or both) of the lifecycle methods static **getDerivedStateFromError()** or **componentDidCatch()** 

Use static getDerivedStateFromError()` to render a fallback UI after an error has been thrown. 
Use `componentDidCatch()` to log error information.
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsG5UYlp7KiSA9jOyYUyXIl" -->
### What is an Error Boundarie in React do not catch ?**::
 Error boundaries do **not** catch errors for:
-   Event handlers 
-   Asynchronous code (e.g. `setTimeout` or `requestAnimationFrame` callbacks)
-   Server side rendering
-   Errors thrown in the error boundary itself (rather than its children)
<!-- basicblock-end -->