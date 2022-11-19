---
deck: Mastermind my memory::Web Tools::Grid
---
<!-- basicblock-start oid="Obs2kL0azatO56vh8pAArhxt" -->
How to do this in TailwindCSS and CSS:
![[Pasted image 20221020140754.png]]

We want :
	- 2 cols for small size
	- 5 cols for md size and more
	- the children is place on the 3 col for md size and more::

**Tailwind CSS:** 
```css
className=("grid-cols-2 md:grid-cols-5")
```

**CSS:** 
```css
.grid-cols-2 {  
grid-template-columns: repeat(2, minmax(0, 1fr));  
}
```

```css
	@media (min-width: 768px) {  
		.md\:grid-cols-5 {  
			grid-template-columns: repeat(5, minmax(0, 1fr));  
		}  
	}
```
Which is equivalent to this:

```css
	@media (min-width: 768px) {  
		.md\:grid-cols-5 {  
			grid-template-columns:  minmax(0, 1fr) minmax(0, 1fr) minmax(0, 1fr) minmax(0, 1fr)minmax(0, 1fr);  
		}  
	}

```

And for the children : 

**Tailwind CSS:** 
```css
md:col-span-3
```

**CSS:** 
```css
@media (min-width: 768px) {  
	.md\:col-span-3 {  
		grid-column: span 3 / span 3;  
	}  
}
```
<!-- basicblock-end -->