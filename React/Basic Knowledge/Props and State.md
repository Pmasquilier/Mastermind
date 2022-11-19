---
deck: Mastermind my memory::ReactJS
---

# Props and State
## React Props 
### Definition

==React Props== are like function arguments in JavaScript _and_ attributes in HTML. To send props into a component, use the same syntax as HTML attributes. ![[Pasted image 20220930012706 1.png]]
^1664512382812

## Properties
Props are ==Read-Only== : Whether you declare a component as a function or a class, it must never modify its own props. Consider this sum function: ![[Pasted image 20220930013124 1.png]]. Such functions are called ==pure== because they do not attempt to change their inputs, and always return the same result for the same inputs. In contrast, this function is ==impure== because it changes its own input: ![[Pasted image 20220930013224 1.png]]. React is pretty flexible but it has a single strict rule: All React components must act like pure functions with respect to their props.
^1664512480320

## React State

Using ==state==, you can store data within a component, and you can make the component interactive by updating the ==state==. When you want to communicate with another component, ==props== come into play. If you want to access the ==state== of a component outside of that component, you need to use ==props== to pass that ==state==. Then, other components can access it. But if the component wants to change that ==state==, then it needs to contact the component where the ==state== is defined. Again, it can use a ==prop== to do that communication. The ==props== are read-only, while the ==state== can be updated. 
^1664512876648

### Do Not Modify State Directly

<!-- clozeblock-start oid="ObskzlKRGZM2fD1cVjCp7WcW" -->

For example, this will not re-render a component:

```
// Wrong
this.state.comment = 'Hello';
```

Instead, use ==setState()==

```
// Correct
this.setState({comment: 'Hello'});
```

The only place where you can assign `this.state` is the ==constructor==.

<!-- clozeblock-end -->

### State Updates May Be Asynchronous

<!-- basicblock-start oid="ObsxDiUnBPSkm8X93fIxHUV3" -->
 `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

For example, this code may fail to update the counter:

```
// Wrong
this.setState({
  counter: this.state.counter + this.props.increment,
});
```

To fix it, use a second form of `setState()` that accepts a function rather than an object. That function will receive the previous state as the first argument, and the props at the time the update is applied as the second argument::

```
// Correct
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
<!-- basicblock-end -->

