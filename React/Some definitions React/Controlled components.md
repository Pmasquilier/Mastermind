---
deck: Mastermind my memory::ReactJS
---

## Controlled Component

<!-- basicblock-start oid="ObsBzSqIXErhNSI3GQ9297RW" -->
****What is the name of a input form element whose value is controlled by React ?::

Its called a **“controlled component”**.

In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, and only updated with setState()

We can combine the two by making the React state be the “single source of truth”. Then the React component that renders a form also controls what happens in that form on subsequent user input. 
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsepzOVYSfSfYEhjVbxBJIM" -->

**How to handle multiple controlled input elements ?**::

When you need to handle multiple controlled `input` elements, you can add a `name` attribute to each element and let the handler function choose what to do based on the value of `event.target.name` and we can use the compued property name syntax to update the state key corresponding to the given input name:

```
this.setState({
  [name]: value});
```

<!-- basicblock-end -->

## Alternatives to Controlled Components

[[Uncontrolled Component]]