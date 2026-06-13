![[Pasted image 20240625111836.png]]

![[Pasted image 20240625111957.png]]
- There are over 100 tags in html and above are 105 listed tags.
___
> There are specific attributes reserved for certain elements and there are [Global attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes) which can be used on any HTML elements.([[List of Global attributes]])

- [meta](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta)
	- To redirect to other page after 3s of loading the website
```html
<meta http-equiv="refresh" content="3;url=https://example.com">
```
- [Heading](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)
    - Avoid using multiple < h1> elements on one page in case they are nested.
    - Do not skip one or more heading levels but linearly change the heading levels.
- [Paragraph](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p)
	- ![[Pasted image 20240625170229.png|400]]
	- 

- [[Void Element]]
	- Ex [Horizontal Rule Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/hr) , image tag, br tag.
	- [[hr Tag Attributes|Attributes]] of </hr > Tag.
- [Lists](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li)
     - The **`<li>`** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element is used to represent an item in a list. It must be contained in a parent element: an ordered list ([`<ol>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ol)), unordered list ([`<ul>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)), or a menu([`<menu>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/menu))
     - Though not a conforming usage, the obsolete [`<dir>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dir) can also be a parent.
     - Popular attribute used in <.li>include [type](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li#attributes)(in < ul>, < ol>) , [value](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li#attributes)(in < li>) ,  [start](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ol) (in < ol>)
     - Use [list-style-type](https://developer.mozilla.org/en-US/docs/Web/CSS/list-style-type) now days.
     - [[OrderedList]]
     - [[UnorderedList]]
     - [[Nested List]]
     - [[Definition List]]
- [Anchor Tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)
	- The **`<a>`** [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) element (or _anchor_ element), with [its `href` attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#href), creates a hyperlink to web pages, files, email addresses, locations in the same page, or anything else a URL can address.
	- Use [draggable](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes) attribute to prevent text, image to get dragged with mouse cursor.
	- Use[ title](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes) attribute to give alt info about the link on Hovering.
	- [[Make an Clickable|Learn]] how to make your link a Clickable.
	- [target](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#attributes) attribute in anchor tab.
	- We can provide video and audio link in href and it will preview the content and provide you options to download it.
	- use [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) to embed another HTML page in current HTML page .
	- [[AnchorTag Attributes]]
	- [[iframe]]
		![[Pasted image 20241109184407.png]]
		After clicking the link current window opens inside the iframe![[Pasted image 20241109184429.png]]
	- Types of Link: 
    	1. [[absolute]] 
    	2. [[relative]]
    ![[Pasted image 20240717092842.png|500]]
    
- [Image Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img)
     - It is a [[Void Element]].
     - For testing there is a website you can use to get random images https://picsum.photos/ you can also customize width and height by adding https://picsum.photos/200/300
     - Use [alt](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attributes) attribute to show alternative text also if we implement screen readers for visually impaired then it will read the alternate text about the image.
     - If you only mention only one parameter (either width or height) then other parameter automatically changes.
     - Using [[map]] for zooming the image.
     - [[align]] attribute in image tag.
     - [[attribute]]
 >href, src, alt, title and their roles.    [Link](obsidian://open?vault=Lessons&file=WebD%2FHTML%2FAttributes%2FRoles)

>**NOTE**
>In windows 1 css pixel is equal to 1 by 1 machine pixel.
>In mac retina displays 1 css pixel is equal to 2 by 2 machine pixel.


- [Video](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)
  [[type attribute in video]]
  **Avoid using absolute path for local images and video**
  It may not work in a web browser. Browsers typically can't access files directly from your local drive when using absolute paths like this, especially if the file isn't hosted on a server.

  **Browsers don't support mkv video files.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <video controls width="400px"  loop>
        <source src="../song.mp4"  type="video/mp4"/>
        Download the mp4.
    </video>
</body>
</html>
```
The statement "Download the mp4."** inside the `<video>` tag is not visible because it is placed as fallback content within the `<video>` element. This content is only shown when the video cannot be played (e.g., the browser doesn't support the video format, or the video file can't be found).
However, in modern browsers that support the MP4 format (as specified in the `type="video/mp4"`), the video will play, and the fallback text will not be displayed.
![[Pasted image 20250629155510.png]]

- [Audio](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)
- [Table Tag](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables)
	- [[Table structure]]
	- [[Table Attributes]]
	- By default cellpadding is 2px
- Head Tag
	- Head tag is the first tag rendered in your html file.
	- Avoid using many 3rd party data elements as it can make the head tag heavy, due to which your website will load slowly. Even try to apply css after head tag finishes. Link JS in body.

- Meta Tag
	- In it we often use [[UTF-8]] (**Unicode Transformation Format - 8-bit**.)