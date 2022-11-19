---
deck: Mastermind my memory::ReactJS
---
# useEffect

## Effects Without Cleanup
```
 useEffect(() => {
    document.title = `You clicked ${count} times`;
  });
```

The _Effect Hook_ lets you perform side effects in function components:

If you’re familiar with React class lifecycle methods, you can think of `useEffect` Hook as `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` combined.

<!-- basicblock-start oid="Obsftug9i0MoP3PX6cM08Uw1" -->
**What does `useEffect` do?**::
By using this Hook, you tell React that your component needs to do something after render. React will remember the function you passed (we’ll refer to it as our “effect”), and call it later after performing the DOM updates.
<!-- basicblock-end -->

<!-- clozeblock-start oid="Obst21hUbre272CtF0ppg3nE" -->
**Does `useEffect` run after every render?** Yes! By default, it runs both after the first render _and_ after every update. Instead of thinking in terms of “mounting” and “updating”, you might find it easier to think that effects happen ==“after render”==.
<!-- clozeblock-end -->

## Effects with Cleanup
Sometimes, we need to clean some side effects. For example, **we might want to set up a subscription** to some external data source. In that case, it is important to clean up so that we don’t introduce a memory leak!

```
import React, { useState, useEffect } from 'react';

function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {    
  
	  function handleStatusChange(status) {
	        setIsOnline(status.isOnline);    
	    }    
	    
	    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
	    // Specify how to clean up after this effect:    
	    
		return function cleanup() {
			ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
		};  
	});
	
  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

<!-- basicblock-start oid="ObskJ6msXJw3ZIP5SeJV0rq9" -->
**Why did we return a function from our effect?**::
This is the optional cleanup mechanism for effects. Every effect may return a function that cleans up after it. This lets us keep the logic for adding and removing subscriptions close to each other. It's equivalent to componentWillUnmount.
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsiEi3Awb8AQY18jiqC6EWn" -->
**When exactly does React clean up an effect?**::
React performs the cleanup when the component unmounts. However, effects run for every render and not just once. This is why React _also_ cleans up effects from the previous render before running the effects next time.
<!-- basicblock-end -->

We don’t have to return a named function from the effect. We called it `cleanup` here to clarify its purpose, but you could return an arrow function or call it something different.

## Tips for Using Effects

### Tip: Use Multiple Effects to Separate Concerns

<!-- clozeblock-start oid="ObsyXTJ5npNsVioHjAksLLnS" -->
You can use several effects, this lets us separate ==unrelated logic== into different effects : 

```
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {    
	  document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {    
	  function handleStatusChange(status) {
	      setIsOnline(status.isOnline);
	    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
}
```

<!-- clozeblock-end -->

### Explanation: Why Effects Run on Each Update

<!-- basicblock-start oid="ObseEf5i82NF4KFwPEhdq6xb" -->
**Why Effects run on each update ?**:: 
Because prop can changes while the component is on the screen and that can bring bugs and memory leak or crash.

If you’re used to classes, you might be wondering why the effect cleanup phase happens after every re-render, and not just once during unmounting.

```
  componentDidMount() {
    ChatAPI.subscribeToFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }

  componentWillUnmount() {
    ChatAPI.unsubscribeFromFriendStatus(
      this.props.friend.id,
      this.handleStatusChange
    );
  }
```

**What happens if the `friend` prop changes** while the component is on the screen? Our component would continue displaying the online status of a different friend. This is a bug. We would also cause a memory leak or crash when unmounting since the unsubscribe call would use the wrong friend ID.

With hooks, here is a sequence of subscribe using useEffect that not create bug : 

```
// Mount with { friend: { id: 100 } } props
ChatAPI.subscribeToFriendStatus(100, handleStatusChange);     // Run first effect

// Update with { friend: { id: 200 } } props
ChatAPI.unsubscribeFromFriendStatus(100, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(200, handleStatusChange);     // Run next effect

// Update with { friend: { id: 300 } } props
ChatAPI.unsubscribeFromFriendStatus(200, handleStatusChange); // Clean up previous effect
ChatAPI.subscribeToFriendStatus(300, handleStatusChange);     // Run next effect

// Unmount
ChatAPI.unsubscribeFromFriendStatus(300, handleStatusChange); // Clean up last effect
```
<!-- basicblock-end -->

### Tip: Optimizing Performance 

<!-- basicblock-start oid="ObsoK3LAcVNUimclN1OelFKx" -->
In some cases, cleaning up or applying the effect after every render might create a performance problem. **So how to optimize performance ?**::

You can tell React to _skip_ applying an effect if certain values haven’t changed between re-renders. To do so, pass an array as an optional second argument to `useEffect`:

```
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if count changes
```

This also works for effects that have a cleanup phase.
<!-- basicblock-end -->

<!-- basicblock-start oid="Obsy1Wy9jhch3J089nhFI5nB" -->
**What to be carrefull when using optimization performance of useEffect ?**::
If you use this optimization, make sure the array includes all values from the component scope (such as props and state) that change over time and that are used by the effect. Otherwise, your code will reference stale values from previous renders.
<!-- basicblock-end -->

<!-- basicblock-start oid="ObscfA8RLxleElnCKUWYUh8c" -->
**How to run an effect and cleant it up only once (on mount and unmount) ?**::
You can pass an empty array (`[]`) as a second argument. This tells React that your effect doesn’t depend on _any_ values from props or state, so it never needs to re-run.
<!-- basicblock-end -->
