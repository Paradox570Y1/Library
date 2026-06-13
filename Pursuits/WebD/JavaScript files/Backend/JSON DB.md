To install dependency
```bash
npm i -g json-server
```

Now create a json file
```json
{
    "products": [
        {
            "id": "1",
            "name": "Wireless Mouse",
            "price": 25.99,
            "category": "Electronics",
            "stock": 150,
            "image": "https://placehold.co/300x250"
        },
        {
            "id": "2",
            "name": "Bluetooth Headphones",
            "price": 59.99,
            "category": "Electronics",
            "stock": 85,
            "image": "https://placehold.co/300x250"
        },
        {
            "id": "3",
            "name": "Coffee Maker",
            "price": 89.99,
            "category": "Appliances",
            "stock": 40,
            "image": "https://placehold.co/300x250"
        },
        {
            "id": "4",
            "name": "Yoga Mat",
            "price": 19.99,
            "category": "Fitness",
            "stock": 200,
            "image": "https://placehold.co/300x250"
        },
        {
            "id": "5",
            "name": "Desk Lamp",
            "price": 34.99,
            "category": "Furniture",
            "stock": 120,
            "image": "https://placehold.co/300x250"
        }
    ]
}
```

![[Pasted image 20251115100848.png]]

```bash
json-server db.json --port 4000
```

![[Pasted image 20251115100831.png|300]]
![[Pasted image 20251115102957.png]]

![[Pasted image 20251115103859.png]]

![[Pasted image 20251115104858.png]]

![[Pasted image 20251115103951.png]]



![[Pasted image 20251115104729.png]]
- we can add authorization, it can define the criticality of  a request and browser can make use of OPTIONS to handle critical request.


![[Pasted image 20251115112542.png]]

# Server setup

![[Pasted image 20251115112333.png]]

![[Pasted image 20251115112659.png]]

First create HTTP server. Node.js provides the libraries , packages or basic utilities to create a process that can run on our machine as a service.

Old way for building API

```js
var http = require('http');
var port = 5000;
// this helps to create a process which is our server
//all the request will come into createServer method
var server = http.createServer(function(req, res) {
    const reqPath = req ? req.url : null;
    console.log(`Request for ${reqPath} recieved.`);
    // to check if req is not empty
  if(req && reqPath == '/') {
    //check if it's a valid request
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end("Hello world");
  } else if(req && reqPath == '/products') {
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end(`[
        {
            "id": "1",
            "name": "Wireless Mouse",
            "price": 25.99,
            "category": "Electronics",
            "stock": 150,
            "image": "https://placehold.co/300x250"
    }]`);
  } else {
    res.writeHead(404, {'Content-Type': 'text/plain'});
    res.end("Not found");
  }
})

server.listen(port, "localhost", ()=> {
    console.log(`Server is running at http://localhost:${port}/`);
});
```

**Response**
- Status codes
	- success status codes (2xx) - 200,  204(empty response)
		- If empty response then browser will not try to download the response which is a minor performance improvement.

![[Pasted image 20251115115912.png|300]]
![[Pasted image 20251115115918.png|300]]

![[Pasted image 20251115120002.png|300]]
![[Pasted image 20251115120026.png]]

Here we have to handle everything from creating server to handle request everything. But this can be handled by express with far less code.


Configure POSTMAN for next class.
- It is used for api testing or automating testing.

>[Doc of Express](https://expressjs.com/en/5x/api.html)

