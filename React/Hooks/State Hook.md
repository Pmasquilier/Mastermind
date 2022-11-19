---
deck: Mastermind my memory::ReactJS
---

# useState

```
  const [fruit, setFruit] = useState('banana');
```

This JavaScript syntax is called **array destructuring**.

**What does calling `useState` do?** It declares a “state variable” and is a new way to use the exact same capabilities that `this.state` provides in a class. 

**What do we pass to `useState` as an argument?** The only argument to the `useState()` Hook is the initial state.

**What does `useState` return?** It returns a pair of values: the current state and a function that updates it.

**why is `useState` not named `createState` instead?** “Create” wouldn’t be quite accurate because the state is only created the first time our component renders. During the next renders, `useState` gives us the current state. Otherwise it wouldn’t be “state” at all!

Unlike the `setState` method found in class components, `useState` does not automatically merge update objects. You can replicate this behavior by combining the function updater form with object spread syntax:

```
const [state, setState] = useState({});
setState(prevState => {
  // Object.assign would also work
  return {...prevState, ...updatedValues};
});
```

#### Lazy initial state

The `initialState` argument is the state used during the initial render. In subsequent renders, it is disregarded. If the initial state is the result of an expensive computation, you may provide a function instead, which will be executed only on the initial render:

```
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```
