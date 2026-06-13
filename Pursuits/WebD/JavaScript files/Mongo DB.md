- The greatest factor to decided on whether to use Mongo DB or SQL is
	- what is the type of data , not the structure, but like is it a transactional data (ex: when a person do the checkout then it reserves the quantity from inventory and also a unique id for order is generated and their are many state changes that happen, so to create order their are multiple changes involved, such data is transactional in nature.)
- NoSQL is good for both read and write operation than SQL in general but it's not good for transactional data which happens in multi-threaded environment. 
- So in some scenarios we have to use NoSQL database then there is some scenario where we prefer to use NoSQL database.
- For local development developers uses local database but for production their are vulnerabilities on doing so. Hence now days developers tends to use cloud databases like on `Atlas`. Now it has become so good that it's as easy as using local database even for development.

# Mongoose library
- It provides easier operations for MongoDB. It is ORM(Object Relational Mapping) for MongoDB
- It makes constructing queries easier for developers.
- It's sole purpose to link developers code with database code.


# Clients in MongoDB
- Clients acts as an interface to interact with MongoDB Server.
- There are many clients like:
	- shell
	- compass
	- Node

Install Mongo DB Community Server
```txt
https://fastdl.mongodb.org/windows/mongodb-windows-x86_64-8.2.2-signed.msi
```

Install Mongo DB Shell
```txt
https://downloads.mongodb.com/compass/mongosh-2.5.10-x64.msi
```


Command to run mongo DB
```js
mongod --dbpath .
```

Command to run mongo DB Shell
```bash
mongosh
```
![[Pasted image 20251129112008.png]]


# Basic commands used
```txt
show dbs
use dbname
show collections
db
```

# Creating products database

```bash
admin> use classdb1
switched to db classdb1
classdb1> db
classdb1
classdb1> db.classdb1.createCollection("products")
TypeError: db.classdb1.createCollection is not a function
classdb1> db.classdb1.insertOne({"name" : "Mobile 1"})
{
  acknowledged: true,
  insertedId: ObjectId('692a8b6e4420c8a1a51e2621')
}
classdb1> db.products.insertOne({"name" : "Mobile"})
{
  acknowledged: true,
  insertedId: ObjectId('692a8b974420c8a1a51e2622')
}
classdb1> show collections
classdb1
products
classdb1> db.products.find()
[ { _id: ObjectId('692a8b974420c8a1a51e2622'), name: 'Mobile' } ]
classdb1> db.products.find()
[ { _id: ObjectId('692a8b974420c8a1a51e2622'), name: 'Mobile' } ]
classdb1> db.products.insertOne({"name" : "Mobile 2", price : 20})
{
  acknowledged: true,
  insertedId: ObjectId('692a8c804420c8a1a51e2623')
}
classdb1> db.products.find()
[
  { _id: ObjectId('692a8b974420c8a1a51e2622'), name: 'Mobile' },
  {
    _id: ObjectId('692a8c804420c8a1a51e2623'),
    name: 'Mobile 2',
    price: 20
  }
]
```

Look about Indexing related to mongo DB shell.

>Other technologies to look into
>Nest.js , fastify js



#### Installing Mongoose at backend side

```bash
npm i mongoose
```

It is a middleware connecting our codebase to the database.
- Mongo DB doesn't have any restrictions for requests.
- But restrictions can be imposed by creating Schema in mongoose.
- In mongoose, connection to database is given by `mongoose.connect()`


Flow of code in our codebase and vice versa
```txt
Node.js -> index.js -> routes (products.js) -> model -> database
```

#### Important
Why Mongoose to connect the database?
Its's a library which provides some functions to easily with database. It's like a ORM (Object Relational Mapping). It provides an interface which developer understands then converts it to a form needed by database.
- ORM is a concept which is also supported by mongoose.
- One of the main advantage of ORM is write code in one environment and then run anywhere without any recreation of database by running the same queries.
- Mongoose library also can also put restriction on mongodb code.  So that only valid code is provided by developer. 
If we create mongoose at multiple files then only single instance is created in the first line it was executed then all are just pointers to the same instance.

