## grid-column  grid-row

Shorthand for [[grid-column-start  grid-column-end grid-row-start  grid-row-end]]

### Example:

```css
.item-c {
  grid-column: 3 / span 2;
  grid-row: third-line / 4;
}
```

![Example of grid-column/grid-row](https://css-tricks.com/wp-content/uploads/2018/11/grid-column-row.svg)
If no end line value is declared, the item will span 1 track by default.