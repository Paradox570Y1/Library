- [[border]]
- [[width]] (in percent)
- [[cellpadding]]
- [[colspan]]
- [[rowspan]]
- bgcolor
- cellspacing
- background - to insert image as background of table just assign the link to it.
- border-spacing
- caption

![[Pasted image 20250629161330.png]]

Table structure with semantics
```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8" />
        <title>table page</title>
    </head>
    <body>
        <table border="1"  width="80%" cellpadding="8px" cellspacing="0px"  background="./images/mountain.jpg" bgcolor="black">
            <caption>table1</caption>
            <thead>
                <tr>
                    <th colspan="2">heading1</th>   
                    <th>heading2</th>   
                    <th>heading3</th>   
                </tr>
            </thead>
            
            <tbody>
                <tr>
                    <td rowspan="2">txt1</td>
                    <td>txt2</td>
                    <td>txt3</td>
                    <td>txt4</td>
                </tr>
                <tr>
                    <td>txt2</td>
                    <td>txt3</td>
                    <td>txt4</td>
                </tr>
                <tr>
                    <td>txt1</td>
                    <td>txt2</td>
                    <td>txt3</td>
                    <td>txt4</td>
                </tr>
            </tbody>
        </table>
    </body>
</html>
```


# Making Table dynamic

```java
<table id="data">
        <thead>
            <tr>
                <th>Product name</th>
                <th>Price</th>
                <th>Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Product 1</td>
                <td>$10.00</td>
                <td>This is a great product.</td>
            </tr>
        </tbody>
    </table>
```

Now we may require to add 100's of rows of data so that is done dynamically.
So we will take the help of JavaScript.


# Template literal
- Use backtick to contain multi line string in JavaScript.

![[Pasted image 20250719121244.png]]
Just copy the inside of table in the javascript function.
![[Pasted image 20250719121258.png|400]]
![[Pasted image 20250719122345.png]]

![[Pasted image 20250719122412.png|400]]
![[Pasted image 20250719122424.png]]

