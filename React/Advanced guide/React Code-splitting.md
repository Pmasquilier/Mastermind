
---
deck: Mastermind my memory::ReactJS
---

# Code-Splitting

## [[Bundling]]

Most React apps will have their files “bundled” using tools like Webpack, Rollup or Browserify. 
If you’re using Create React App, Next.js, Gatsby, or a similar tool, you will have a Webpack setup out of the box to bundle your app.

## [[Code Splitting]]

Bundling is great, but as your app grows, your bundle will grow too. Especially if you are including large third-party libraries. You need to keep an eye on the code you are including in your bundle so that you don’t accidentally make it so large that your app takes a long time to load.

To avoid winding up with a large bundle, it’s good to get ahead of the problem and start “splitting” your bundle. See [[Code Splitting]].

# Two ways to introduce code-splitting into a react app 
<!-- basicblock-start oid="ObsK3VpIRY6iJK5kZEPm2vNR" -->
**Give two ways to introduce code-splitting into a react app**::

## `import()`

The best way to introduce code-splitting into your app is through the dynamic `import()` syntax.

**Before:**

```
import { add } from './math';

console.log(add(16, 26));
```

**After:**

```
import("./math").then(math => {
  console.log(math.add(16, 26));
});
```

## `React.lazy`

The `React.lazy` function lets you render a dynamic import as a regular component.

**Before:**

```
import OtherComponent from './OtherComponent';
```

**After:**

```
const OtherComponent = React.lazy(() => import('./OtherComponent'));
```

This will automatically load the bundle containing the `OtherComponent` when this component is first rendered.

<!-- basicblock-end -->
<!-- basicblock-start oid="ObsDtGyGNBGOTjqKxEqvfrF7" -->
**How to show some fallback content (such as a loading indicator) while we’re waiting for a lazy component to load ?**::

The lazy component should then be rendered inside a `Suspense` component, which allows us to show some fallback content (such as a loading indicator) while we’re waiting for the lazy component to load.

```
import React, { Suspense } from 'react';

const OtherComponent = React.lazy(() => import('./OtherComponent'));

function MyComponent() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <OtherComponent />
      </Suspense>
    </div>
  );
}
```

The `fallback` prop accepts any React elements that you want to render while waiting for the component to load. 
<!-- basicblock-end -->

### [[Error boundaries]]

If the other module fails to load (for example, due to network failure), it will trigger an error. You can handle these errors to show a nice user experience and manage recovery with Error Boundaries. Once you’ve created your Error Boundary, you can use it anywhere above your lazy components to display an error state when there’s a network error.

```
import React, { Suspense } from 'react';
import MyErrorBoundary from './MyErrorBoundary';

const OtherComponent = React.lazy(() => import('./OtherComponent'));
const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

const MyComponent = () => (
  <div>
    <MyErrorBoundary>
      <Suspense fallback={<div>Loading...</div>}>
        <section>
          <OtherComponent />
          <AnotherComponent />
        </section>
      </Suspense>
    </MyErrorBoundary>
  </div>
);
```

## Route-based code splitting

A good place to start with code-splitting to know where to introduce it in your app is to use route. 

Here’s an example of how to setup route-based code splitting into your app using libraries like [React Router](https://reactrouter.com/) with `React.lazy`.

```
import React, { Suspense, lazy } from 'react';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';

const Home = lazy(() => import('./routes/Home'));
const About = lazy(() => import('./routes/About'));

const App = () => (
  <Router>
    <Suspense fallback={<div>Loading...</div>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  </Router>
);
```

## Named Exports

`React.lazy` currently only supports default exports. If the module you want to import uses named exports, you can create an intermediate module that reexports it as the default. This ensures that tree shaking keeps working and that you don’t pull in unused components.

```
// ManyComponents.js
export const MyComponent = /* ... */;
export const MyUnusedComponent = /* ... */;
```

```
// MyComponent.js
export { MyComponent as default } from "./ManyComponents.js";
```

```
// MyApp.js
import React, { lazy } from 'react';
const MyComponent = lazy(() => import("./MyComponent.js"));
```