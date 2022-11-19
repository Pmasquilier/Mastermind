---
deck: Mastermind my memory::Web Tools::Grid
---

<!-- basicblock-start oid="ObsHVkHYNgdXFF6fe1cR2QU4" -->
**What is fr unit ?**::
The **fr** unit represents a fraction of the leftover space in the grid container. 

Tracks sized with fr units are called **flexible tracks** as they flex in response to leftover space similar to how flex items with a zero base size fill space in a flex container.
<!-- basicblock-end -->

### Exercice
<!-- basicblock-start oid="ObsJIaWcG9k5JKoUzuySBufK" -->

![[Pasted image 20221020162713.png]] How to represents a navigation of 250px on the left followed by a twelve column grid with 10 px between them ?::

```css
.grid {
  display: grid;
  grid-template-columns: 250px repeat(12, 1fr);
  grid-column-gap: 10px;
}
```
<!-- basicblock-end -->