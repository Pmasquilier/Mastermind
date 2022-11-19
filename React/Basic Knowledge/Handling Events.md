---
deck: Mastermind my memory::ReactJS
---

# Handling Events

<!-- basicblock-start oid="ObsEJWg7WnQvQCLC3pkwbFes" -->
There are some syntax differences between handling events with React elements and to handling events on DOM elements. 

For example, the HTML:

```
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

is slightly different in React ::

```
<button onClick={activateLasers}>  Activate Lasers
</button>
```
<!-- basicblock-end -->

## Don't forget to bind

<!-- basicblock-start oid="ObsSxiuzh9B6AXK87FUnfUB9" -->

```
class LoggingButton extends React.Component {
  
  handleClick = () => {    
	  console.log('this is:', this);  
  };  
  
  render() {
    return (
      <button onClick={this.handleClick}>
        Click me
      </button>
    );
  }
}
```
****What is the problem in this code ?
Give 3 solutions to resolve this issue::

In this case, 'this' will be undefined. 3 solutions :

1) Write in the constructor :
```
    this.handleClick = this.handleClick.bind(this);
```

2) Use public class field syntax :
```
handleClick = () => {    
	console.log('this is:', this);  
};
```

3) Use arrow function in the callback :

```
	<button onClick={() => this.handleClick()}>        
	 Click me
	</button>
```

<!-- basicblock-end -->

## Synthetics Events

<!-- clozeblock-start oid="ObsyVY0aMdLnA91anydnvoDr" -->
In order to work as a cross-browser application, React has created a wrapper same as the native browser in order to avoid creating multiple implementations for multiple methods for multiple browsers, creating common names for all events across browsers. We call the handling events in React ==SyntheticEvent==. 
<!-- clozeblock-end -->



