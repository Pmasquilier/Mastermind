
## Introduction 

ES6 adds import and export keywords to JavaScript and finally supports real modularity as a core language feature. ES6 modularity is conceptually the same as Node modularity: each file is its own module, and constants, variables, functions, and classes defined within a file are private to that module unless they are explicitly exported. Values that are exported from one module are available for use in modules that explicitly import them. ES6 modules differ from Node modules in the syntax used for exporting and importing and also in the way that modules are defined in web browsers.

To export a constant, variable, function, or class from an ES6 module, simply add the keyword export before the declaration: 
```
export const PI = Math.PI; 

export function degreesToRadians(d) { 
	return d * PI / 180; 
}
```

## Export keyword 

<!-- basicblock-start oid="ObsO6SCXd7HqGTYHOcin04dt" -->
**What is the difference between "export" and "export default" ? ** ::

It is common to write modules that export only one value (typically a function or class), and in this case, we usually use **export default** instead of export:

```
export default class BitSet { // implementation omitted } 
```

Default exports are slightly easier to import than non-default exports, so when there is only one exported value, using export default makes things easier for the modules that use your exported value. 

It is legal, but somewhat uncommon, for modules to have a set of regular exports and also a default export. **If a module has a default export, it can only have one.**
<!-- basicblock-end -->

You import values that have been exported by other modules with the import keyword. The simplest form of import is used for modules that define a default export: 

```
import BitSet from './bitset.js'; 
```

## Imports

Like function declarations, imports are **“hoisted”** to the top, and all imported values are available for any of the module’s code runs.

By near-universal convention, the imports needed by a module are placed at the start of the module. Interestingly, however, this is not required.

Style guides sometimes recommend that you explicitly import every symbol that your module will use. 

<!-- basicblock-start oid="ObspQV3LTLvz7Jsi315mz6wG" -->
**How to import everything from a module ?** ::

When importing from a module that defines many exports, however, you can easily import everything with an import statement like this: 

```
import * as stats from "./stats.js"; 
```

An import statement like this creates an object and assigns it to a constant named stats. **Each of the non-default exports of the module being imported becomes a property of this stats object.** 
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsnnkPzpqOK5lqUlXz5UMuC" -->
**How to import values from a module that exports multiple values ?** ::

So far, we’ve only considered the case of importing a single value from a module that uses export default. To import values from a module that exports multiple values, we use a slightly different syntax: 

```
import { mean, stddev } from "./stats.js";
```

It is legal, but somewhat uncommon, for a module to use both export and export default. But when a module does that, you can import both the default value and the named values with an import statement like this: 

```
import Histogram, { mean, stddev } from "./histogram-stats.js" 
```
<!-- basicblock-end -->

<!-- basicblock-start oid="ObsfKFUaDBNmX1gmBquPkI2u" -->
**How to do if two modules export two different values using the same name and you want to import both of those values?**::

you will have to rename one or both of the values when you import it. Similarly, if you want to import a value whose name is already in use in your module, you will need to rename the imported value. You can use the **as keyword** with named imports to rename them as you import them: 

```
import { render as renderImage } from "./imageutils.js"; 
import { render as renderUI } from "./ui.js";
```

Here is another way to import both the default and named exports of that module:

```
import { default as Histogram, mean, stddev } from "./histogram-stats.js"; 
```

In this case, the JavaScript keyword default serves as a placeholder and allows us to indicate that we want to import and provide a name for the default export of the module.
<!-- basicblock-end -->

## Script

A ```<script type="module">``` tag marks the starting point of a modular program. None of the modules it imports are expected to be in ```<script>``` tags, however: instead, they are loaded on demand as regular JavaScript files and are executed in strict mode as regular ES6 modules. Using a ```<script type="module">``` tag to define the main entry point for a modular JavaScript program can be as simple as this: 

```
<script type="module">
import "./main.js";
</script>
``` 

<!-- basicblock-start oid="ObsRQtTLsU6wQklCFUMIA1Kj" -->
**What the differences() between ```<script>``` and  ```<script type="module">``` ?** ::

The difference between regular scripts and module scripts has to do with cross-origin loading. A regular ```<script>``` tag will load a file of JavaScript code from any server on the internet, and the internet’s infrastructure of advertising, analytics, and tracking code depends on that fact. But ```<script type="module">``` provides an opportunity to tighten this up, and modules can only be loaded from the same origin as the containing HTML document or when proper CORS headers are in place to securely allow cross-origin loads 

Some programmers like to use the filename extension .mjs to distinguish their modular JavaScript files from their regular, non-modular JavaScript files with the traditional .js extension.
<!-- basicblock-end -->

## Import dynamically

if we want to import a file and use it dynamically
:
```
import * as stats from "./stats.js";

 import("./stats.js").then(stats => { 
	 let average = stats.mean(data); 
}) 
```

It is common for web applications to initially load only enough of their code to render the first page displayed to the user. Then, once the user has some preliminary content to interact with, they can begin to load the often much larger amount of code needed for the rest of the web app. Web browsers make it easy to dynamically load code by using the DOM API to inject a new ```<script>``` tag into the current HTML document, and web apps have been doing this for many years. Although dynamic loading has been possible for a long time, it has not been part of the language itself. 

That changes with the introduction of **import()** in ES2020 (as of early 2020, dynamic import is supported by all browsers that support ES6 modules). You pass a module specifier to import() and it returns a Promise object that represents the asynchronous process of loading and running the specified module. When the dynamic import is complete, the Promise is “fulfilled” and produces an object like the one you would get with the import * as form of the static import statement.

