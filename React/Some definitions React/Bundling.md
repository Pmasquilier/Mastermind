---
deck: Mastermind my memory::ReactJS
---

<!-- basicblock-start oid="ObsFihcU87LBVbONmfnWaqxd" -->
What is bundling ?::
Bundling is the process of following imported files and merging them into a single file: a “bundle”. This bundle can then be included on a webpage to load an entire app at once.

**App:**

```
// app.js
import { add } from './math.js';

console.log(add(16, 26)); // 42
```

```
// math.js
export function add(a, b) {
  return a + b;
}
```

**Bundle:**

```
function add(a, b) {
  return a + b;
}

console.log(add(16, 26)); // 42
```
<!-- basicblock-end -->