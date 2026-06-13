```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>CSS Flag Project</title>
  <style>
    /* Write your CSS Code here */
    .flag{
      width:900px;
      height:600px;
      background-color:#ce1126;
      position: relative;
    }
    
    .flag>div{
      height:300px;
      width:100%;
      background-color:#002868;
      position:absolute;
      top:150px;
    }
    .flag>div>div{
      width:200px;
      height: 200px;
      background-color:#ffffff;
      position:relative;
      top:50px;
      left:350px;
      border-radius:50%;
    }
    p{
      margin:0;
      font-size:5rem;
      text-align:center;
      color:white;
    }
    .flag div p{
      color:black;
    }
  </style>
</head>
<body>
  <div class="flag">
    <p>The Flag</p>
    <div>
      <div>
        <p>of Laos</p>
      </div>
    </div>
  </div>
</body>

</html>
```

![[Pasted image 20240716105744.png|400]]
