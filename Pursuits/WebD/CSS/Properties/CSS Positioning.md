![[Pasted image 20240716094526.png|500]]
- [Demo](https://appbrewery.github.io/css-positioning/)
- HTML default flow is static.
- Relative positioning is relative to default positioning.
	[[Example 1 CSS]]
- Absolute positioning makes position relative to nearest positioned ancestor.
	- If there is no ancestor then it gets positioned to top left corner of webpage.
	- Use z-index to control if the element should be behind other elements or above other elements. By Default all elements have z-index set to 0.
- Fixed Positioning positions the div relative to the top left corner of browser window.
	- Even if we scroll then still the div will remain positioned as before.
	- use sticky for better animation.

- To set child element relative to parent element set parent element to relative then use absolute on child. If their is another child inside child then you can use relative on it to set it relative to previous child.
	Ex:  [[Building Flag]]


