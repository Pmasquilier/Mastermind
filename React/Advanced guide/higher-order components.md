---
deck: Mastermind my memory::ReactJS
---

# Higher-Order Components

<!-- basicblock-start oid="ObssOxdy4c57oJWX1J70v8mT" -->
**What is a higher-order component (HOC)** ? ::
A higher-order component (HOC) is an advanced technique in React for reusing component logic. 

Concretely, **a higher-order component is a function that takes a component and returns a new component.**

```
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

Whereas a component transforms props into UI, a higher-order component transforms a component into another component.

```
// This function takes a component...
function withSubscription(WrappedComponent, selectData) {
  // ...and returns another component...
  return class extends React.Component {
    constructor(props) {
      super(props);
      this.handleChange = this.handleChange.bind(this);
      this.state = {
        data: selectData(DataSource, props)
      };
    }

    componentDidMount() {
      // ... that takes care of the subscription...
      DataSource.addChangeListener(this.handleChange);
    }

    componentWillUnmount() {
      DataSource.removeChangeListener(this.handleChange);
    }

    handleChange() {
      this.setState({
        data: selectData(DataSource, this.props)
      });
    }

    render() {
      // ... and renders the wrapped component with the fresh data!
      // Notice that we pass through any additional props
      return <WrappedComponent data={this.state.data} {...this.props} />;
    }
  };
}
```
<!-- basicblock-end -->


## Convention: Pass Unrelated Props Through to the Wrapped Component

HOCs add features to a component. They shouldn’t drastically alter its contract. It’s expected that the component returned from a HOC has a similar interface to the wrapped component.

### Don’t Use HOCs Inside the render Method

**Don't do this :**
```
render() {
  // A new version of EnhancedComponent is created on every render
  // EnhancedComponent1 !== EnhancedComponent2
  const EnhancedComponent = enhance(MyComponent);
  // That causes the entire subtree to unmount/remount each time!
  return <EnhancedComponent />;
}
```

### Refs Aren’t Passed Through

While the convention for higher-order components is to pass through all props to the wrapped component, this does not work for [[refs]]. That’s because `ref` is not really a prop.

The solution for this problem is to use the `React.forwardRef`