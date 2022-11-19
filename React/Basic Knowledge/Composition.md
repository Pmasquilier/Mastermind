---
deck: Mastermind my memory::ReactJS
---

# Composition vs Inheritance

<!-- basicblock-start oid="ObsU5FZyx7dLRZTyJYHt7zUx" -->
****What can we use to use composition instead of inheritance that is not recommanded in React ?::

React has a powerful composition model, and we recommend using composition instead of inheritance to reuse code between components.

Some components don’t know their children ahead of time. This is especially common for components like `Sidebar` or `Dialog` that represent generic “boxes”.

We recommend that such components use the special **`children`** prop to pass children elements directly into their output:

```
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}    
    </div>
  );
}
```

This lets other components pass arbitrary children to them by nesting the JSX:

```
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">        Welcome      </h1>      
      <p className="Dialog-message">        
      Thank you for visiting our spacecraft!      
      </p>    
    </FancyBorder>
  );
}
```

<!-- basicblock-end -->