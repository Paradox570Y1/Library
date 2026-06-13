![[Pasted image 20240718003939.png]]

> [Grid vs Flexbox](https://appbrewery.github.io/grid-vs-flexbox/)
> [Game practice](https://appbrewery.github.io/gridgarden/)

- Flexbox is good for 1D layout but Grid is better for 2D layout.

```css
.container{
	display:grid;
	grid-template-columns: 1fr 2fr;
	grid-template-rows: 1fr 1fr;
	gap:10px;
}
```
![[Pasted image 20240724192546.png|300]]


# Working

#### `grid-template-rows`
#### `grid-template-columns`

```css
.container{
      height:50vh;
      display:grid;
      grid-template-columns:1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
      /*    For ratio use fr (fractional unit)*/
    }
    .white{
      width:100px;
      background-color: #f0d9b5;

    }
    .black{
      width:100px;
      background-color:#b58863;
    }
```
- For right screen size:
![[Pasted image 20240724193351.png|300]]
- If we increase increase the screen size:
![[Pasted image 20240724193432.png]]
- In above figure we have fixed the width of the items in grid and parent container tries to occupy all the width available as we have not fixed it hence above pattern is observed.
- If we don't assign any width to items then they will stretch.
![[Pasted image 20240724193723.png]]

```css
.container{
      height:50vh;
      width:50vh;
      display:grid;
      grid-template-columns:1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    }
    .white{
      background-color: #f0d9b5;

    }
    .black{
      background-color:#b58863;
    }
```

- If we fix the width of parent and doesn't assign any width to items then :
![[Pasted image 20240724193855.png|300]]
```css
.container{
      display:grid;
      grid-template-rows:100px 200px;
      grid-template-columns:400px 800px;
    }
```
- If we use fixed width like above then our grid will not be responsive.

#### Shorthand property
```css
.grid-container{
	display:grid;
	grid-template: 100px 200px / 400px 800px;   /* rows/columns */
}
```

```css
.grid-container{
	display:grid;
	grid-template-rows: 100px auto;
	grid-template-columns: 200px auto;
}
```
- auto works differently for row and column
- In row auto just try to fit the content of that item.
- In column auto tries to fit whole width available to parent container.

> [Grid Practice](https://appbrewery.github.io/grid-sizing/)

#### using minmax

```css
.container {
            display: grid;
            grid-template-rows: 200px 400px;
            grid-template-columns:200px minmax(400px,800px);
            gap: 10px;
            
        }
```

- goes max at 800px even if screen is wider
![[Pasted image 20240724195853.png|600]]

- goes min at 400px even if screen becomes narrower the content will overflow in right
![[Pasted image 20240724200000.png|300]]

#### Repeat
```css
.container{
      height:50vh;
      width:50vh;
      display:grid;
      grid-template-columns:1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
      /* We can achieve same no. of columns with repeat */
	  grid-template-columns: repeat(8,1fr); /* 8 times with 1fr size */
    }
```

### `grid-auto-rows`

```html
<style>
        .container {
            display: grid;
            grid-template-rows: 200px 200px;
            grid-template-columns:200px 200px;
            gap: 10px;
            
        }
        div>div{
            background-color:green;
            color:white;
            font-size:28px;
        }
</style>
<body>
    <div class="container">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div></div>
    </div>
</body>
```
There are only 4 div on web page but we have defined 5 div 
![[Pasted image 20240724200837.png|300]]

- on adding element but keeping css same 
```html
<body>
    <div class="container">
        <div>1</div>
        <div>2</div>
        <div>3</div>
        <div>4</div>
        <div>5</div>
    </div>
</body
```
- Now 5th div takes width property from grid but takes height of content ,This is because we are adding single column in 2 column grid.
![[Pasted image 20240724201044.png|200]]

```css
.container {
            display: grid;
            grid-template-rows: 200px 200px;
            grid-template-columns:200px 200px;
            grid-auto-rows:300px;  
            gap: 10px;
            
        }
```
![[Pasted image 20240724201506.png|200]]
On applying the grid-auto-rows the loner item also gets height assigned to it here 300px.

## Chrome developer tools
![[Pasted image 20240724201757.png]]

# Grid Placements
It includes:
- **Lines**: Dividers that define the edges of grid tracks in both the row and column dimensions.
- **Tracks**: Rows or columns created by grid lines, forming the structure of the grid.
- **Cells**: The smallest units in a grid, formed at the intersection of row and column tracks.
- **Container**: The element that contains and defines the grid structure.
- **Items**: The elements placed inside the grid container, positioned within the defined grid cells.


### Centering elements inside item in grid
- Using flexbox inside grid
```css
.container {
      height: 100vh;
      display: grid;
      gap: 3rem;
      grid-template-columns: 1fr 1fr 1.5fr;
      grid-template-rows: 1fr 1fr;
      
    }

    .item {
      font-size: 5rem;
      color: white;
      font-family: Arial, Helvetica, sans-serif;
      background-color: blueviolet;
      /* TODO: Use Flexbox to align the text to the center horizontally and vertically. 
      See goal1 image.
      */
      display:flex;
      justify-content: center;
      align-items: center;
    }
```

![[Pasted image 20240724205632.png|300]]

### `grid-column:span  or grid-row:span`
- It is a shorthand property for grid-column-start and grid-column-end

```css
  height: 100vh;
      display: grid;
      gap: 3rem;
      grid-template-columns: 1fr 1fr 1.5fr;
      grid-template-rows: 1fr 1fr;
    }

    .item {
      font-size: 5rem;
      color: white;
      font-family: Arial, Helvetica, sans-serif;
      background-color: blueviolet;
      display: flex;
      align-items: center;
      justify-content: center;
    }


    .cowboy {
      background-color: #00B9FF;
      grid-column: span 2;
    }
```
- same result from this too.
![[Pasted image 20240724210416.png]]
- grid-column: span is shorthand property for start and end both
![[Pasted image 20240724210048.png]]
- if we do -1 then 
- we can even start at 4 and end at 2 , it works , can also use auto
![[Pasted image 20240724210538.png]]

#### `order`
- use order to move the item to the end of items. Default order of all items is 0.
```css
.astronaut {
      background-color: #03989E;
      order: 1;
      grid-column:span 2;
      /*   OR   */
      grid-column-start:1;
      grid-column-end:3;
      
      /*    And  */
      
      grid-row:span 1;
      /*   OR   */
      grid-row-start:2;  /* as astronaut is inserted in second row */ 
      grid-row-end:3;
      /*   OR   */
      grid-row: 2/3;
    }
```

### `Grid Area`
- It is a shorthand property
```css
.astronaut {
      background-color: #03989E;
      order: 1;
      grid-column-start:1;
      grid-column-end:3;
      grid-row-start:2; 
      grid-row-end:3;
      /* To write all above four parameters in one go*/
      grid-area:2/1/3/3;    row-start/column-start/row-end/column-end
    }
```



# Project

![[Pasted image 20240725104221.png|300]]
	 
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mondrian Project</title>
  <style>
    .container{
      height:748px;
      width:748px;
      margin:auto;
      margin-top:5%;
      background-color: #6d1111;
      display:grid;
      grid-template-columns:320px 9px 198px 9px  153px 9px 50px;
      grid-template-rows:414px 9px 130px 9px 9px 155px 9px 20px; 
      
    }
    .white{
      background-color: #F0F1EC;
    }
    .red{
      background-color: #E72F24;
    }
    .yellow{
      background-color:#F9D01E;
    }
    .black{
      background-color:#232629;
    }
    .blue{
      background-color: #004592;
    }
    .line{
      background-color: #000;
    }
    .col-span-5{
      grid-column:span 5;
    }
   
    .line-full-col{
      grid-column-start:1;
      grid-column-end:8;
    }
    .row-span-4{
      grid-row:span 4;
    }
    .col-span-3{
      grid-column:span 3;
    }
    .row-span-2{
      grid-row:span 2;
    }
    .row-span-3{
      grid-row:span 3;
    }
    .col-span-6{
      grid-column:span 6;
    }
  </style>
</head>

<body>
  <!-- Write your HTML here -->
   <div class="container">
      <div class="red"></div>
      <div class="line"></div>
      <div class="white col-span-5"></div>
      <div class="line line-full-col"></div>
      <div class="white row-span-4"></div>
      <div class="line row-span-4"></div>
      <div class="white row-span-4 col-span-3"></div>
      <div class="line row-span-4"></div>
      <div class="blue"></div>
      <div class="line row-span-2"></div>
      <div class="white row-span-3"></div>
      <div class="line col-span-6"></div>
      <div class="white"></div>
      <div class="line"></div>
      <div class="yellow"></div>
      <div class="line"></div>
      <div class="black"></div>
      <div class="line"></div>
   </div>
</body>

</html>
```

Below code better executed
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mondrian Project</title>
  <style>
    body{
      margin:0;
      padding:0;
      height:100vh;
      display:flex;
      justify-content: center;
      align-items:center;
    }
    .container{
      height:748px;
      width:748px;
      background-color: #000;
      display:grid;
      grid-template-columns:320px 198px 153px 50px;
      grid-template-rows:414px 130px 155px 20px; 
      gap:9px;
    }
    .white{
      background-color: #F0F1EC;
    }
    .red{
      background-color: #E72F24;
    }
    .yellow{
      background-color:#F9D01E;
    }
    .black{
      background-color:#232629;
    }
    .blue{
      background-color: #004592;
      border-bottom:10px solid #000;
    }
    .col-span-3{
      grid-column:span 3;
    }
    .row-span-2{
      grid-row:span 2;
    }
    .col-span-2{
      grid-column:span 2;
    }
  </style>
</head>

<body>
  <!-- Write your HTML here -->
   <div class="container">
      <div class="red"></div>
      <div class="white col-span-3"></div>
      <div class="white row-span-2"></div>
      <div class="white row-span-2 col-span-2"></div>
      <div class="blue"></div>
      <div class="white row-span-2"></div>
      <div class="white"></div>
      <div class="yellow"></div>
      <div class="black"></div>
   </div>
</body>

</html>
```