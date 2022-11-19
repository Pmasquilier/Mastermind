---
deck: Mastermind my memory::ReactJS
---

# Lifting State Up

Often, several components need to reflect the same changing data. We recommend lifting the shared state up to their closest common ancestor.

<!-- clozeblock-start oid="Obs5f4urNuie1ZGF42EOKyv8" -->

There should be a single “source of truth” for any data that changes in a React application.

Usually, the state is first added to the component that needs it for rendering. Then, if other components also need it, you can ==lift it up== to their closest common ancestor. 

<!-- clozeblock-end -->

Instead of trying to sync the state between different components, you should rely on the [top-down data flow](https://reactjs.org/docs/state-and-lifecycle.html#the-data-flows-down).