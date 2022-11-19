---
deck: Mastermind my memory::ReactJS
---
#Index

# Hooks at a glance

Hooks are a new addition in React 16.8. They let you use state and other React features without writing a class.

Hooks are functions that let you “hook into” React state and lifecycle features from function components. Hooks don’t work inside classes — **they let you use React without classes.**

## [[State Hook]]
This example renders a counter. When you click the button, it increments the value:

```
import React, { useState } from 'react';
function Example() {
 const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

Here, `useState` is a _Hook_. React will preserve this state between re-renders. `useState` returns a pair: the _current_ state value and a function that lets you update it.

It’s similar to `this.setState` in a class, except it doesn’t merge the old and new state together. (We’ll show an example comparing `useState` to `this.state` in [[State Hook]].

The only argument to `useState` is the initial state. In the example above, it is `0` because our counter starts from zero.

### Declaring multiple state variables

You can use the State Hook more than once in a single component:

React assumes that if you call `useState` many times, you do it in the same order during every render. 

## [[Hook Effect]]

You’ve likely performed data fetching, subscriptions, or manually changing the DOM from React components before. We call these operations [[Side effect]] (or “effects” for short) because they can affect other components and can’t be done during rendering.

<!-- basicblock-start oid="ObsEyVMcpgYzph4t72RIXZAg" -->
**What is a Hook Effect ?** :: 
The Effect Hook, `useEffect`, adds the ability to perform side effects from a function component. It serves the same purpose as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in React classes, but unified into a single API.
<!-- basicblock-end -->


## Rules of Hooks

<!-- basicblock-start oid="ObsgHc4IXVazNxzh0ZAIF4Je" -->
Hooks are JavaScript functions, but they impose two additional rules::
-   Only call Hooks **at the top level**. Don’t call Hooks inside loops, conditions, or nested functions.
-   Only call Hooks **from React function components** (Or from custom Hooks.). Don’t call Hooks from regular JavaScript functions. 
<!-- basicblock-end -->

## [[Custom Hooks]]

Sometimes, we want to reuse some stateful logic between components. Traditionally, there were two popular solutions to this problem: [[higher-order components]] and [[render props]]. Custom Hooks let you do this, but without adding more components to your tree.

 Hooks are a way to reuse _stateful logic_, not state itself. In fact, each _call_ to a Hook has a completely isolated state — so you can even use the same custom Hook twice in one component.

Custom Hooks are more of a convention than a feature. If a function’s name starts with ”`use`” and it calls other Hooks, we say it is a custom Hook. The `useSomething` naming convention is how our linter plugin is able to find bugs in the code using Hooks.

You can write custom Hooks that cover a wide range of use cases like form handling, animation, declarative subscriptions, timers, and probably many more we haven’t considered.

## [[Other Hooks]]

