- Default display property for span is inline.
- If you want part of text always separated by line then don't forget to use br tag.
- You can make the div in column by making them float left right with width 45%.
- Do width 100% to fit the div for mobile screen.
- To fit the text set text-align to justify.
- You can use text properties on div to apply on all the content inside it.
### Viewport height

In CSS, `100vh` refers to 100% of the viewport height. The `vh` unit stands for "viewport height," where 1vh is equal to 1% of the height of the viewport (the visible part of a web page in the browser window). Therefore, `100vh` means the element will take up 100% of the viewport height, making it as tall as the browser window. This unit is commonly used for creating full-height sections on web pages.

- Use viewport height to set height to the whole page.
- Often using gap in flexbox set it to 2rem.
- To use light gray transparency color use #f2f2f2
- Before adding spacing in list items make sure to make padding and margin of list set to 0.Then you can use margin-bottom to give spacing.
- When flex direction is column try to set height to 100% instead of 100vh.
To center a div use following style
```css
body{
      margin:0;
      padding:0;
      height:100vh;
      display:flex;
      justify-content: center;
      align-items:center;
    }
```

- To remove bullet points use `list-style:none`