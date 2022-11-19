---
deck: Mastermind my memory::ReactJS
---

# Render-tree Construction, Layout, and Paint
## Creation of Render Tree
![[Pasted image 20220930003157 1.png]] **With the render tree in place, we can proceed to the =="layout"== stage.** 
^1664509550290

After we've calculated which nodes should be visible and their computed styles, we have to calculated their exact position and size within the viewport of the device---that's the =="layout"== stage, also known as =="reflow."==. The output of the layout process is a ==box model==
^1664510164429

==box model== precisely captures the exact position and size of each element within the viewport: all of the relative measurements are converted to absolute ==pixels== on the screen. 
^1664510164439

When we have the ==box model==, we can convert each node in the render tree to actual pixels on the screen. This step is often referred to as =="painting"== .
^1664510164447