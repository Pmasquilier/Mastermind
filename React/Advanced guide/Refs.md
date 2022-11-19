---
deck: Mastermind my memory::ReactJS
---

# Refs and the DOM

<!-- basicblock-start oid="Obs43JCyLJYRMR2z6tXEG2Zs" -->
**What is Ref and when to use it ?**::
Refs provide a way to access DOM nodes or React elements created in the render method.

### When to Use Refs

There are a few good use cases for refs:

-   Managing focus, text selection, or media playback.
-   Triggering imperative animations.
-   Integrating with third-party DOM libraries.
- <!-- basicblock-end -->

### Creating Refs

Refs are created using `React.createRef()` and attached to React elements via the `ref` attribute. Refs are commonly assigned to an instance property when a component is constructed so they can be referenced throughout the component.

```
class MyComponent extends React.Component {

  constructor(props) {
    super(props);
    this.myRef = React.createRef();  
  }
  
  render() {
    return <div ref={this.myRef} />;  
  }
}
```

### Accessing Refs

When a ref is passed to an element in `render`, a reference to the node becomes accessible at the `current` attribute of the ref.

```
const node = this.myRef.current;
```

The value of the ref differs depending on the type of the node:

-   When the `ref` attribute is used on an HTML element, the `ref` created in the constructor with `React.createRef()` receives the underlying DOM element as its `current` property.
-   When the `ref` attribute is used on a custom class component, the `ref` object receives the mounted instance of the component as its `current`.
-   **You may not use the `ref` attribute on function components** because they don’t have instances.

#### Refs and Function Components

By default, **you may not use the `ref` attribute on function components** because they don’t have instances:

If you want to allow people to take a `ref` to your function component, you can use forwardRef