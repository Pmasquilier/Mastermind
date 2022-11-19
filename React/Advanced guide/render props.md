---
deck: Mastermind my memory::ReactJS
---
# Render Props
<!-- basicblock-start oid="Obs4hWuZgPSrZHcuo3D0rkkb" -->
**What is render props ?**::
The term "render props" refers to a technique for sharing code between React components using a prop whose value is a function.

A component with a render prop takes a function that returns a React element and calls it instead of implementing its own render logic.

```
<DataProvider render={data => (
  <h1>Hello {data.target}</h1>
)}/>
```
<!-- basicblock-end -->

