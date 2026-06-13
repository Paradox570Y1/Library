1. **src**: Specifies the path to the image file.
    - Example: 
```css
<img src="path/to/image.jpg">
```

2. **alt**: Provides alternative text for the image if it cannot be displayed.
    - Example: 
```css
<img src="path/to/image.jpg" alt="A beautiful landscape">
```

3. **width** and **height**: Set the dimensions of the image.
    - Example: 
```css
<img src="path/to/image.jpg" width="300" height="200">
```

4. **title**: Provides additional information about the image, often displayed as a tooltip when the mouse hovers over the image.
    - Example: 
```css
<img src="path/to/image.jpg" title="A beautiful landscape">
```

5. **loading**: Indicates how the browser should load the image. The values can be `lazy` or `eager`.
    - Example: 
```css
<img src="path/to/image.jpg" loading="lazy">
```

```txt
The loading attribute in the <img> tag has a default value of eager. This means that, by default, images are loaded immediately, as soon as the browser finds the <img> tag in the HTML, without waiting for the image to come into the viewport.

Here is how the attribute works:

lazy: Defer loading of the image until it reaches a calculated distance from the viewport, which helps improve performance, especially on pages with many images.
eager: Load the image immediately, regardless of its position on the page (default behavior).
```

6. **srcset**: Defines a set of images to be used based on screen resolution and other factors.
    - Example: 
```css
<img src="small.jpg" srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w" alt="Responsive image">
```

7. **sizes**: Specifies how much space (in viewport width) the image will take up. This works with the `srcset` attribute.
    - Example: 
```css
<img src="small.jpg" srcset="large.jpg 1024w, medium.jpg 640w, small.jpg 320w" sizes="(max-width: 600px) 100vw, 50vw" alt="Responsive image">
```
- For viewports up to 600px wide, the image takes up 100% of the viewport width.
- For viewports wider than 600px, the image takes up 50% of the viewport width.

1. **usemap**: Associates the image with an image map (created with the `<map>` tag) for clickable areas within the image.
    - Example: 
```css
<img src="path/to/image.jpg" usemap="#mapname">
```