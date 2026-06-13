- [[Attributes in form]]
- [[Forms.pdf]]
```html
<!DOCTYPE html>
<html lang="eng">
    <head>
        <title>Forms</title>
    </head>
    <body>
        <form>
            Name: <input type="text"          name="fname">
            <br><br>
            Class: <input type="text" name="class">
            <br><br>
            Email: <input type="text" name="mail">
            <br><br>
            <input type="submit" name="">
            <br><br>
            <input type="reset" name="">
        </form>
    </body>
    
</html>
```

![[Pasted image 20240708164144.png|200]]
- Now press Submit
- Your html file link will store
	![[Pasted image 20240708164244.png|400]]

##  Placeholder vs Value
```html
<form>
            Name: <input type="text" name="fname" value="Apurav">
            <br><br>
            Class: <input type="text" name="class" placeholder="class">
            <br><br>
            Email: <input type="text" name="mail">
            <br><br>
            <input type="submit" name="">
            <br><br>
            <input type="reset" name="">
        </form>
```

![[Pasted image 20240708164436.png|200]]
![[Pasted image 20240708164616.png|300]]
- class is empty while fname is fill

