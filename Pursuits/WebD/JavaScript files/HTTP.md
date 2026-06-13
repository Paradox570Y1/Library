- It's a high level or application level protocol that uses TCP and IP based communication. TCP breaks the packets at sender side and reorganize at receiver's end. 
- It is stateless protocol.
- Every packet is independent of other so every packet asks for permission who can use it based on authorization.
### What is Protocol?
- Defined set of rules for two parties to interact with each other.
- Protocol includes suite of tasks it needs to be perform 

![[Pasted image 20250911203738.png]]

- It occupies the bandwidth as long as packets are not delivered and it freezes the bandwidth when packets are delivered.
- There is no point to point communication.



# HTTP Client - Server

![[Pasted image 20250911203949.png]]


## HTTP Parameters
![[Pasted image 20250911204138.png]]

-  Host google.com
- Learn about HTTP Ports.
![[Pasted image 20250911205644.png]]

Traditional page refresh
![[Pasted image 20250911204844.png]]


![[Pasted image 20250911204932.png]]

- Earlier full page request was sent for even little update  to server and new page after updates is rendered again on frontend.

- On changing web page, full page refresh, but now a part of page can get refreshed instead of full page.

Asynchronous JavaScript and XML
![[Pasted image 20250911204820.png]]

- Fetch is browser method.
- Fetch is  returns a promise along with details.
- It is entirely based on promise.


- Server side content security policy doesn't allow google website's content to be directly accessed from the console.
- make sure when you pass an website link as argument include `http` before it otherwise it appends that link to current page like if you have opened edge browser and use call `fetch("www.google.com");` then it will redirect to `https://edge/www.google.com` which will become invalid then.


- Fetch returns a promise.
![[Pasted image 20250911211501.png|300]]

- Response of fetch.
![[Pasted image 20250911211603.png]]
- Event this Response is a Promise.


- Fetch is not a core method of Javascript.
- Initially when it came it was not fetch but an `XMLHttpRequest` which is a constructor function and that was actually used for making http request and returns a promise. Fetch is just a wrapper on top of it. Now days there are too many wrappers developed over underline implementation.

![[Pasted image 20250911211930.png]]

- This topic is extension of Promise. 
- Primarily Promise is used for API calls.
![[Pasted image 20250911212541.png]]

# How XMLHttpRequest works

```js
var xmlHTTPRequest1 =  new XMLHttpRequest();
xmlHTTPRequest1.open("GET", "http://localhost:8080/data");
xmlHTTPRequest1.send();

xmlHTTPRequest1.onreadystatechange = function () {
  if(vxmlHTTPRequest1.readyState === 4) {
    console.log("Response received from server is: ", xmlHTTPRequest1.response)
  }
}
```


States of `xmlHTTPRequest` : 0 -> open -> fulfilled/ rejected
- Internally there are many states.

![[Pasted image 20250911212943.png]]
![[Pasted image 20250911213051.png]]

- then and catch doesn't work in `XMLHttpRequest` because it doesn't return a Promise like fetch does.

# Now lets implement custom Fetch on top of `XMLHttpRequest`.

```
// Implementing custom fetch using XMLHttpRequest
// Accepts a URL
// Returns a Promise
// The promise is resolved when the data is fetched from the server
```



```js
function customFetch(url) {
  // return Promise;
  return new Promise(executorFunc);

  function executorFunc(resolve, reject) {
    var xmlHTTPRequest1 = new XMLHttpRequest();
    xmlHTTPRequest1.open("GET", url);
    xmlHTTPRequest1.send();

    xmlHTTPRequest1.onreadystatechange = function () {
      if (xmlHTTPRequest1.readyState === 4) {
        console.log(
          "Response received from server is: ",
          xmlHTTPRequest1.response
        );
        resolve(xmlHTTPRequest1.response);
      }
    };
  }
}

var data = customFetch("http://localhost:8080/data");

data.then((response) => {
  console.log("Response from custom fetch is: ", response);
}); 
```

- Above is the one core part of fetch implementation.


# Uses of Promises
- To read a file which is also asynchronous task.
- It can be used for timer and delay using [[sleep in JS]]

