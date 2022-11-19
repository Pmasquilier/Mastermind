---
deck: Mastermind my memory::ReactJS
---

# Context
<!-- basicblock-start oid="Obs06JhmW80kFXQdsc7lD1Y1" -->
**What is Context ?**::
Context provides a way to pass data through the component tree without having to pass props down manually at every level.

Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language.
<!-- basicblock-end -->

<!-- basicblock-start oid="ObssA8pdT7dX2L79t5sXWNco" -->
**What are the 3 principales steps to create and consume context  ?**::
```
const MyContext = React.createContext(defaultValue); 
// Create the context object on the parent

<MyContext.Provider value={/* some value */}> 
// The Provider component accepts a `value` prop to be passed to consuming components that are descendants of this Provider.

<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
// Consume the context. The function receives the current context value and returns a React node. 

```
<!-- basicblock-end -->

**If you only want to avoid passing some props [[Composition]] is often a simpler solution than context.**

## API

### [](https://reactjs.org/docs/context.html#reactcreatecontext)`React.createContext`

```
const MyContext = React.createContext(defaultValue);
```

Creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching `Provider` above it in the tree.

The `defaultValue` argument is **only** used when a component does not have a matching Provider above it in the tree. This default value can be helpful for testing components in isolation without wrapping them.

### `Context.Provider`

```
<MyContext.Provider value={/* some value */}>
```

Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.

The Provider component accepts a `value` prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers.

All consumers that are descendants of a Provider will re-render whenever the Provider’s `value` prop changes.


### `Class.contextType`

```
class MyClass extends React.Component {
  componentDidMount() {
    let value = this.context;
    /* perform a side-effect at mount using the value of MyContext */
  }
}
MyClass.contextType = MyContext;
```

The `contextType` property on a class can be assigned a Context object created by React.createContext. Using this property lets you consume the nearest current value of that Context type using `this.context`.

You can only subscribe to a single context using this API. If you need to read more than one see Consuming Multiple Contexts above. 

### `Context.Consumer`

```
<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
```

A React component that subscribes to context changes. Using this component lets you subscribe to a context within a function component.

Requires a function as a child. The function receives the current context value and returns a React node. The `value` argument passed to the function will be equal to the `value` prop of the closest Provider for this context above in the tree. If there is no Provider for this context above, the `value` argument will be equal to the `defaultValue` that was passed to `createContext()`.

### Updating Context from a Nested Component

It is often necessary to update the context from a component that is nested somewhere deeply in the component tree. In this case you can pass a function down through the context to allow consumers to update the context:

```
export const ThemeContext = React.createContext({
  theme: themes.dark,  toggleTheme: () => {},});
```

### Consuming Multiple Contexts

To keep context re-rendering fast, React needs to make each context consumer a separate node in the tree.

```
// Theme context, default to light theme
const ThemeContext = React.createContext('light');

// Signed-in user context
const UserContext = React.createContext({
  name: 'Guest',
});

class App extends React.Component {
  render() {
    const {signedInUser, theme} = this.props;

    // App component that provides initial context values
    return (
      <ThemeContext.Provider value={theme}>        
	      <UserContext.Provider value={signedInUser}>          
		      <Layout />
		  </UserContext.Provider>      
        </ThemeContext.Provider>    
    );
  }
}

function Layout() {
  return (
    <div>
      <Sidebar />
      <Content />
    </div>
  );
}

// A component may consume multiple contexts
function Content() {
  return (
    <ThemeContext.Consumer>      
	    {theme => (        
		    <UserContext.Consumer>          
			    {user => (            
				    <ProfilePage user={user} theme={theme} />          
			    )}        
		    </UserContext.Consumer>      
	    )}    
    </ThemeContext.Consumer>  );
}
```