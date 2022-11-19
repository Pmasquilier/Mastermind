---
kindle-sync:
  bookId: '48367'
  title: Just React Learn React the React Way (Hari Narayn) (z-lib.org)
  author: Unknown
  highlightsCount: 28
---
# Just React Learn React the React Way
## Metadata
* Author: [[Unknown]]

## Highlights
Next, the browser determines what styles need to apply to elements and creates another tree, called the CSS Object Model (CSSOM) tree. Then it combines the DOM and CSSOM trees to produce the render tree. The difference between a DOM tree and a render tree is that the render tree knows about the styles. — location: [429]() ^ref-33106

---
React uses a concept called the Virtual DOM to work a bit differently. It creates two copies of the DOM in memory. When we change the DOM, it changes one copy of the DOM. Then, it compares that copy with the other copy to determine what has changed. This process is called diffing. React then batches these changes and applies them to the real DOM in one shot. — location: [472]() ^ref-35498

---
A JavaScript library is a library of pre-written JavaScript code that allows for easier development of JavaScript-based applications. React is a JavaScript library, whereas Angular is a JavaScript framework. A framework comes with a structure and more features. — location: [536]() ^ref-60079

---
There are two kinds of applications: single-page and multi-page. In a single-page application (SPA), the browser gets only one page from the server. — location: [547]() ^ref-27292

---
A single-page application interacts with the user by dynamically rewriting the current web page with new data from the web server, instead of the default method of a web browser loading entire new pages. — location: [552]() ^ref-49919

---
One is to build SPAs, where React controls the entire UI — location: [565]() ^ref-26252

---
Do only SPAs use React? Not necessarily. You can even use React in MPAs. Basically, you can use React for two purposes. One is to build SPAs, where React controls the entire UI after the browser loaded the single page from the server. The other purpose is to control parts or widgets of a page in MPAs. — location: [564]() ^ref-29613

---
You use ReactDOM as the middleman that renders your React elements in the browser. The react-dom package helps you put your root HTML file into the browser using root.render(). First, we use the createRoot() method of ReactDOM to access the root node, and we call render() — location: [1143]() ^ref-39121

---
We don’t use ReactDOM in mobile devices. We use React-Native for mobile development with React. React-Native acts as the middleman there. We use ReactDOM only in web apps. — location: [1146]() ^ref-7956

---
We use the webpack package to bundle all our code. The webpack-dev-server package allows us to execute the application in a local server during development. — location: [1183]() ^ref-19060

---
The webpack-cli package provides a set of commands we can use while setting up the project. The html-webpack-plugin is a Webpack plugin that is used to inject the bundled JS file into the HTML file. — location: [1185]() ^ref-37616

---
Babel is a JavaScript compiler. Babel converts ES6 and above code into a version of JS that runs in any browser, as well as JSX code. — location: [1214]() ^ref-27306

---
We call Babel a transpiler. Transpiling is a special type of compiling where source code written in one language is transformed into another language that has a similar level of abstraction. — location: [1218]() ^ref-41598

---
babel/core is the core Babel library, which does the transpiling. The babel/preset-env package is a preset that allows you to use modern JS without worrying about browser compatibility issues. The babel/preset-react package exactly does the same thing but for JSX code. And the babel-loader is a package that tells Webpack how to interpret and translate files before it does the bundling. The transformation occurs on a per-file basis before Webpack constructs the dependency graph. — location: [1221]() ^ref-1531

---
It’s known as JavaScript XML (JSX). JSX is used by React to describe how the UI looks like. We can write the component code in plain JS, including the creation of HTML elements. JSX makes it easier by providing a visual feel like HTML. — location: [1353]() ^ref-38524

---
a form submit event will invoke browser refresh, which is a native behavior of the submit button. We cancel this default behavior by adding event.preventDefault( ). — location: [1497]() ^ref-846

---
The props are read-only, while the state can be updated. — location: [1686]() ^ref-10273

---
Using state, you can store data within a component, — location: [1694]() ^ref-21454

---
and you can make the component interactive by updating the state. When you want to communicate with another component, props come into play. If you want to access the state of a component outside of that component, you need to use props to pass that state. Then, other components can access it. But if the component wants to change that state, then it needs to contact the component where the state is defined. Again, it can use a prop to do that communication. The props are read-only, while the state can be updated. The props are used to pass data through the component tree from top to bottom. We can pass state as props, just like setUpdatedSeats in our example. — location: [1695]() ^ref-36955

---
Prettier, ESLint, ES7 React/Redux/GraphQL/ — location: [1792]() ^ref-42887

---
React-Native snippets, VS Code React Refactor, and JS JSX Snippets. Another useful extension is JavaScript Booster. — location: [1793]() ^ref-16943

---
Note Fluent UI is a collection of user experience (UX) frameworks designed by Microsoft using react. You can access the full list here: https://developer. microsoft.com/en- us/fluentui#/. There is a section for react elements and styles. You can get into this by selecting Controls/Styles under “react” from the Fluent UI home page. — location: [1995]() ^ref-55230

---
const EnrolList = React.lazy(() => import("./EnrolList.js")); Compared with the previous code we had, I added a React.lazy() function to import the list component. This lets you load the list component lazily. In addition, I added React and Suspense to import from the React library. This is required to use the Lazy function and the Suspense component. — location: [2484]() ^ref-53863

---
I wrapped the EnrolList inside a Suspense component. This is required by the Lazy function to wrap the lazy component. — location: [2493]() ^ref-2863

---
By props drilling, we mean sending props from a higher-level component to a lower-level component. — location: [2515]() ^ref-37220

---
If your application is complex, imagine what it would be like. Managing the application through props drilling will be extremely difficult due to the large component tree. By using a concept called React Context, we can avoid this issue with props drilling. — location: [2524]() ^ref-20512

---
Fragments in React allow us to group items without having to wrap them inside another element, such as a div. — location: [2715]() ^ref-24614

---
Context is an API built into React that provides an alternate and more convenient method of passing data between components. Using Context, we can create a kind of global state that can be used by all components. To implement Context, we need three steps. Create a context, provide it from a component, and then consume it from any other component that requires it. — location: [2977]() ^ref-20450

---
