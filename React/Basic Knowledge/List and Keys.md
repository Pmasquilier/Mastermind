---
deck: Mastermind my memory::ReactJS
---

# Syntax

```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}
```

# Keys 

Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity:

```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>    {number}
  </li>
);
```

<!-- clozeblock-start oid="ObsX7wUV9HK60ViJ3OEFpG4f" -->

Generate a unique _id_ for every item and use it as _key_ when rendering the list.

We don’t recommend using indexes for keys if the order of items may change. This can negatively impact performance and may cause issues with component state.

The best way to add id to List in React is to use the library ==nanoid== : https://github.com/ai/nanoid/. 

<!-- clozeblock-end -->

more: https://robinpokorny.com/blog/index-as-a-key-is-an-anti-pattern/


## Extracting Components with Keys
<!-- basicblock-start oid="Obslpxr0ufz2Fs8LcfRB2yUf" -->

****To what elements should be given the Keys ? ::

Keys only make sense in the context of the surrounding array.
A good rule of thumb is that elements inside the `map()` call need keys.

For example, if you extract a `ListItem` component, you should keep the key on the `<ListItem />` elements in the array rather than on the `<li>` element in the `ListItem` itself.

**Example: Incorrect Key Usage**

```
function ListItem(props) {
  const value = props.value;
  return (
    // Wrong! There is no need to specify the key here:    
	    <li key={value.toString()}>      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Wrong! The key should have been specified here:    
    <ListItem value={number} />  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

**Example: Correct Key Usage**

```
function ListItem(props) {
  // Correct! There is no need to specify the key here:  
  return <li>{props.value}</li>;}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.    
    <ListItem key={number.toString()} value={number} />  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

<!-- basicblock-end -->


<!-- basicblock-start oid="Obslbuj6n0wvFDd4E0HXhvqO" -->

****Is the Keys attributed is passed to childrens components ? ::

No, Keys serve as a hint to React but they don’t get passed to your components. If you need the same value in your component, pass it explicitly as a prop with a different name:

```
const content = posts.map((post) =>
  <Post key={post.id}    id={post.id}    title={post.title} />
);
```

With the example above, the `Post` component can read `props.id`, but not `props.key`.

<!-- basicblock-end -->

