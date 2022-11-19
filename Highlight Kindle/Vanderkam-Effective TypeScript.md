---
kindle-sync:
  bookId: '33584'
  title: Effective TypeScript
  author: Dan Vanderkam
  highlightsCount: 2
---
# Effective TypeScript
## Metadata
* Author: [[Dan Vanderkam]]

## Highlights
TypeScript is a superset of JavaScript. In other words, all JavaScript programs are already TypeScript programs. TypeScript has some syntax of its own, so TypeScript programs are not, in general, valid JavaScript programs. TypeScript adds a type system that models JavaScript’s runtime behavior and tries to spot code which will throw exceptions at runtime. But you shouldn’t expect it to flag every exception. It is possible for code to pass the type checker but still throw at runtime. While TypeScript’s type system largely models JavaScript behavior, there are some constructs that JavaScript allows but TypeScript chooses to bar, such as calling functions with the wrong number of arguments. This is largely a matter of taste. — location: [497]() ^ref-35080

---
The TypeScript compiler includes several settings which affect core aspects of the language. Configure TypeScript using tsconfig.json rather than command-line options. Turn on noImplicitAny unless you are transitioning a JavaScript project to TypeScript. Use strictNullChecks to prevent “undefined is not an object”-style runtime errors. Aim to enable strict to get the most thorough checking that TypeScript can offer. — location: [607]() ^ref-55606

---
