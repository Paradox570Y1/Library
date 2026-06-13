- It is like a flexible container
- We make the parent div flex to use it.
![[Pasted image 20240723082059.png|500]]
_**All the elements inside it don't abide their own properties(like inline, block, inline block) but follows the grid properties**_

> [Flexbox Cheat Sheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
> [Practice by Game](https://appbrewery.github.io/flexboxfroggy/)




- Following are the elements with default display styles.
![[Pasted image 20240723082614.png|500]]
- After applying flexbox , flexbox rules are applied to all.
- As we can see the outer div has display like block.
![[Pasted image 20240723082647.png|500]]

- We can use `display:inline-flex` to make outer div display like inline.
![[Pasted image 20240723083212.png|300]]

### Other ways
![[Pasted image 20240723084809.png]]

![[Pasted image 20240723084831.png]]

![[Pasted image 20240723085258.png]]
![[Pasted image 20240723085343.png|400]]

![[Pasted image 20240723085440.png]]
## Attributes of Flex
`flex-direction:row` (by default)
	-It is set on parent.
	-main axis is from left to right.
	-cross axis is from top to bottom.
![[Pasted image 20240723090141.png|600]]
```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
`flex-direction:column` 
	-It is set on parent.
	-main axis is from top to bottom.
	-cross axis is from left to right.
![[Pasted image 20240723090222.png|500]]

`flex-basis` 
	-It is set on child.
	-It flexis the child inside parent across the main axis.
	-In case of flex-direction column flex-basis is set to height whereas in case of row it set to  width.
![[Pasted image 20240723090830.png|300]]
> Most properties are applied to the main-axis.

`order`
	-It is applied on specific child.
	-By default order of all child is 0.
	-If you increase the order(like order:1;) then that child will be set at last position and if you further increase order of another child then they will be set in increasing order.

`flex-wrap`
	-It is set to parent.
	-Values are: nowrap, wrap, wrap-reverse
	-By default flex-wrap is set to nowrap.
	-If set to wrap then if child doesn't fit the screen then they move to next row.
	-Remember now align-items doesn't work on wrap.
	_[Practical](https://appbrewery.github.io/flex-layout/)_
![[Pasted image 20240723100826.png|400]]


`justify-content`
	-It is set to parent.
	-Values are: flex-start, flex-end, center, space-between, space-around, space-evenly
	-By default it is flex-start
	_[Practical](https://appbrewery.github.io/flex-layout/)_

`align-items`
	-It is set to parent.
	-It is set in cross axis.
	-By default align-items is set to stretch.
	-To apply it we need to set the height of the container(parent).
	-It works only when flex-wrap is set to nowrap(which is by default).
	-Values are: flex-start, flex-end, center, stretch, baseline.
	_[Practical](https://appbrewery.github.io/flex-layout/)_

`align-self`
	-It is set to particular child.
	-On applying it to a child that child works independently with respect to other.
![[Pasted image 20240723094219.png|400]]

`align-content`
	-It is similar to align items but it only works when flex-wrap is set to wrap.
	-Few of its values only work when their is not enough space to accommodate all items.
	_[Practical](https://appbrewery.github.io/flex-layout/)_

# Flex Sizing
![[Pasted image 20240724090428.png]]

- max-width: maximum width of content.
- min-width: maximum width of a word
![[Pasted image 20240724092005.png|400]]
> [Practice here](https://appbrewery.github.io/flexbox-sizing-exercise/)

DEFAULT VALUES
```css
flex-basis:auto;
flex-grow:0;
flex-shrink:1;
```

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
```

![[Pasted image 20240724090659.png]]
![[Pasted image 20240724090717.png|100]]


```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
width:100px;
```
![[Pasted image 20240724090914.png]]
- If container is less than 400px then min-width takes over the set width
![[Pasted image 20240724091007.png|200]]


> flex-basis sets the initial starting value.

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
width:100px; /* Ignored */
flex-basis:200px;/*flex-basis sets the initial starting value.*/
```
![[Pasted image 20240724091149.png]]
- Again if container becomes smaller then the content width then min-width take over
![[Pasted image 20240724091244.png|200]]
> By default flex-basis is `auto` which means width is applied based on content width.

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:200px; /*ignored*/
max-width:100px;
```
- max width determine how much your items can grow to.
![[Pasted image 20240724090914.png]]
![[Pasted image 20240724091244.png|200]]

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:200px; /*ignored*/
min-width:300px;
```
![[Pasted image 20240724092409.png]]
- Min width determine how much your items can shrink to
![[Pasted image 20240724092432.png|500]]

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:100px; /*flex-basis sets the initial starting value.*/
flex-grow:0;
flex-shrink:0;
```
- flex-grow 0 means , your items can't grow.
- flex-shrink 0 means, your items can't shrink.
![[Pasted image 20240724092800.png]]
![[Pasted image 20240724092807.png|240]]

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:100px; /*flex-basis sets the initial starting value.*/
flex-grow:1;
flex-shrink:0;
```
- Since there is plenty space to grow and our flex-items are allowed to grow, they fill up all space.
![[Pasted image 20240724093141.png]]
- As shrink is 0 and flex-basis is 100px, items are not allowed to shrink but maintains 100px width.
![[Pasted image 20240724093322.png|200]]

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:100px; /*flex-basis sets the initial starting value.*/
flex-grow:0; /* By Default*/
flex-shrink:1;/* By Default */
```
- Items are not going to grow but are going to shrink.
![[Pasted image 20240724093529.png]]
![[Pasted image 20240724093555.png|200]]

```css
/* Applied on flex container */
display:flex;
gap:10px;
/* Applied on flex items */
flex-basis:0; /*switching off flex-basis*/
flex-grow:1;
flex-shrink:1;
/*              OR            */
flex: 1 1 0; /*short hand property for : grow shrink basis*/
/*              OR            */
flex:1; /*As it is often used so there is even shorter way to write flex:1 1 0*/
```

![[Pasted image 20240724093922.png]]
![[Pasted image 20240724093936.png|200]]
![[Pasted image 20240724094001.png|100]]

Examples
![[Pasted image 20240724094333.png|500]]
- It's like defining the ratio for grow and shrink.
![[Pasted image 20240724094350.png]]
![[Pasted image 20240724094415.png|100]]


