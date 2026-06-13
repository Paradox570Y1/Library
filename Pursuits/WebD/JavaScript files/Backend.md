- [[NodeJS]]

# Theory

![[Pasted image 20250107163210.png|300]]


# What is Backend
It consists of three components:
- Server - 24/7 running computer 
- Application - which is basically all the logic that enables web app to function.
- Database - to store and retrieve user data

### Server
As we are going to build websites locally we are going to use  `localhost`, which means using own computer as server. It needs to be on just when we are testing website.

# Application
It is basically the logic that runs on the computer and this logic determines how you want to respond to the requests from the browser.

- Based on logic server can send back another html file, data or even status code.

# Database
This is not a requirement of web applications, but usually when your app becomes more complex and larger, then it's going to store user data and that is what databases are for. Database is what permanently stores data even if server is offline. Otherwise restarting a server will clean all the data.


![[Pasted image 20250107165509.png]]
In backend we can work with any programming language.

The reason why backend language doesn't really matter is as long as you can use something to generate the HTML, CSS, JS files to send back over to the frontend then it doesn't really matter what language you use to do it. 

```d
Frameworks that you might come across over Internet
Rails  (Ruby)
Java Spring Framework (Java)
ASP.NET from Microsoft (C#)
Laravel or Cake (php)
Flask & Django (Python)
Node (JavaScript)
```

# Framework Rankings 
(based on survey on stack overflow by developers)
![[Pasted image 20250107170036.png|300]]

#  Why we require Framework?

> Why can't we directly do the application logic in programming language.

This is because the framework makes job easier by providing built in components without us to need write every single line of code from scratch.
![[Pasted image 20250116153007.png|400]]

# Node
- It is not quite a framework.
- It is an asynchronous event-driven JavaScript runtime.
- Node.js is designed to build scalable network applications.
- It uses V8 Engine.
	- V8 Engine comes from chromium.
	- It is written in C/C++.
	- It's blazingly fast and it powers the chrome browser.
	![[Pasted image 20250116153715.png|200]]

>
	-Earlier the Javascript code was locked in Browser use only but now Node.js liberated the  JavaScript form Browser land and give it freedom to allow us to write any sort of application desktop or server side.
	-Node provides JavaScript runtime so that we can run JavaScript on any machine like our own local computer.

##### Asynchronous Event Driven
- It means your javascript code doesn't have to do everything sequentially.

> *Example of synchronous*
> You ordered something from amazon , now if this process was synchronous then you have to wait until your parcel gets delivered and you can't do anything in mean time.
> So , synchronous means tying up the resources until some sort of event resolves.

>*Example of asynchronous*
>You can initiate the order and instead to wait for it  , it can free up the resources and only when order is delivered then continue execution of next bits of code. So in this way we can trigger the code once an event happens.

> **Summary**
> We need Node bcz it allows us to build an application on a computer using JavaScript and Application is the key aspect of our Backend.
> As we know application is going to run on Server  which is a computer not a browser and hence NodeJS is what allows it to happen.

![[Pasted image 20250117145934.png|400]]
**why we choose Node ?**
- It's easy to transition to backend from frontend as we are using single language.
- Node.js is designed to build scalable network applications.
- It does not block resources as it is asynchronous.
- It has a lot of resources out there like documentation and tutorials.

All the following apps uses NodeJS, Even NASA uses NodeJS
![[Pasted image 20250117150319.png|400]]


![[Pasted image 20250117150448.png|400]]



