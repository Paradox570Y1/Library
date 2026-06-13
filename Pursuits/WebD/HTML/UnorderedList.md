**Attributes:**
- type (decrypted)
	- disc (default)
	- square
	- circle
	- triangle(only works for WebTV interface)
- `list-style-type` (use this inside style)
```html
<style>
list-style-type: disc;
list-style-type: circle;
list-style-type: square;
list-style-type: decimal;
list-style-type: georgian;
list-style-type: trad-chinese-informal;
list-style-type: kannada;
list-style-type: devanagari;
list-style-type: "👍";
/* <string> value */
list-style-type: "-";
<style>

/* Example */
<ul style='list-style-type: "->";line-height: 120%; ' >
    <li>a</li>
    <li>b</li>
    <li>c</li>
</ul>
/* to use double quotes inside style use single quotes to wrap all attributes */
```


- `line-height`  (also used in styles)
	-  Using it we can define the spacing between lines in a list