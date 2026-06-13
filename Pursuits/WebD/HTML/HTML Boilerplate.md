![[Pasted image 20240701095849.png]]
![[Pasted image 20240703092759.png|500]]
//It tells how your  website will get display when it opens
![[Pasted image 20240701094650.png|200]]
# Why still not HTML6?🤔
- HTML6 is not coming after HTML5 because HTML has shifted from versioned releases to a continuous, evolving specification.
- HTML5 introduced the concept of a "living standard," meaning HTML is now continuously updated and improved. Instead of major version releases.
- The living standard approach focuses on backward compatibility, ensuring that new features integrate smoothly with existing ones without requiring drastic changes to the syntax or structure of HTML.
- **Standardized by WHATWG**: HTML is now maintained as a living standard by WHATWG (Web Hypertext Application Technology Working Group), with a focus on long-term usability and stability rather than major releases.


`<!DOCTYPE html>`
- It is not an tag, but is more like an instruction to browser which tells that "This is a HTML5 Document" so interpret the code according to modern web standards instead of emulating older less strict  rendering for compatibility.

`<html lang="en"></html>`
- This attribute is essential for screen readers.
- screen readers are assistive tools to help visually impaired users by converting text on a webpage into spoken words or Braille.
- It is essential for screen readers bcz language identification  helps screen readers to pronounce words more correctly as well increase Text to Speech Accuracy.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" user-scalable="no"/>
```

- `meta name="viewport"` means this meta tag is named viewport.
- `content="width=device-width, intial-scale=1.0" ` , this tag defines the width of the browser based on device and scales the content accordingly. Otherwise in early times you cannot use website on small screen devices like mobile.
- It only works for mobile.
