- We can manually create a server or make use of Express JS
- Express JS is a library which helps in API development. It just provides wrapper on top of core methods of creating and setting up server.
- BSON (Binary JSON) format used by MongoDB to store data which is finally JSON
- NodeJS server is basically a service running in background.
To fetch data from json
```js
var Data = require("./db.json");// not a good way

const fileSystem = require("fs");
fileSystem.readFile("./db.json", "utf8", (error, data) => {})
```

- Every request has URL and Type which are mandatory attributes of HTTP.
- Before processing the request if want to do authentication , convert to json or do some other stuff then we can use middlewares.

```js
var bodyParser = require("body-parser");//converting the incoming request to json
```

# HW

![[Pasted image 20251120214725.png]]


- Serialization is analogous to `JSON.stringfy()`.
- Deserialization is analogous to `JSON.parse()`;

- OPTIONS request is used to send critical data.

# Modifying database issues
- After creating a body when you want to add new data or modified data to database then it's good to check if that body has valid data or not.
- For that you can use sanitization libraries.
- Behavior of same API code is different when making requests from Postman vs making requests from browser.



> fetch API call for GET method is done by the server.
> fetch API call for POST method is done by client.


>**Behavior of form submission"**
>- If we use a button of type submit which is a form button then we should use `event.preventDefault()`  but if we use some button which is not a form button then it's default behavior doesn't involve reloading the page so in that case `event.preventDefault()` is not needed.

- `UseRef`  hook is used 


> CORS is a feature of browser so CORS error originates from browser and server never does that.
> It is partially thrown by browser and partially handled by server.


- `app.use()` method is used to create middleware.

```js
app.use("/*splat", function (req, res, next)){
  res.header("Access-Control-Allow-Origin", "*");
});
```

- Get request can never have CORS error as it is called by server.

![[Pasted image 20251127202522.png]]

- If instead of allowing particular IP to access the server if we do \* then anyone can access the server although due to authentication they will not be able to login but still they can do DDOS like attack.


- we can make our next project a module by adding `module` to `package.json` 
	Then instead using require we can import the modules
	![[Pasted image 20251127203213.png|400]]
	- default import is done directly like in this image.
	- normal import is done inside of `{}` curly braces.

![[Pasted image 20251127204916.png|400]]


