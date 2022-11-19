---
deck: Mastermind my memory::ReactJS
---

# Portals

<!-- basicblock-start oid="ObsU0l8YdciBQJv4BjW1mHn9" -->
**What is Portals ?**::
Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component.

```
ReactDOM.createPortal(child, container)
```

The first argument (`child`) is any renderable React child, such as an element, string, or fragment. The second argument (`container`) is a DOM element.

A typical use case for portals is when a parent component has an `overflow: hidden` or `z-index` style, but you need the child to visually “break out” of its container. For example, dialogs, hovercards, and tooltips.
<!-- basicblock-end -->