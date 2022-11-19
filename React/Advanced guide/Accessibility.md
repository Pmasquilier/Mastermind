**Doc incomplete;** [go to React Doc](https://reactjs.org/docs/accessibility.html/)
# Wai-Aria

All `aria-*` HTML attributes are fully supported in JSX. Whereas most DOM properties and attributes in React are camelCased, these attributes should be hyphen-cased (also known as kebab-case, lisp-case, etc).

# Semantic HTML

Using the various HTML elements to reinforce the meaning of information in our websites will often give us accessibility for free.

Sometimes we break HTML semantics when we add `<div>` elements to our JSX to make our React code work. In these cases we should rather use [[Fragments]] to group together multiple elements.

```
function Glossary(props) {
  return (
    <dl>
      {props.items.map(item => (
        // Fragments should also have a `key` prop when mapping collections
        <Fragment key={item.id}>          
		    <dt>{item.term}</dt>
	        <dd>{item.description}</dd>
        </Fragment>     
     ))}
    </dl>
  );
}
```


# Accessible Forms
## Labeling

Every HTML form control, such as `<input>` and `<textarea>`, needs to be labeled accessibly. We need to provide descriptive labels that are also exposed to screen readers.

Although HTML practices can be directly used in React, note that the `for` attribute is written as `htmlFor` in JSX:

## Notifying the user of errors

Error situations need to be understood by all users. The following link shows us how to expose error texts to screen readers as well:
-   [The W3C demonstrates user notifications](https://www.w3.org/WAI/tutorials/forms/notifications/)
-   [WebAIM looks at form validation](https://webaim.org/techniques/formvalidation/)

# Focus Control
Ensure that your web application can be fully operated with the keyboard only:

**Doc incomplete;** [go to React Doc](https://reactjs.org/docs/accessibility.html/)
