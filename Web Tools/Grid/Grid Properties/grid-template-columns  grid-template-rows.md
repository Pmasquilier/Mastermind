## grid-template-columns  grid-template-rows

Defines the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line:

-   **`<track-size>`** – can be a length, a percentage, or a fraction of the free space in the grid using the [[fr unit]] unit.
-   **`<line-name>`** – an arbitrary name of your choosing

### Exemple

```css
.container {
  grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
  grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```
![[Pasted image 20221020133906.png]]

### Repeat notation

If your definition contains repeating parts, you can use the 'repeat' notation to streamline things:

```css
.container {
  grid-template-columns: repeat(3, 20px [col-start]);
}
```

Which is equivalent to this:

```css
.container {
  grid-template-columns: 20px [col-start] 20px [col-start] 20px [col-start];
}
```

If multiple lines share the same name, they can be referenced by their line name and count.

```css
.item {
  grid-column-start: col-start 2;
}
```
