---
deck: Mastermind my memory::ReactJS
---

## Fragments

<!-- clozeblock-start oid="ObsPKchFTzHQIaSC8r1BzhkK" -->

A common pattern in React is for a component to return multiple elements. Fragments let you group a list of children without adding extra nodes to the DOM. Fragments declared with the explicit =={React.Fragment}== syntax may have keys. `key` is the only attribute that can be passed to Fragment. 
 
```
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // Without the `key`, React will fire a key warning
        <React.Fragment key={item.id}>
          <dt>{item.term}</dt>
          <dd>{item.description}</dd>
        </React.Fragment>
      ))}
    </dl>
  );
}
```

<!-- clozeblock-end -->