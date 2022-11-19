---
deck: Mastermind my memory::ReactJS
---

# Uncontrolled Components
<!-- basicblock-start oid="ObsPRHo8OqxCdZ97dGmC6QKp" -->
**What is an uncontrolled components and what react concept to use ?** ::
In most cases, we recommend using [[Controlled components]] to implement forms. In a controlled component, form data is handled by a React component. The alternative is uncontrolled components, where form data is handled by the DOM itself.

To write an uncontrolled component, instead of writing an event handler for every state update, you can use a [[Refs]] to get form values from the DOM.

For example, this code accepts a single name in an uncontrolled component:

```
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.input = React.createRef();  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.input.current.value);    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" ref={this.input} />        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```
<!-- basicblock-end -->