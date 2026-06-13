- [[#Why Float ?|Why Float ?]]
- [[#Example ->|Example ->]]
- [[History]]
##### Why Float ?
- To make the text wrap around different shape like here.
![[Pasted image 20240718001143.png|250]]
#Values
- left
- right

#clear attribute
```css
footer{
	clear:both;
}
```
![[Pasted image 20240718204349.png|500]]

#### Example ->
![[Pasted image 20240718001622.png|120]]
![[Pasted image 20240718001635.png|250]]

![[Pasted image 20240718001739.png]]
![[Pasted image 20240718001753.png]]


![[Pasted image 20240718001830.png]]
![[Pasted image 20240718001842.png]]

> Only use float to wrap text around image. Do not use it to create complex layout like following.
![[Pasted image 20240718001924.png]]

![[Pasted image 20240718003110.png]]

```html
<!DOCTYPE html>
<html lang="en">

<!-- TODO
1. Make both paragraph elements wrap around the image.
2. Use Float to move the cat div to the left and the dog div to the right.
3. Use clear to make the footer go below both the cat and dog div. -->

<head>
  <meta charset="UTF-8">
  <title>CSS Float</title>
  <style>
    div {
      display: inline-block;
      width: 35%;
    }

    p {
      font-size: 2em;
    }

    .cat {
      background-color: aquamarine;
      float:left;
    }
    img{
      float:left;
    }
    .dog {
      background-color: coral;
      float:right;
    }

    footer {
      text-align: center;
      background-color: blueviolet;
      clear:both;
    }
  </style>
</head>

<body>
  <div class="cat">
    <h2>CatCSS</h2>

    <img src="cat.jpeg" alt="cat in a box" />
    <p class="first-paragraph">Nap all day cat dog hate mouse eat string barf pillow no baths hate everything but kitty
      poochy. Sleep on keyboard
      toy
      mouse squeak roll over. Mesmerizing birds. Poop on grasses licks paws destroy couch intently sniff hand. The dog
      smells
      bad gnaw.</p>
  </div>
  <div class="dog">
    <h2>DogCSS</h2>
    <img src="dog.jpeg" alt="dogs in a box" />
    <p class="second-paragraph">Heckin good boys and girls long woofer big ol wow very biscit long woofer heck what a
      nice
      floof, long doggo noodle
      horse vvv very taste wow. Very taste wow many pats aqua doggo he made many woofs pupperino, puggo doing me a
      frighten.</p>
  </div>

  <footer>Copyright. This is the footer</footer>
</body>

</html>
```


# Practical Learning
```css
.blue{
    background: blue;
}
.green{
    background: green;
}
.red{
    background-color: red;
}
```
![[Pasted image 20240806181937.png|100]]
![[Pasted image 20240806182044.png|400]]
![[Pasted image 20240806182158.png|400]]
![[Pasted image 20240806182246.png|400]]
![[Pasted image 20240806182406.png|400]]
On decreasing the width until it cannot accomodate more div.
![[Pasted image 20240806201400.png|200]]