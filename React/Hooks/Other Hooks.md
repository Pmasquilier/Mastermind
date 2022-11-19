---
deck: Mastermind my memory::ReactJS
---
# `useContext`

<!-- basicblock-start oid="ObsGCDO6lFSPYI3Ad5g3szmh" -->
**What is context and when to use it ?** ::

[[Context]] is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language. 

Accepts a context object (the value returned from `React.createContext`) and returns the current context value for that context. The current context value is determined by the `value` prop of the nearest `<MyContext.Provider>` above the calling component in the tree.

When the nearest `<MyContext.Provider>` above the component updates, this Hook will trigger a rerender with the latest context `value` passed to that `MyContext` provider.

**Putting it together with Context.Provider**

```
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  const theme = useContext(ThemeContext);  
  return (    
	  <button style={{ background: theme.background, color: theme.foreground }}>      
		  I am styled by theme context!    
	  </button>  
	);
}
```
<!-- basicblock-end -->



