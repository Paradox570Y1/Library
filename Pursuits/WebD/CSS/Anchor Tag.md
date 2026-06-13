![[Pasted image 20240806102713.png|300]]
- To link external page use link in href
- To link section of page use its id in href
- To send an Email use `mailto:mail@gmail.com`
- To make a Call use `tel:+911234567890`
- On clicking pop up comes
![[Pasted image 20240806103326.png|300]]
![[Pasted image 20240806103349.png|200]]
- To make an image download on clicking on it
```css
<a href="./beautiful.jpg" download>
    <img src="./beautiful.jpg" alt="flower in water">
</a>
/* To assign different name to photo while download*/
<a href="./beautiful.jpg" download="flower">
    <img src="./beautiful.jpg" alt="flower in water">
</a>
```
On clicking following window will appear.
![[Pasted image 20240806103855.png|300]]
- New Tab & Security
Using the `rel="noopener"` attribute in an anchor (`<a>`) tag is important for security reasons. This attribute prevents the newly opened page from being able to access the `window.opener` property, which can be exploited to manipulate the original page.

```css
<a href="https://example.com" target="_blank" rel="noopener">Open Example</a>
```
In this example:

- `href="https://example.com"` specifies the URL of the page to link to.
- `target="_blank"` opens the link in a new tab or window.
- `rel="noopener"` enhances security by preventing the new page from accessing the `window.opener` property of the original page.

This is especially important when opening links to third-party sites, as it helps prevent potential security vulnerabilities such as phishing attacks or unwanted manipulations.


- Using iframe to open link in parent or self
```html
/*index.html (running)*/
<p>I am index file</p>
<iframe src="./children.html" ></iframe>

/* children.html */
<p>I am a Children</p>
<iframe src="./grand.html"></iframe>

/* grand.html */
<p>I am a Grand Children</p>
<a href="https://example.com"
   target="_parent"
>Example</a>
```
- target set to `_parent`.
![[Pasted image 20240806130831.png]]

- target set to `_blank`
![[Pasted image 20240806130926.png|300]]


- To count how many times a page is visited
	we use ping
```html
<body>
    <a href="https://example.com"
       target="_blank"
       ping="https://example.com/track"
    >
    Example
    </a>
</body>
```
![[Pasted image 20240806131649.png]]

You can count the ping and then use it to change elements after every visit.

#### Styling Anchor Tag
- Four states of anchor tag:
	- link
	- hover
	- active
	- visited
Use pseudo classes for different parts of link.
```css
a{
            font-size:30px;
        }
        a:link{
            color:green;
        }
        a:hover{
            color:orangered;
        }
        a:active{
            color:black;
        }
        a:visited{
            color:purple;
        }
```