![[Pasted image 20251225202716.png]]

- Whenever we use mongoose
- In NoSQL we don't need to define any kind of shape but in MongoDB then we do define a shape, `mongo db` at core level doesn't support restriction bcz it's Javascript Object. That doesn't means it doesn't allow any restriction.\

- Model is instance of collection
- To work with mongoose we need to create a schema.
	- It's like the type of data in the collection.
- Now provide the schema to create the model 
	- ![[Pasted image 20251225210134.png|400]]
![[Pasted image 20251225210533.png]]

- Now we can export the model and that will be exposed and can be accessed by route and the functional logic can be implemented there but we don't want a lot of logic in the routes instead write the core logic in the mongoose js itself inside some method which could be called at the routes page
	![[Pasted image 20251225212825.png|300]]

![[Pasted image 20251225213423.png|300]]
- It doesn't return the data , it returns a Promise so we should make use of async
- await here.
![[Pasted image 20251225213512.png|400]]

- Now instead of json data is coming from bson.
![[Pasted image 20251225214518.png|400]]

- Example of exception thrown by `find()` method , these exceptions are expensive and can lead to database crash.
![[Pasted image 20251227102433.png|400]]

Learn about error object in javascript. It is implemented by node.js.


![[Pasted image 20251227103245.png|400]]

![[Pasted image 20251227103254.png|300]]


- Now where we fetch the result that's the same place where to send the data for processing or error handling instead of handling this inside the model from where data is fetched.
- So to reduce the complexity we are using callbacks which acts like references to different routes data can be sent for processing.
![[Pasted image 20251227104046.png|300]]

![[Pasted image 20251227104253.png|300]]


- 404 errors are not handled by catch function but handled by then only as they are not exactly an error but a valid response which means data cannot be accessed which could be due to permission or no such data exists.
- body parser to convert json to string and then their is internal implementation by mongoose to handle the conversion between string and bson in which the data is actually stored in mongoose.

![[Pasted image 20251227121407.png]]

Now to authenticate we will be setting password using hashing string with `bcrypt`.

- We should never modify the request object like once we have created an encrypted password then do not directly modify it in request body but create a new object with spread operator and override to encrypted password there.

![[Pasted image 20260110103702.png]]
- On frontend don't send details like username and password after creation of user , just send message like user created successfully.

- Salt
![[Pasted image 20260110105848.png]]

# JWT
- Don't put any sensitive information in JWT Token as it is quite possible to decode it
- In JWT we have to provide an object which could be any object which can uniquely identify the user
	![[Pasted image 20260110115922.png]]


![[Pasted image 20260110201130.png|300]]

- Core property of JWT token
	- Nobody can temper it but anybody can read it.
	- JWT is self verifiable, their is no need to call any database to verify this.
![[Pasted image 20260110202009.png|300]]

Now the problem with this is logging out
- solution 1 is to remove the token from local storage if logged off. 
	- What if token is residing somewhere else in some api or any other service where that token might still persist. So to solve this old way is used to keep track of expired token in cache.

Why cookies is better to store JWT tokens?
- bcz others can't read the token from there
- it's better for security and prevents cross site scripting.

Issue with using local mongo DB?
- We can't migrate from one environment to another.
- In many companies data is kept on server in LAN and every new member to be add in the team requires to give that member access to the LAN.

What's the solution?
- Use MongoDB Atlas which gives database as a service. It provides UI to setup our database on a server hosted on cloud.

More about JSON token
- JSON token is secure as it can be decrypted but it can be used to increase security at application level by verifying any incoming token with the secret key.
- Unlike JSON web token Cookie doesn't has any specification.


![[Pasted image 20260122210303.png]]
- Browser automatically attach cookie so we don't have to append it.
- Both has to be sent over the internet in http/https requests


- For JWT token email id is enough to generate but anyone can decipher the token and get the data it was made from, so a SECRET KEY is used to decode. Therefore no sensitive info should be put in a token

- Middle ware is just a series of function.